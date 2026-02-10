---
name: appwrite-ruby
description: Appwrite Ruby SDK skill. Use when building server-side Ruby applications with Appwrite, including Rails and Sinatra integrations. Covers user management, database/table CRUD, file storage, and functions via API keys.
---


# Appwrite Ruby SDK

## Installation

```bash
gem install appwrite
```

## Setting Up the Client

```ruby
require 'appwrite'

include Appwrite

client = Client.new
    .set_endpoint('https://<REGION>.cloud.appwrite.io/v1')
    .set_project(ENV['APPWRITE_PROJECT_ID'])
    .set_key(ENV['APPWRITE_API_KEY'])
```

## Code Examples

### User Management

```ruby
users = Users.new(client)

# Create user
user = users.create(user_id: ID.unique, email: 'user@example.com', password: 'password123', name: 'User Name')

# List users
list = users.list(queries: [Query.limit(25)])

# Get user
fetched = users.get(user_id: '[USER_ID]')

# Delete user
users.delete(user_id: '[USER_ID]')
```

### Database Operations

> **Note:** Use `TablesDB` (not the deprecated `Databases` class) for all new code. Only use `Databases` if the existing codebase already relies on it or the user explicitly requests it.

```ruby
tables_db = TablesDB.new(client)

# Create database
db = tables_db.create(database_id: ID.unique, name: 'My Database')

# Create row
doc = tables_db.create_row(
    database_id: '[DATABASE_ID]',
    table_id: '[TABLE_ID]',
    row_id: ID.unique,
    data: { title: 'Hello World' }
)

# Query rows
results = tables_db.list_rows(
    database_id: '[DATABASE_ID]',
    table_id: '[TABLE_ID]',
    queries: [Query.equal('title', 'Hello World'), Query.limit(10)]
)

# Get row
row = tables_db.get_row(database_id: '[DATABASE_ID]', table_id: '[TABLE_ID]', row_id: '[ROW_ID]')

# Update row
tables_db.update_row(
    database_id: '[DATABASE_ID]',
    table_id: '[TABLE_ID]',
    row_id: '[ROW_ID]',
    data: { title: 'Updated' }
)

# Delete row
tables_db.delete_row(database_id: '[DATABASE_ID]', table_id: '[TABLE_ID]', row_id: '[ROW_ID]')
```

### File Storage

```ruby
storage = Storage.new(client)

# Upload file
file = storage.create_file(bucket_id: '[BUCKET_ID]', file_id: ID.unique, file: InputFile.from_path('/path/to/file.png'))

# List files
files = storage.list_files(bucket_id: '[BUCKET_ID]')

# Delete file
storage.delete_file(bucket_id: '[BUCKET_ID]', file_id: '[FILE_ID]')
```

### Serverless Functions

```ruby
functions = Functions.new(client)

# Execute function
execution = functions.create_execution(function_id: '[FUNCTION_ID]', body: '{"key": "value"}')

# List executions
executions = functions.list_executions(function_id: '[FUNCTION_ID]')
```

### Server-Side Rendering (SSR) Authentication

SSR apps using Ruby frameworks (Rails, Sinatra, etc.) use the **server SDK** to handle auth. You need two clients:

- **Admin client** — uses an API key, creates sessions, bypasses rate limits (reusable singleton)
- **Session client** — uses a session cookie, acts on behalf of a user (create per-request, never share)

```ruby
require 'appwrite'
include Appwrite

# Admin client (reusable)
admin_client = Client.new
    .set_endpoint('https://<REGION>.cloud.appwrite.io/v1')
    .set_project('[PROJECT_ID]')
    .set_key(ENV['APPWRITE_API_KEY'])

# Session client (create per-request)
session_client = Client.new
    .set_endpoint('https://<REGION>.cloud.appwrite.io/v1')
    .set_project('[PROJECT_ID]')

session = cookies['a_session_[PROJECT_ID]']
session_client.set_session(session) if session
```

#### Email/Password Login (Sinatra)

```ruby
post '/login' do
    account = Account.new(admin_client)
    session = account.create_email_password_session(
        email: params[:email],
        password: params[:password]
    )

    # Cookie name must be a_session_<PROJECT_ID>
    response.set_cookie('a_session_[PROJECT_ID]', {
        value: session.secret,
        httponly: true,
        secure: true,
        same_site: :strict,
        path: '/',
    })

    content_type :json
    { success: true }.to_json
end
```

#### Authenticated Requests

```ruby
get '/user' do
    session = request.cookies['a_session_[PROJECT_ID]']
    halt 401, { error: 'Unauthorized' }.to_json unless session

    session_client = Client.new
        .set_endpoint('https://<REGION>.cloud.appwrite.io/v1')
        .set_project('[PROJECT_ID]')
        .set_session(session)

    account = Account.new(session_client)
    user = account.get

    content_type :json
    user.to_json
end
```

#### OAuth2 SSR Flow

```ruby
# Step 1: Redirect to OAuth provider
get '/oauth' do
    account = Account.new(admin_client)
    redirect_url = account.create_o_auth2_token(
        provider: OAuthProvider::GITHUB,
        success: 'https://example.com/oauth/success',
        failure: 'https://example.com/oauth/failure'
    )
    redirect redirect_url
end

# Step 2: Handle callback — exchange token for session
get '/oauth/success' do
    account = Account.new(admin_client)
    session = account.create_session(
        user_id: params[:userId],
        secret: params[:secret]
    )

    response.set_cookie('a_session_[PROJECT_ID]', {
        value: session.secret,
        httponly: true, secure: true, same_site: :strict, path: '/',
    })

    content_type :json
    { success: true }.to_json
end
```

> **Cookie security:** Always use `httponly`, `secure`, and `same_site: :strict` to prevent XSS. The cookie name must be `a_session_<PROJECT_ID>`.

> **Forwarding user agent:** Call `session_client.set_forwarded_user_agent(request.user_agent)` to record the end-user's browser info for debugging and security.

## Permissions & Roles (Critical)

Appwrite uses permission strings to control access to resources. Each permission pairs an action (`read`, `update`, `delete`, `create`, or `write` which grants create + update + delete) with a role target. By default, **no user has access** unless permissions are explicitly set at the document/file level or inherited from the collection/bucket settings. Permissions are arrays of strings built with the `Permission` and `Role` helpers.

```ruby
# Permission and Role are included in the main require
require 'appwrite'
include Appwrite
```

### Database Row with Permissions

```ruby
doc = tables_db.create_row(
    database_id: '[DATABASE_ID]',
    table_id: '[TABLE_ID]',
    row_id: ID.unique,
    data: { title: 'Hello World' },
    permissions: [
        Permission.read(Role.user('[USER_ID]')),     # specific user can read
        Permission.update(Role.user('[USER_ID]')),   # specific user can update
        Permission.read(Role.team('[TEAM_ID]')),     # all team members can read
        Permission.read(Role.any),                   # anyone (including guests) can read
    ]
)
```

### File Upload with Permissions

```ruby
file = storage.create_file(
    bucket_id: '[BUCKET_ID]',
    file_id: ID.unique,
    file: InputFile.from_path('/path/to/file.png'),
    permissions: [
        Permission.read(Role.any),
        Permission.update(Role.user('[USER_ID]')),
        Permission.delete(Role.user('[USER_ID]')),
    ]
)
```

> **When to set permissions:** Set document/file-level permissions when you need per-resource access control. If all documents in a collection share the same rules, configure permissions at the collection/bucket level and leave document permissions empty.

> **Common mistakes:**
> - **Forgetting permissions** — the resource becomes inaccessible to all users (including the creator)
> - **`Role.any` with `write`/`update`/`delete`** — allows any user, including unauthenticated guests, to modify or remove the resource
> - **`Permission.read(Role.any)` on sensitive data** — makes the resource publicly readable

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
