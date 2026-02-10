# Users

The Users service allows you to manage your project users.

## List users

`list`
Get a list of all the project&#039;s users. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: name, email, phone, status, passwordUpdate, registration, emailVerification, phoneVerification, labels (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `userList`

## Create user

`create`
Create a new user.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `email` | string | No | User email. |
| `phone` | string | No | Phone number. Format this number with a leading &#039;+&#039; and a country code, e.g., +16175551212. |
| `password` | string | No | Plain text user password. Must be at least 8 chars. |
| `name` | string | No | User name. Max length: 128 chars. |

**Response:** `user`

## Create user with Argon2 password

`createArgon2User`
Create a new user. Password provided must be hashed with the [Argon2](https://en.wikipedia.org/wiki/Argon2) algorithm. Use the [POST /users](https://appwrite.io/docs/server/users#usersCreate) endpoint to create users with a plain text password.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `email` | string | Yes | User email. |
| `password` | string | Yes | User password hashed using Argon2. |
| `name` | string | No | User name. Max length: 128 chars. |

**Response:** `user`

## Create user with bcrypt password

`createBcryptUser`
Create a new user. Password provided must be hashed with the [Bcrypt](https://en.wikipedia.org/wiki/Bcrypt) algorithm. Use the [POST /users](https://appwrite.io/docs/server/users#usersCreate) endpoint to create users with a plain text password.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `email` | string | Yes | User email. |
| `password` | string | Yes | User password hashed using Bcrypt. |
| `name` | string | No | User name. Max length: 128 chars. |

**Response:** `user`

## List identities

`listIdentities`
Get identities for all users.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: userId, provider, providerUid, providerEmail, providerAccessTokenExpiry (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `identityList`

## Delete identity

`deleteIdentity`
Delete an identity by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `identityId` | string | Yes | Identity ID. |


## Create user with MD5 password

`createMD5User`
Create a new user. Password provided must be hashed with the [MD5](https://en.wikipedia.org/wiki/MD5) algorithm. Use the [POST /users](https://appwrite.io/docs/server/users#usersCreate) endpoint to create users with a plain text password.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `email` | string | Yes | User email. |
| `password` | string | Yes | User password hashed using MD5. |
| `name` | string | No | User name. Max length: 128 chars. |

**Response:** `user`

## Create user with PHPass password

`createPHPassUser`
Create a new user. Password provided must be hashed with the [PHPass](https://www.openwall.com/phpass/) algorithm. Use the [POST /users](https://appwrite.io/docs/server/users#usersCreate) endpoint to create users with a plain text password.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or pass the string `ID.unique()`to auto generate it. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `email` | string | Yes | User email. |
| `password` | string | Yes | User password hashed using PHPass. |
| `name` | string | No | User name. Max length: 128 chars. |

**Response:** `user`

## Create user with Scrypt password

`createScryptUser`
Create a new user. Password provided must be hashed with the [Scrypt](https://github.com/Tarsnap/scrypt) algorithm. Use the [POST /users](https://appwrite.io/docs/server/users#usersCreate) endpoint to create users with a plain text password.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `email` | string | Yes | User email. |
| `password` | string | Yes | User password hashed using Scrypt. |
| `passwordSalt` | string | Yes | Optional salt used to hash password. |
| `passwordCpu` | integer | Yes | Optional CPU cost used to hash password. |
| `passwordMemory` | integer | Yes | Optional memory cost used to hash password. |
| `passwordParallel` | integer | Yes | Optional parallelization cost used to hash password. |
| `passwordLength` | integer | Yes | Optional hash length used to hash password. |
| `name` | string | No | User name. Max length: 128 chars. |

**Response:** `user`

## Create user with Scrypt modified password

`createScryptModifiedUser`
Create a new user. Password provided must be hashed with the [Scrypt Modified](https://gist.github.com/Meldiron/eecf84a0225eccb5a378d45bb27462cc) algorithm. Use the [POST /users](https://appwrite.io/docs/server/users#usersCreate) endpoint to create users with a plain text password.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `email` | string | Yes | User email. |
| `password` | string | Yes | User password hashed using Scrypt Modified. |
| `passwordSalt` | string | Yes | Salt used to hash password. |
| `passwordSaltSeparator` | string | Yes | Salt separator used to hash password. |
| `passwordSignerKey` | string | Yes | Signer key used to hash password. |
| `name` | string | No | User name. Max length: 128 chars. |

**Response:** `user`

## Create user with SHA password

`createSHAUser`
Create a new user. Password provided must be hashed with the [SHA](https://en.wikipedia.org/wiki/Secure_Hash_Algorithm) algorithm. Use the [POST /users](https://appwrite.io/docs/server/users#usersCreate) endpoint to create users with a plain text password.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `email` | string | Yes | User email. |
| `password` | string | Yes | User password hashed using SHA. |
| `passwordVersion` | string | No | Optional SHA version used to hash password. Allowed values are: &#039;sha1&#039;, &#039;sha224&#039;, &#039;sha256&#039;, &#039;sha384&#039;, &#039;sha512/224&#039;, &#039;sha512/256&#039;, &#039;sha512&#039;, &#039;sha3-224&#039;, &#039;sha3-256&#039;, &#039;sha3-384&#039;, &#039;sha3-512&#039; |
| `name` | string | No | User name. Max length: 128 chars. |

**Response:** `user`

## Get users usage stats

`getUsage`
Get usage metrics and statistics for all users in the project. You can view the total number of users and sessions. The response includes both current totals and historical data over time. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, range defaults to 30 days.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageUsers`

## Get user

`get`
Get a user by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |

**Response:** `user`

## Delete user

`delete`
Delete a user by its unique ID, thereby releasing it&#039;s ID. Since ID is released and can be reused, all user-related resources like documents or storage files should be deleted before user deletion. If you want to keep ID reserved, use the [updateStatus](https://appwrite.io/docs/server/users#usersUpdateStatus) endpoint instead.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |


## Update email

`updateEmail`
Update the user email by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `email` | string | Yes | User email. |

**Response:** `user`

## Create user JWT

`createJWT`
Use this endpoint to create a JSON Web Token for user by its unique ID. You can use the resulting JWT to authenticate on behalf of the user. The JWT secret will become invalid if the session it uses gets deleted.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `sessionId` | string | No | Session ID. Use the string &#039;recent&#039; to use the most recent session. Defaults to the most recent session. |
| `duration` | integer | No | Time in seconds before JWT expires. Default duration is 900 seconds, and maximum is 3600 seconds. (default: `900`) |

**Response:** `jwt`

## Update user labels

`updateLabels`
Update the user labels by its unique ID. 

Labels can be used to grant access to resources. While teams are a way for user&#039;s to share access to a resource, labels can be defined by the developer to grant access without an invitation. See the [Permissions docs](https://appwrite.io/docs/permissions) for more info.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `labels` | array\<string\> | Yes | Array of user labels. Replaces the previous labels. Maximum of 1000 labels are allowed, each up to 36 alphanumeric characters long. |

**Response:** `user`

## List user logs

`listLogs`
Get the user activity logs list by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `logList`

## List user memberships

`listMemberships`
Get the user membership list by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: userId, teamId, invited, joined, confirm, roles (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `membershipList`

## updateMfa

`updateMfa` **(DEPRECATED — use `users.updateMFA` instead)**
Enable or disable MFA on a user account.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `mfa` | boolean | Yes | Enable or disable MFA. |

**Response:** `user`

## updateMFA

`updateMFA`
Enable or disable MFA on a user account.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `mfa` | boolean | Yes | Enable or disable MFA. |

**Response:** `user`

## deleteMfaAuthenticator

`deleteMfaAuthenticator` **(DEPRECATED — use `users.deleteMFAAuthenticator` instead)**
Delete an authenticator app.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `type` | string | Yes | Type of authenticator. |


## deleteMFAAuthenticator

`deleteMFAAuthenticator`
Delete an authenticator app.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `type` | string | Yes | Type of authenticator. |


## listMfaFactors

`listMfaFactors` **(DEPRECATED — use `users.listMFAFactors` instead)**
List the factors available on the account to be used as a MFA challange.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |

**Response:** `mfaFactors`

## listMFAFactors

`listMFAFactors`
List the factors available on the account to be used as a MFA challange.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |

**Response:** `mfaFactors`

## getMfaRecoveryCodes

`getMfaRecoveryCodes` **(DEPRECATED — use `users.getMFARecoveryCodes` instead)**
Get recovery codes that can be used as backup for MFA flow by User ID. Before getting codes, they must be generated using [createMfaRecoveryCodes](/docs/references/cloud/client-web/account#createMfaRecoveryCodes) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |

**Response:** `mfaRecoveryCodes`

## getMFARecoveryCodes

`getMFARecoveryCodes`
Get recovery codes that can be used as backup for MFA flow by User ID. Before getting codes, they must be generated using [createMfaRecoveryCodes](/docs/references/cloud/client-web/account#createMfaRecoveryCodes) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |

**Response:** `mfaRecoveryCodes`

## updateMfaRecoveryCodes

`updateMfaRecoveryCodes` **(DEPRECATED — use `users.updateMFARecoveryCodes` instead)**
Regenerate recovery codes that can be used as backup for MFA flow by User ID. Before regenerating codes, they must be first generated using [createMfaRecoveryCodes](/docs/references/cloud/client-web/account#createMfaRecoveryCodes) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |

**Response:** `mfaRecoveryCodes`

## updateMFARecoveryCodes

`updateMFARecoveryCodes`
Regenerate recovery codes that can be used as backup for MFA flow by User ID. Before regenerating codes, they must be first generated using [createMfaRecoveryCodes](/docs/references/cloud/client-web/account#createMfaRecoveryCodes) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |

**Response:** `mfaRecoveryCodes`

## createMfaRecoveryCodes

`createMfaRecoveryCodes` **(DEPRECATED — use `users.createMFARecoveryCodes` instead)**
Generate recovery codes used as backup for MFA flow for User ID. Recovery codes can be used as a MFA verification type in [createMfaChallenge](/docs/references/cloud/client-web/account#createMfaChallenge) method by client SDK.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |

**Response:** `mfaRecoveryCodes`

## createMFARecoveryCodes

`createMFARecoveryCodes`
Generate recovery codes used as backup for MFA flow for User ID. Recovery codes can be used as a MFA verification type in [createMfaChallenge](/docs/references/cloud/client-web/account#createMfaChallenge) method by client SDK.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |

**Response:** `mfaRecoveryCodes`

## Update name

`updateName`
Update the user name by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `name` | string | Yes | User name. Max length: 128 chars. |

**Response:** `user`

## Update password

`updatePassword`
Update the user password by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `password` | string | Yes | New user password. Must be at least 8 chars. |

**Response:** `user`

## Update phone

`updatePhone`
Update the user phone by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `number` | string | Yes | User phone number. |

**Response:** `user`

## Get user preferences

`getPrefs`
Get the user preferences by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |

**Response:** `preferences`

## Update user preferences

`updatePrefs`
Update the user preferences by its unique ID. The object you pass is stored as is, and replaces any previous value. The maximum allowed prefs size is 64kB and throws error if exceeded.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `prefs` | object | Yes | Prefs key-value JSON object. (default: `{}`) |

**Response:** `preferences`

## List user sessions

`listSessions`
Get the user sessions list by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `sessionList`

## Create session

`createSession`
Creates a session for a user. Returns an immediately usable session object.

If you want to generate a token for a custom authentication flow, use the [POST /users/{userId}/tokens](https://appwrite.io/docs/server/users#createToken) endpoint.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |

**Response:** `session`

## Delete user sessions

`deleteSessions`
Delete all user&#039;s sessions by using the user&#039;s unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |


## Delete user session

`deleteSession`
Delete a user sessions by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `sessionId` | string | Yes | Session ID. |


## Update user status

`updateStatus`
Update the user status by its unique ID. Use this endpoint as an alternative to deleting a user if you want to keep user&#039;s ID reserved.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `status` | boolean | Yes | User Status. To activate the user pass `true` and to block the user pass `false`. |

**Response:** `user`

## List user targets

`listTargets`
List the messaging targets that are associated with a user.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: userId, providerId, identifier, providerType (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `targetList`

## Create user target

`createTarget`
Create a messaging target.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `targetId` | string | Yes | Target ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `providerType` | string | Yes | The target provider type. Can be one of the following: `email`, `sms` or `push`. |
| `identifier` | string | Yes | The target identifier (token, email, phone etc.) |
| `providerId` | string | No | Provider ID. Message will be sent to this target from the specified provider ID. If no provider ID is set the first setup provider will be used. |
| `name` | string | No | Target name. Max length: 128 chars. For example: My Awesome App Galaxy S23. |

**Response:** `target`

## Get user target

`getTarget`
Get a user&#039;s push notification target by ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `targetId` | string | Yes | Target ID. |

**Response:** `target`

## Update user target

`updateTarget`
Update a messaging target.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `targetId` | string | Yes | Target ID. |
| `identifier` | string | No | The target identifier (token, email, phone etc.) |
| `providerId` | string | No | Provider ID. Message will be sent to this target from the specified provider ID. If no provider ID is set the first setup provider will be used. |
| `name` | string | No | Target name. Max length: 128 chars. For example: My Awesome App Galaxy S23. |

**Response:** `target`

## Delete user target

`deleteTarget`
Delete a messaging target.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `targetId` | string | Yes | Target ID. |


## Create token

`createToken`
Returns a token with a secret key for creating a session. Use the user ID and secret and submit a request to the [PUT /account/sessions/token](https://appwrite.io/docs/references/cloud/client-web/account#createSession) endpoint to complete the login process.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `length` | integer | No | Token length in characters. The default length is 6 characters (default: `6`) |
| `expire` | integer | No | Token expiration period in seconds. The default expiration is 15 minutes. (default: `900`) |

**Response:** `token`

## Update email verification

`updateEmailVerification`
Update the user email verification status by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `emailVerification` | boolean | Yes | User email verification status. |

**Response:** `user`

## Update phone verification

`updatePhoneVerification`
Update the user phone verification status by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `phoneVerification` | boolean | Yes | User phone verification status. |

**Response:** `user`

