---
name: appwrite-python
description: Appwrite Python SDK skill. Use when building server-side Python applications with Appwrite, including Django, Flask, and FastAPI integrations. Covers user management, database/table CRUD, file storage, and functions via API keys.
---


# Appwrite Python SDK

## Installation

```bash
pip install appwrite
```

## Setting Up the Client

```python
from appwrite.client import Client
from appwrite.id import ID
from appwrite.query import Query
from appwrite.services.users import Users
from appwrite.services.tablesdb import TablesDB
from appwrite.services.storage import Storage
from appwrite.services.functions import Functions
from appwrite.enums.o_auth_provider import OAuthProvider

import os

client = (Client()
    .set_endpoint('https://<REGION>.cloud.appwrite.io/v1')
    .set_project(os.environ['APPWRITE_PROJECT_ID'])
    .set_key(os.environ['APPWRITE_API_KEY']))
```

## Code Examples

### User Management

```python
users = Users(client)

# Create user
user = users.create(ID.unique(), 'user@example.com', None, 'password123', 'User Name')

# List users
result = users.list([Query.limit(25)])

# Get user
fetched = users.get('[USER_ID]')

# Delete user
users.delete('[USER_ID]')
```

### Database Operations

> **Note:** Use `TablesDB` (not the deprecated `Databases` class) for all new code. Only use `Databases` if the existing codebase already relies on it or the user explicitly requests it.

```python
tables_db = TablesDB(client)

# Create database
db = tables_db.create(ID.unique(), 'My Database')

# Create row
doc = tables_db.create_row('[DATABASE_ID]', '[TABLE_ID]', ID.unique(), {
    'title': 'Hello World'
})

# Query rows
results = tables_db.list_rows('[DATABASE_ID]', '[TABLE_ID]', [
    Query.equal('title', 'Hello World'),
    Query.limit(10)
])

# Get row
row = tables_db.get_row('[DATABASE_ID]', '[TABLE_ID]', '[ROW_ID]')

# Update row
tables_db.update_row('[DATABASE_ID]', '[TABLE_ID]', '[ROW_ID]', {
    'title': 'Updated'
})

# Delete row
tables_db.delete_row('[DATABASE_ID]', '[TABLE_ID]', '[ROW_ID]')
```

### File Storage

```python
from appwrite.input_file import InputFile

storage = Storage(client)

# Upload file
file = storage.create_file('[BUCKET_ID]', ID.unique(), InputFile.from_path('/path/to/file.png'))

# List files
files = storage.list_files('[BUCKET_ID]')

# Delete file
storage.delete_file('[BUCKET_ID]', '[FILE_ID]')
```

### Serverless Functions

```python
functions = Functions(client)

# Execute function
execution = functions.create_execution('[FUNCTION_ID]', body='{"key": "value"}')

# List executions
executions = functions.list_executions('[FUNCTION_ID]')
```

### Server-Side Rendering (SSR) Authentication

SSR apps (Flask, Django, FastAPI, etc.) use the **server SDK** to handle auth. You need two clients:

- **Admin client** — uses an API key, creates sessions, bypasses rate limits (reusable singleton)
- **Session client** — uses a session cookie, acts on behalf of a user (create per-request, never share)

```python
from appwrite.client import Client
from appwrite.services.account import Account
from flask import request, jsonify, make_response, redirect

# Admin client (reusable)
admin_client = (Client()
    .set_endpoint('https://<REGION>.cloud.appwrite.io/v1')
    .set_project('[PROJECT_ID]')
    .set_key(os.environ['APPWRITE_API_KEY']))

# Session client (create per-request)
session_client = (Client()
    .set_endpoint('https://<REGION>.cloud.appwrite.io/v1')
    .set_project('[PROJECT_ID]'))

session = request.cookies.get('a_session_[PROJECT_ID]')
if session:
    session_client.set_session(session)
```

#### Email/Password Login

```python
@app.post('/login')
def login():
    account = Account(admin_client)
    session = account.create_email_password_session(
        request.json['email'], request.json['password']
    )

    # Cookie name must be a_session_<PROJECT_ID>
    resp = make_response(jsonify({'success': True}))
    resp.set_cookie('a_session_[PROJECT_ID]', session['secret'],
                    httponly=True, secure=True, samesite='Strict',
                    expires=session['expire'], path='/')
    return resp
```

#### Authenticated Requests

```python
@app.get('/user')
def get_user():
    session = request.cookies.get('a_session_[PROJECT_ID]')
    if not session:
        return jsonify({'error': 'Unauthorized'}), 401

    session_client = (Client()
        .set_endpoint('https://<REGION>.cloud.appwrite.io/v1')
        .set_project('[PROJECT_ID]')
        .set_session(session))

    account = Account(session_client)
    return jsonify(account.get())
```

#### OAuth2 SSR Flow

```python
# Step 1: Redirect to OAuth provider
@app.get('/oauth')
def oauth():
    account = Account(admin_client)
    redirect_url = account.create_o_auth2_token(
        OAuthProvider.Github,
        'https://example.com/oauth/success',
        'https://example.com/oauth/failure',
    )
    return redirect(redirect_url)

# Step 2: Handle callback — exchange token for session
@app.get('/oauth/success')
def oauth_success():
    account = Account(admin_client)
    session = account.create_session(request.args['userId'], request.args['secret'])

    resp = make_response(jsonify({'success': True}))
    resp.set_cookie('a_session_[PROJECT_ID]', session['secret'],
                    httponly=True, secure=True, samesite='Strict',
                    expires=session['expire'], path='/')
    return resp
```

> **Cookie security:** Always use `httponly`, `secure`, and `samesite='Strict'` to prevent XSS. The cookie name must be `a_session_<PROJECT_ID>`.

> **Forwarding user agent:** Call `session_client.set_forwarded_user_agent(request.headers.get('user-agent'))` to record the end-user's browser info for debugging and security.

## Permissions & Roles (Critical)

Appwrite uses permission strings to control access to resources. Each permission pairs an action (`read`, `update`, `delete`, `create`, or `write` which grants create + update + delete) with a role target. By default, **no user has access** unless permissions are explicitly set at the document/file level or inherited from the collection/bucket settings. Permissions are arrays of strings built with the `Permission` and `Role` helpers.

```python
from appwrite.permission import Permission
from appwrite.role import Role
```

### Database Row with Permissions

```python
doc = tables_db.create_row('[DATABASE_ID]', '[TABLE_ID]', ID.unique(), {
    'title': 'Hello World'
}, [
    Permission.read(Role.user('[USER_ID]')),     # specific user can read
    Permission.update(Role.user('[USER_ID]')),   # specific user can update
    Permission.read(Role.team('[TEAM_ID]')),     # all team members can read
    Permission.read(Role.any()),                 # anyone (including guests) can read
])
```

### File Upload with Permissions

```python
file = storage.create_file('[BUCKET_ID]', ID.unique(), InputFile.from_path('/path/to/file.png'), [
    Permission.read(Role.any()),
    Permission.update(Role.user('[USER_ID]')),
    Permission.delete(Role.user('[USER_ID]')),
])
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
