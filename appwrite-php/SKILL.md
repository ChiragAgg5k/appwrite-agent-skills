---
name: appwrite-php
description: Appwrite PHP SDK skill. Use when building server-side PHP applications with Appwrite, including Laravel and Symfony integrations. Covers user management, database/table CRUD, file storage, and functions via API keys.
---


# Appwrite PHP SDK

## Installation

```bash
composer require appwrite/appwrite
```

## Setting Up the Client

```php
use Appwrite\Client;
use Appwrite\ID;
use Appwrite\Query;
use Appwrite\Services\Users;
use Appwrite\Services\TablesDB;
use Appwrite\Services\Storage;
use Appwrite\Services\Functions;
use Appwrite\InputFile;

$client = (new Client())
    ->setEndpoint('https://<REGION>.cloud.appwrite.io/v1')
    ->setProject(getenv('APPWRITE_PROJECT_ID'))
    ->setKey(getenv('APPWRITE_API_KEY'));
```

## Code Examples

### User Management

```php
$users = new Users($client);

// Create user
$user = $users->create(ID::unique(), 'user@example.com', null, 'password123', 'User Name');

// List users
$list = $users->list([Query::limit(25)]);

// Get user
$fetched = $users->get('[USER_ID]');

// Delete user
$users->delete('[USER_ID]');
```

### Database Operations

> **Note:** Use `TablesDB` (not the deprecated `Databases` class) for all new code. Only use `Databases` if the existing codebase already relies on it or the user explicitly requests it.

```php
$tablesDB = new TablesDB($client);

// Create database
$db = $tablesDB->create(ID::unique(), 'My Database');

// Create row
$doc = $tablesDB->createRow('[DATABASE_ID]', '[TABLE_ID]', ID::unique(), [
    'title' => 'Hello World'
]);

// Query rows
$results = $tablesDB->listRows('[DATABASE_ID]', '[TABLE_ID]', [
    Query::equal('title', ['Hello World']),
    Query::limit(10)
]);

// Get row
$row = $tablesDB->getRow('[DATABASE_ID]', '[TABLE_ID]', '[ROW_ID]');

// Update row
$tablesDB->updateRow('[DATABASE_ID]', '[TABLE_ID]', '[ROW_ID]', [
    'title' => 'Updated'
]);

// Delete row
$tablesDB->deleteRow('[DATABASE_ID]', '[TABLE_ID]', '[ROW_ID]');
```

### File Storage

```php
$storage = new Storage($client);

// Upload file
$file = $storage->createFile('[BUCKET_ID]', ID::unique(), InputFile::withPath('/path/to/file.png'));

// List files
$files = $storage->listFiles('[BUCKET_ID]');

// Delete file
$storage->deleteFile('[BUCKET_ID]', '[FILE_ID]');
```

### Serverless Functions

```php
$functions = new Functions($client);

// Execute function
$execution = $functions->createExecution('[FUNCTION_ID]', '{"key": "value"}');

// List executions
$executions = $functions->listExecutions('[FUNCTION_ID]');
```

### Server-Side Rendering (SSR) Authentication

SSR apps (Laravel, Symfony, etc.) use the **server SDK** to handle auth. You need two clients:

- **Admin client** — uses an API key, creates sessions, bypasses rate limits (reusable singleton)
- **Session client** — uses a session cookie, acts on behalf of a user (create per-request, never share)

```php
use Appwrite\Client;
use Appwrite\Services\Account;

// Admin client (reusable)
$adminClient = (new Client())
    ->setEndpoint('https://<REGION>.cloud.appwrite.io/v1')
    ->setProject('[PROJECT_ID]')
    ->setKey(getenv('APPWRITE_API_KEY'));

// Session client (create per-request)
$sessionClient = (new Client())
    ->setEndpoint('https://<REGION>.cloud.appwrite.io/v1')
    ->setProject('[PROJECT_ID]');

$session = $_COOKIE['a_session_[PROJECT_ID]'] ?? null;
if ($session) {
    $sessionClient->setSession($session);
}
```

#### Email/Password Login

```php
$account = new Account($adminClient);
$session = $account->createEmailPasswordSession($email, $password);

// Cookie name must be a_session_<PROJECT_ID>
setcookie('a_session_[PROJECT_ID]', $session['secret'], [
    'httpOnly' => true,
    'secure' => true,
    'sameSite' => 'strict',
    'expires' => strtotime($session['expire']),
    'path' => '/',
]);
```

#### Authenticated Requests

```php
$session = $_COOKIE['a_session_[PROJECT_ID]'] ?? null;
if (!$session) {
    http_response_code(401);
    exit;
}

$sessionClient->setSession($session);
$account = new Account($sessionClient);
$user = $account->get();
```

#### OAuth2 SSR Flow

```php
// Step 1: Redirect to OAuth provider
$account = new Account($adminClient);
$redirectUrl = $account->createOAuth2Token(
    OAuthProvider::GITHUB(),
    'https://example.com/oauth/success',
    'https://example.com/oauth/failure',
);
header('Location: ' . $redirectUrl);

// Step 2: Handle callback — exchange token for session
$account = new Account($adminClient);
$session = $account->createSession($_GET['userId'], $_GET['secret']);

setcookie('a_session_[PROJECT_ID]', $session['secret'], [
    'httpOnly' => true, 'secure' => true, 'sameSite' => 'strict',
    'expires' => strtotime($session['expire']), 'path' => '/',
]);
```

> **Cookie security:** Always use `httpOnly`, `secure`, and `sameSite: 'strict'` to prevent XSS. The cookie name must be `a_session_<PROJECT_ID>`.

> **Forwarding user agent:** Call `$sessionClient->setForwardedUserAgent($_SERVER['HTTP_USER_AGENT'])` to record the end-user's browser info for debugging and security.

## Permissions & Roles (Critical)

Appwrite uses permission strings to control access to resources. Each permission pairs an action (`read`, `update`, `delete`, `create`, or `write` which grants create + update + delete) with a role target. By default, **no user has access** unless permissions are explicitly set at the document/file level or inherited from the collection/bucket settings. Permissions are arrays of strings built with the `Permission` and `Role` helpers.

```php
use Appwrite\Permission;
use Appwrite\Role;
```

### Database Row with Permissions

```php
$doc = $tablesDB->createRow('[DATABASE_ID]', '[TABLE_ID]', ID::unique(), [
    'title' => 'Hello World'
], [
    Permission::read(Role::user('[USER_ID]')),     // specific user can read
    Permission::update(Role::user('[USER_ID]')),   // specific user can update
    Permission::read(Role::team('[TEAM_ID]')),     // all team members can read
    Permission::read(Role::any()),                 // anyone (including guests) can read
]);
```

### File Upload with Permissions

```php
$file = $storage->createFile('[BUCKET_ID]', ID::unique(), InputFile::withPath('/path/to/file.png'), [
    Permission::read(Role::any()),
    Permission::update(Role::user('[USER_ID]')),
    Permission::delete(Role::user('[USER_ID]')),
]);
```

> **When to set permissions:** Set document/file-level permissions when you need per-resource access control. If all documents in a collection share the same rules, configure permissions at the collection/bucket level and leave document permissions empty.

> **Common mistakes:**
> - **Forgetting permissions** — the resource becomes inaccessible to all users (including the creator)
> - **`Role::any()` with `write`/`update`/`delete`** — allows any user, including unauthenticated guests, to modify or remove the resource
> - **`Permission::read(Role::any())` on sensitive data** — makes the resource publicly readable

## API Reference

For complete method documentation, see the reference files:

- [Account](references/account.md) — The Account service allows you to authenticate and manage a user account.
- [Avatars](references/avatars.md) — The Avatars service aims to help you complete everyday tasks related to your app image, icons, and avatars.
- [Assistant](references/assistant.md)
- [Console](references/console.md) — The Console service allows you to interact with console relevant information.
- [Databases](references/databases.md) — The Databases service allows you to create structured collections of documents, query and filter lists of documents
- [Functions](references/functions.md) — The Functions Service allows you view, create and manage your Cloud Functions.
- [Graphql](references/graphql.md) — The GraphQL API allows you to query and mutate your Appwrite server using GraphQL.
- [Health](references/health.md) — The Health service allows you to both validate and monitor your Appwrite server&#039;s health.
- [Locale](references/locale.md) — The Locale service allows you to customize your app based on your users&#039; location.
- [Messaging](references/messaging.md) — The Messaging service allows you to send messages to any provider type (SMTP, push notification, SMS, etc.).
- [Migrations](references/migrations.md) — The Migrations service allows you to migrate third-party data to your Appwrite project.
- [Project](references/project.md) — The Project service allows you to manage all the projects in your Appwrite server.
- [Projects](references/projects.md) — The Project service allows you to manage all the projects in your Appwrite server.
- [Proxy](references/proxy.md) — The Proxy Service allows you to configure actions for your domains beyond DNS configuration.
- [Sites](references/sites.md) — The Sites Service allows you view, create and manage your web applications.
- [Storage](references/storage.md) — The Storage service allows you to manage your project files.
- [TablesDB](references/tablesdb.md)
- [Teams](references/teams.md) — The Teams service allows you to group users of your project and to enable them to share read and write access to your project resources
- [Tokens](references/tokens.md)
- [Users](references/users.md) — The Users service allows you to manage your project users.
- [Vcs](references/vcs.md)
