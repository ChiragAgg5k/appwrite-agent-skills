---
name: appwrite-typescript
description: Appwrite TypeScript SDK skill. Use when building browser-based JavaScript/TypeScript apps, React Native mobile apps, or server-side Node.js/Deno backends with Appwrite. Covers client-side auth (email, OAuth, anonymous), database queries, file uploads, real-time subscriptions, and server-side admin via API keys for user management, database administration, storage, and functions.
---


# Appwrite TypeScript SDK

## Installation

```bash
# Web
npm install appwrite

# React Native
npm install react-native-appwrite

# Node.js / Deno
npm install node-appwrite
```

## Setting Up the Client

### Client-side (Web / React Native)

```typescript
// Web
import { Client, Account, TablesDB, Storage, ID, Query } from 'appwrite';

// React Native
import { Client, Account, TablesDB, Storage, ID, Query } from 'react-native-appwrite';

const client = new Client()
    .setEndpoint('https://<REGION>.cloud.appwrite.io/v1')
    .setProject('[PROJECT_ID]');
```

### Server-side (Node.js / Deno)

```typescript
import { Client, Users, TablesDB, Storage, Functions, ID, Query } from 'node-appwrite';

const client = new Client()
    .setEndpoint('https://<REGION>.cloud.appwrite.io/v1')
    .setProject(process.env.APPWRITE_PROJECT_ID)
    .setKey(process.env.APPWRITE_API_KEY);
```

## Code Examples

### Authentication (client-side)

```typescript
const account = new Account(client);

// Email signup
await account.create({
    userId: ID.unique(),
    email: 'user@example.com',
    password: 'password123',
    name: 'User Name'
});

// Email login
const session = await account.createEmailPasswordSession({
    email: 'user@example.com',
    password: 'password123'
});

// OAuth login
account.createOAuth2Session({
    provider: 'github',
    success: 'https://example.com/success',
    failure: 'https://example.com/fail'
});

// Get current user
const user = await account.get();

// Logout
await account.deleteSession({ sessionId: 'current' });
```

### User Management (server-side)

```typescript
const users = new Users(client);

// Create user
const user = await users.create({
    userId: ID.unique(),
    email: 'user@example.com',
    password: 'password123',
    name: 'User Name'
});

// List users
const list = await users.list({ queries: [Query.limit(25)] });

// Get user
const fetched = await users.get({ userId: '[USER_ID]' });

// Delete user
await users.delete({ userId: '[USER_ID]' });
```

### Database Operations

> **Note:** Use `TablesDB` (not the deprecated `Databases` class) for all new code. Only use `Databases` if the existing codebase already relies on it or the user explicitly requests it.

```typescript
const tablesDB = new TablesDB(client);

// Create database (server-side only)
const db = await tablesDB.create({ databaseId: ID.unique(), name: 'My Database' });

// Create table (server-side only)
const col = await tablesDB.createTable({
    databaseId: '[DATABASE_ID]',
    tableId: ID.unique(),
    name: 'My Table'
});

// Create row
const doc = await tablesDB.createRow({
    databaseId: '[DATABASE_ID]',
    tableId: '[TABLE_ID]',
    rowId: ID.unique(),
    data: { title: 'Hello World', content: 'Example content' }
});

// List rows with query
const results = await tablesDB.listRows({
    databaseId: '[DATABASE_ID]',
    tableId: '[TABLE_ID]',
    queries: [Query.equal('status', 'active'), Query.limit(10)]
});

// Get row
const row = await tablesDB.getRow({
    databaseId: '[DATABASE_ID]',
    tableId: '[TABLE_ID]',
    rowId: '[ROW_ID]'
});

// Update row
await tablesDB.updateRow({
    databaseId: '[DATABASE_ID]',
    tableId: '[TABLE_ID]',
    rowId: '[ROW_ID]',
    data: { title: 'Updated Title' }
});

// Delete row
await tablesDB.deleteRow({
    databaseId: '[DATABASE_ID]',
    tableId: '[TABLE_ID]',
    rowId: '[ROW_ID]'
});
```

### File Storage

```typescript
const storage = new Storage(client);

// Upload file (client-side — from file input)
const file = await storage.createFile({
    bucketId: '[BUCKET_ID]',
    fileId: ID.unique(),
    file: document.getElementById('file-input').files[0]
});

// Upload file (server-side — from path)
import { InputFile } from 'node-appwrite/file';

const file2 = await storage.createFile({
    bucketId: '[BUCKET_ID]',
    fileId: ID.unique(),
    file: InputFile.fromPath('/path/to/file.png', 'file.png')
});

// List files
const files = await storage.listFiles({ bucketId: '[BUCKET_ID]' });

// Get file preview (image)
const preview = storage.getFilePreview({
    bucketId: '[BUCKET_ID]',
    fileId: '[FILE_ID]',
    width: 300,
    height: 300
});

// Download file
const download = await storage.getFileDownload({
    bucketId: '[BUCKET_ID]',
    fileId: '[FILE_ID]'
});

// Delete file
await storage.deleteFile({ bucketId: '[BUCKET_ID]', fileId: '[FILE_ID]' });
```

### Real-time Subscriptions (client-side)

```typescript
// Subscribe to row changes
const unsubscribe = client.subscribe('databases.[DATABASE_ID].tables.[TABLE_ID].rows', (response) => {
    console.log(response.payload);
});

// Subscribe to file changes
client.subscribe('buckets.[BUCKET_ID].files', (response) => {
    console.log(response.payload);
});

// Unsubscribe
unsubscribe();
```

### Serverless Functions (server-side)

```typescript
const functions = new Functions(client);

// Execute function
const execution = await functions.createExecution({
    functionId: '[FUNCTION_ID]',
    body: JSON.stringify({ key: 'value' })
});

// List executions
const executions = await functions.listExecutions({ functionId: '[FUNCTION_ID]' });
```

### Server-Side Rendering (SSR) Authentication

SSR apps (Next.js, SvelteKit, Nuxt, Remix, Astro) use the **server SDK** (`node-appwrite`) to handle auth. You need two clients:

- **Admin client** — uses an API key, creates sessions, bypasses rate limits (reusable singleton)
- **Session client** — uses a session cookie, acts on behalf of a user (create per-request, never share)

```typescript
import { Client, Account, OAuthProvider } from 'node-appwrite';

// Admin client (reusable)
const adminClient = new Client()
    .setEndpoint('https://<REGION>.cloud.appwrite.io/v1')
    .setProject('[PROJECT_ID]')
    .setKey(process.env.APPWRITE_API_KEY);

// Session client (create per-request)
const sessionClient = new Client()
    .setEndpoint('https://<REGION>.cloud.appwrite.io/v1')
    .setProject('[PROJECT_ID]');

const session = req.cookies['a_session_[PROJECT_ID]'];
if (session) {
    sessionClient.setSession(session);
}
```

#### Email/Password Login

```typescript
app.post('/login', async (req, res) => {
    const account = new Account(adminClient);
    const session = await account.createEmailPasswordSession({
        email: req.body.email,
        password: req.body.password,
    });

    // Cookie name must be a_session_<PROJECT_ID>
    res.cookie('a_session_[PROJECT_ID]', session.secret, {
        httpOnly: true,
        secure: true,
        sameSite: 'strict',
        expires: new Date(session.expire),
        path: '/',
    });

    res.json({ success: true });
});
```

#### Authenticated Requests

```typescript
app.get('/user', async (req, res) => {
    const session = req.cookies['a_session_[PROJECT_ID]'];
    if (!session) return res.status(401).json({ error: 'Unauthorized' });

    // Create a fresh session client per request
    const sessionClient = new Client()
        .setEndpoint('https://<REGION>.cloud.appwrite.io/v1')
        .setProject('[PROJECT_ID]')
        .setSession(session);

    const account = new Account(sessionClient);
    const user = await account.get();
    res.json(user);
});
```

#### OAuth2 SSR Flow

```typescript
// Step 1: Redirect to OAuth provider
app.get('/oauth', async (req, res) => {
    const account = new Account(adminClient);
    const redirectUrl = await account.createOAuth2Token({
        provider: OAuthProvider.Github,
        success: 'https://example.com/oauth/success',
        failure: 'https://example.com/oauth/failure',
    });
    res.redirect(redirectUrl);
});

// Step 2: Handle callback — exchange token for session
app.get('/oauth/success', async (req, res) => {
    const account = new Account(adminClient);
    const session = await account.createSession({
        userId: req.query.userId,
        secret: req.query.secret,
    });

    res.cookie('a_session_[PROJECT_ID]', session.secret, {
        httpOnly: true, secure: true, sameSite: 'strict',
        expires: new Date(session.expire), path: '/',
    });
    res.json({ success: true });
});
```

> **Cookie security:** Always use `httpOnly`, `secure`, and `sameSite: 'strict'` to prevent XSS. The cookie name must be `a_session_<PROJECT_ID>`.

> **Forwarding user agent:** Call `sessionClient.setForwardedUserAgent(req.headers['user-agent'])` to record the end-user's browser info for debugging and security.

## Permissions & Roles (Critical)

Appwrite uses permission strings to control access to resources. Each permission pairs an action (`read`, `update`, `delete`, `create`, or `write` which grants create + update + delete) with a role target. By default, **no user has access** unless permissions are explicitly set at the document/file level or inherited from the collection/bucket settings. Permissions are arrays of strings built with the `Permission` and `Role` helpers.

```typescript
import { Permission, Role } from 'appwrite';
// Server-side: import from 'node-appwrite'
```

### Database Row with Permissions

```typescript
const doc = await tablesDB.createRow({
    databaseId: '[DATABASE_ID]',
    tableId: '[TABLE_ID]',
    rowId: ID.unique(),
    data: { title: 'Hello World' },
    permissions: [
        Permission.read(Role.user('[USER_ID]')),     // specific user can read
        Permission.update(Role.user('[USER_ID]')),   // specific user can update
        Permission.read(Role.team('[TEAM_ID]')),     // all team members can read
        Permission.read(Role.any()),                 // anyone (including guests) can read
    ]
});
```

### File Upload with Permissions

```typescript
const file = await storage.createFile({
    bucketId: '[BUCKET_ID]',
    fileId: ID.unique(),
    file: document.getElementById('file-input').files[0],
    permissions: [
        Permission.read(Role.any()),
        Permission.update(Role.user('[USER_ID]')),
        Permission.delete(Role.user('[USER_ID]')),
    ]
});
```

> **When to set permissions:** Set document/file-level permissions when you need per-resource access control. If all documents in a collection share the same rules, configure permissions at the collection/bucket level and leave document permissions empty.

> **Common mistakes:**
> - **Forgetting permissions** — the resource becomes inaccessible to all users (including the creator)
> - **`Role.any()` with `write`/`update`/`delete`** — allows any user, including unauthenticated guests, to modify or remove the resource
> - **`Permission.read(Role.any())` on sensitive data** — makes the resource publicly readable

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
