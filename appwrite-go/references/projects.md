# Projects

The Project service allows you to manage all the projects in your Appwrite server.

## List projects

`list`
Get a list of all projects. You can use the query params to filter your results. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: name, teamId, labels, search (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `projectList`

## Create project

`create`
Create a new project. You can create a maximum of 100 projects per account. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Unique Id. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, and hyphen. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Project name. Max length: 128 chars. |
| `teamId` | string | Yes | Team unique ID. |
| `region` | string | No | Project Region. (default: `default`) |
| `description` | string | No | Project description. Max length: 256 chars. |
| `logo` | string | No | Project logo. |
| `url` | string | No | Project URL. |
| `legalName` | string | No | Project legal Name. Max length: 256 chars. |
| `legalCountry` | string | No | Project legal Country. Max length: 256 chars. |
| `legalState` | string | No | Project legal State. Max length: 256 chars. |
| `legalCity` | string | No | Project legal City. Max length: 256 chars. |
| `legalAddress` | string | No | Project legal Address. Max length: 256 chars. |
| `legalTaxId` | string | No | Project legal Tax ID. Max length: 256 chars. |

**Response:** `project`

## Get project

`get`
Get a project by its unique ID. This endpoint allows you to retrieve the project&#039;s details, including its name, description, team, region, and other metadata. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |

**Response:** `project`

## Update project

`update`
Update a project by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `name` | string | Yes | Project name. Max length: 128 chars. |
| `description` | string | No | Project description. Max length: 256 chars. |
| `logo` | string | No | Project logo. |
| `url` | string | No | Project URL. |
| `legalName` | string | No | Project legal name. Max length: 256 chars. |
| `legalCountry` | string | No | Project legal country. Max length: 256 chars. |
| `legalState` | string | No | Project legal state. Max length: 256 chars. |
| `legalCity` | string | No | Project legal city. Max length: 256 chars. |
| `legalAddress` | string | No | Project legal address. Max length: 256 chars. |
| `legalTaxId` | string | No | Project legal tax ID. Max length: 256 chars. |

**Response:** `project`

## Delete project

`delete`
Delete a project by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |


## updateApiStatus

`updateApiStatus` **(DEPRECATED — use `projects.updateAPIStatus` instead)**
Update the status of a specific API type. Use this endpoint to enable or disable API types such as REST, GraphQL and Realtime.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `api` | string | Yes | API name. |
| `status` | boolean | Yes | API status. |

**Response:** `project`

## updateAPIStatus

`updateAPIStatus`
Update the status of a specific API type. Use this endpoint to enable or disable API types such as REST, GraphQL and Realtime.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `api` | string | Yes | API name. |
| `status` | boolean | Yes | API status. |

**Response:** `project`

## updateApiStatusAll

`updateApiStatusAll` **(DEPRECATED — use `projects.updateAPIStatusAll` instead)**
Update the status of all API types. Use this endpoint to enable or disable API types such as REST, GraphQL and Realtime all at once.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `status` | boolean | Yes | API status. |

**Response:** `project`

## updateAPIStatusAll

`updateAPIStatusAll`
Update the status of all API types. Use this endpoint to enable or disable API types such as REST, GraphQL and Realtime all at once.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `status` | boolean | Yes | API status. |

**Response:** `project`

## Update project authentication duration

`updateAuthDuration`
Update how long sessions created within a project should stay active for.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `duration` | integer | Yes | Project session length in seconds. Max length: 31536000 seconds. |

**Response:** `project`

## Update project users limit

`updateAuthLimit`
Update the maximum number of users allowed in this project. Set to 0 for unlimited users. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `limit` | integer | Yes | Set the max number of users allowed in this project. Use 0 for unlimited. |

**Response:** `project`

## Update project user sessions limit

`updateAuthSessionsLimit`
Update the maximum number of sessions allowed per user within the project, if the limit is hit the oldest session will be deleted to make room for new sessions.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `limit` | integer | Yes | Set the max number of users allowed in this project. Value allowed is between 1-100. Default is 10 |

**Response:** `project`

## Update project memberships privacy attributes

`updateMembershipsPrivacy`
Update project membership privacy settings. Use this endpoint to control what user information is visible to other team members, such as user name, email, and MFA status. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `userName` | boolean | Yes | Set to true to show userName to members of a team. |
| `userEmail` | boolean | Yes | Set to true to show email to members of a team. |
| `mfa` | boolean | Yes | Set to true to show mfa to members of a team. |

**Response:** `project`

## Update the mock numbers for the project

`updateMockNumbers`
Update the list of mock phone numbers for testing. Use these numbers to bypass SMS verification in development. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `numbers` | array\<object\> | Yes | An array of mock numbers and their corresponding verification codes (OTPs). Each number should be a valid E.164 formatted phone number. Maximum of 10 numbers are allowed. |

**Response:** `project`

## Update authentication password dictionary status. Use this endpoint to enable or disable the dicitonary check for user password

`updateAuthPasswordDictionary`
Enable or disable checking user passwords against common passwords dictionary. This helps ensure users don&#039;t use common and insecure passwords. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `enabled` | boolean | Yes | Set whether or not to enable checking user&#039;s password against most commonly used passwords. Default is false. |

**Response:** `project`

## Update authentication password history. Use this endpoint to set the number of password history to save and 0 to disable password history.

`updateAuthPasswordHistory`
Update the authentication password history requirement. Use this endpoint to require new passwords to be different than the last X amount of previously used ones.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `limit` | integer | Yes | Set the max number of passwords to store in user history. User can&#039;t choose a new password that is already stored in the password history list.  Max number of passwords allowed in history is20. Default value is 0 |

**Response:** `project`

## Update personal data check

`updatePersonalDataCheck`
Enable or disable checking user passwords against their personal data. This helps prevent users from using personal information in their passwords. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `enabled` | boolean | Yes | Set whether or not to check a password for similarity with personal data. Default is false. |

**Response:** `project`

## Update project sessions emails

`updateSessionAlerts`
Enable or disable session email alerts. When enabled, users will receive email notifications when new sessions are created.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `alerts` | boolean | Yes | Set to true to enable session emails. |

**Response:** `project`

## Update invalidate session option of the project

`updateSessionInvalidation`
Invalidate all existing sessions. An optional auth security setting for projects, and enabled by default for console project.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `enabled` | boolean | Yes | Update authentication session invalidation status. Use this endpoint to enable or disable session invalidation on password change |

**Response:** `project`

## Update project auth method status. Use this endpoint to enable or disable a given auth method for this project.

`updateAuthStatus`
Update the status of a specific authentication method. Use this endpoint to enable or disable different authentication methods such as email, magic urls or sms in your project. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `method` | string | Yes | Auth Method. Possible values: email-password,magic-url,email-otp,anonymous,invites,jwt,phone |
| `status` | boolean | Yes | Set the status of this auth method. |

**Response:** `project`

## List dev keys

`listDevKeys`
List all the project\&#039;s dev keys. Dev keys are project specific and allow you to bypass rate limits and get better error logging during development.&#039;

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: accessedAt, expire (default: `[]`) |

**Response:** `devKeyList`

## Create dev key

`createDevKey`
Create a new project dev key. Dev keys are project specific and allow you to bypass rate limits and get better error logging during development. Strictly meant for development purposes only.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `name` | string | Yes | Key name. Max length: 128 chars. |
| `expire` | string | Yes | Expiration time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. |

**Response:** `devKey`

## Get dev key

`getDevKey`
Get a project\&#039;s dev key by its unique ID. Dev keys are project specific and allow you to bypass rate limits and get better error logging during development.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `keyId` | string | Yes | Key unique ID. |

**Response:** `devKey`

## Update dev key

`updateDevKey`
Update a project\&#039;s dev key by its unique ID. Use this endpoint to update a project\&#039;s dev key name or expiration time.&#039;

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `keyId` | string | Yes | Key unique ID. |
| `name` | string | Yes | Key name. Max length: 128 chars. |
| `expire` | string | Yes | Expiration time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. |

**Response:** `devKey`

## Delete dev key

`deleteDevKey`
Delete a project\&#039;s dev key by its unique ID. Once deleted, the key will no longer allow bypassing of rate limits and better logging of errors.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `keyId` | string | Yes | Key unique ID. |


## Create JWT

`createJWT`
Create a new JWT token. This token can be used to authenticate users with custom scopes and expiration time. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `scopes` | array\<string\> | Yes | List of scopes allowed for JWT key. Maximum of 100 scopes are allowed. |
| `duration` | integer | No | Time in seconds before JWT expires. Default duration is 900 seconds, and maximum is 3600 seconds. (default: `900`) |

**Response:** `jwt`

## List keys

`listKeys`
Get a list of all API keys from the current project. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `keyList`

## Create key

`createKey`
Create a new API key. It&#039;s recommended to have multiple API keys with strict scopes for separate functions within your project.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `name` | string | Yes | Key name. Max length: 128 chars. |
| `scopes` | array\<string\> | Yes | Key scopes list. Maximum of 100 scopes are allowed. |
| `expire` | string | No | Expiration time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. Use null for unlimited expiration. |

**Response:** `key`

## Get key

`getKey`
Get a key by its unique ID. This endpoint returns details about a specific API key in your project including it&#039;s scopes.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `keyId` | string | Yes | Key unique ID. |

**Response:** `key`

## Update key

`updateKey`
Update a key by its unique ID. Use this endpoint to update the name, scopes, or expiration time of an API key. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `keyId` | string | Yes | Key unique ID. |
| `name` | string | Yes | Key name. Max length: 128 chars. |
| `scopes` | array\<string\> | Yes | Key scopes list. Maximum of 100 events are allowed. |
| `expire` | string | No | Expiration time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. Use null for unlimited expiration. |

**Response:** `key`

## Delete key

`deleteKey`
Delete a key by its unique ID. Once deleted, the key can no longer be used to authenticate API calls. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `keyId` | string | Yes | Key unique ID. |


## Update project labels

`updateLabels`
Update the project labels by its unique ID. Labels can be used to easily filter projects in an organization.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `labels` | array\<string\> | Yes | Array of project labels. Replaces the previous labels. Maximum of 1000 labels are allowed, each up to 36 alphanumeric characters long. |

**Response:** `project`

## Update project OAuth2

`updateOAuth2`
Update the OAuth2 provider configurations. Use this endpoint to set up or update the OAuth2 provider credentials or enable/disable providers. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `provider` | string | Yes | Provider Name |
| `appId` | string | No | Provider app ID. Max length: 256 chars. |
| `secret` | string | No | Provider secret key. Max length: 512 chars. |
| `enabled` | boolean | No | Provider status. Set to &#039;false&#039; to disable new session creation. |

**Response:** `project`

## List platforms

`listPlatforms`
Get a list of all platforms in the project. This endpoint returns an array of all platforms and their configurations. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `platformList`

## Create platform

`createPlatform`
Create a new platform for your project. Use this endpoint to register a new platform where your users will run your application which will interact with the Appwrite API.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `type` | string | Yes | Platform type. Possible values are: web, flutter-web, flutter-ios, flutter-android, flutter-linux, flutter-macos, flutter-windows, apple-ios, apple-macos, apple-watchos, apple-tvos, android, unity, react-native-ios, react-native-android. |
| `name` | string | Yes | Platform name. Max length: 128 chars. |
| `key` | string | No | Package name for Android or bundle ID for iOS or macOS. Max length: 256 chars. |
| `store` | string | No | App store or Google Play store ID. Max length: 256 chars. |
| `hostname` | string | No | Platform client hostname. Max length: 256 chars. |

**Response:** `platform`

## Get platform

`getPlatform`
Get a platform by its unique ID. This endpoint returns the platform&#039;s details, including its name, type, and key configurations. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `platformId` | string | Yes | Platform unique ID. |

**Response:** `platform`

## Update platform

`updatePlatform`
Update a platform by its unique ID. Use this endpoint to update the platform&#039;s name, key, platform store ID, or hostname. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `platformId` | string | Yes | Platform unique ID. |
| `name` | string | Yes | Platform name. Max length: 128 chars. |
| `key` | string | No | Package name for android or bundle ID for iOS. Max length: 256 chars. |
| `store` | string | No | App store or Google Play store ID. Max length: 256 chars. |
| `hostname` | string | No | Platform client URL. Max length: 256 chars. |

**Response:** `platform`

## Delete platform

`deletePlatform`
Delete a platform by its unique ID. This endpoint removes the platform and all its configurations from the project. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `platformId` | string | Yes | Platform unique ID. |


## Update service status

`updateServiceStatus`
Update the status of a specific service. Use this endpoint to enable or disable a service in your project. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `service` | string | Yes | Service name. |
| `status` | boolean | Yes | Service status. |

**Response:** `project`

## Update all service status

`updateServiceStatusAll`
Update the status of all services. Use this endpoint to enable or disable all optional services at once. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `status` | boolean | Yes | Service status. |

**Response:** `project`

## updateSmtp

`updateSmtp` **(DEPRECATED — use `projects.updateSMTP` instead)**
Update the SMTP configuration for your project. Use this endpoint to configure your project&#039;s SMTP provider with your custom settings for sending transactional emails. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `enabled` | boolean | Yes | Enable custom SMTP service |
| `senderName` | string | No | Name of the email sender |
| `senderEmail` | string | No | Email of the sender |
| `replyTo` | string | No | Reply to email |
| `host` | string | No | SMTP server host name |
| `port` | integer | No | SMTP server port (default: `587`) |
| `username` | string | No | SMTP server username |
| `password` | string | No | SMTP server password |
| `secure` | string | No | Does SMTP server use secure connection |

**Response:** `project`

## updateSMTP

`updateSMTP`
Update the SMTP configuration for your project. Use this endpoint to configure your project&#039;s SMTP provider with your custom settings for sending transactional emails. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `enabled` | boolean | Yes | Enable custom SMTP service |
| `senderName` | string | No | Name of the email sender |
| `senderEmail` | string | No | Email of the sender |
| `replyTo` | string | No | Reply to email |
| `host` | string | No | SMTP server host name |
| `port` | integer | No | SMTP server port (default: `587`) |
| `username` | string | No | SMTP server username |
| `password` | string | No | SMTP server password |
| `secure` | string | No | Does SMTP server use secure connection |

**Response:** `project`

## createSmtpTest

`createSmtpTest` **(DEPRECATED — use `projects.createSMTPTest` instead)**
Send a test email to verify SMTP configuration. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `emails` | array\<string\> | Yes | Array of emails to send test email to. Maximum of 10 emails are allowed. |
| `senderName` | string | Yes | Name of the email sender |
| `senderEmail` | string | Yes | Email of the sender |
| `host` | string | Yes | SMTP server host name |
| `replyTo` | string | No | Reply to email |
| `port` | integer | No | SMTP server port (default: `587`) |
| `username` | string | No | SMTP server username |
| `password` | string | No | SMTP server password |
| `secure` | string | No | Does SMTP server use secure connection |


## createSMTPTest

`createSMTPTest`
Send a test email to verify SMTP configuration. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `emails` | array\<string\> | Yes | Array of emails to send test email to. Maximum of 10 emails are allowed. |
| `senderName` | string | Yes | Name of the email sender |
| `senderEmail` | string | Yes | Email of the sender |
| `host` | string | Yes | SMTP server host name |
| `replyTo` | string | No | Reply to email |
| `port` | integer | No | SMTP server port (default: `587`) |
| `username` | string | No | SMTP server username |
| `password` | string | No | SMTP server password |
| `secure` | string | No | Does SMTP server use secure connection |


## Update project team

`updateTeam`
Update the team ID of a project allowing for it to be transferred to another team.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `teamId` | string | Yes | Team ID of the team to transfer project to. |

**Response:** `project`

## Get custom email template

`getEmailTemplate`
Get a custom email template for the specified locale and type. This endpoint returns the template content, subject, and other configuration details. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `type` | string | Yes | Template type |
| `locale` | string | Yes | Template locale |

**Response:** `emailTemplate`

## Update custom email templates

`updateEmailTemplate`
Update a custom email template for the specified locale and type. Use this endpoint to modify the content of your email templates.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `type` | string | Yes | Template type |
| `locale` | string | Yes | Template locale |
| `subject` | string | Yes | Email Subject |
| `message` | string | Yes | Template message |
| `senderName` | string | No | Name of the email sender |
| `senderEmail` | string | No | Email of the sender |
| `replyTo` | string | No | Reply to email |

**Response:** `emailTemplate`

## Delete custom email template

`deleteEmailTemplate`
Reset a custom email template to its default value. This endpoint removes any custom content and restores the template to its original state. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `type` | string | Yes | Template type |
| `locale` | string | Yes | Template locale |

**Response:** `emailTemplate`

## getSmsTemplate

`getSmsTemplate` **(DEPRECATED — use `projects.getSMSTemplate` instead)**
Get a custom SMS template for the specified locale and type returning it&#039;s contents.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `type` | string | Yes | Template type |
| `locale` | string | Yes | Template locale |

**Response:** `smsTemplate`

## getSMSTemplate

`getSMSTemplate`
Get a custom SMS template for the specified locale and type returning it&#039;s contents.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `type` | string | Yes | Template type |
| `locale` | string | Yes | Template locale |

**Response:** `smsTemplate`

## updateSmsTemplate

`updateSmsTemplate` **(DEPRECATED — use `projects.updateSMSTemplate` instead)**
Update a custom SMS template for the specified locale and type. Use this endpoint to modify the content of your SMS templates. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `type` | string | Yes | Template type |
| `locale` | string | Yes | Template locale |
| `message` | string | Yes | Template message |

**Response:** `smsTemplate`

## updateSMSTemplate

`updateSMSTemplate`
Update a custom SMS template for the specified locale and type. Use this endpoint to modify the content of your SMS templates. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `type` | string | Yes | Template type |
| `locale` | string | Yes | Template locale |
| `message` | string | Yes | Template message |

**Response:** `smsTemplate`

## deleteSmsTemplate

`deleteSmsTemplate` **(DEPRECATED — use `projects.deleteSMSTemplate` instead)**
Reset a custom SMS template to its default value. This endpoint removes any custom message and restores the template to its original state. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `type` | string | Yes | Template type |
| `locale` | string | Yes | Template locale |

**Response:** `smsTemplate`

## deleteSMSTemplate

`deleteSMSTemplate`
Reset a custom SMS template to its default value. This endpoint removes any custom message and restores the template to its original state. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `type` | string | Yes | Template type |
| `locale` | string | Yes | Template locale |

**Response:** `smsTemplate`

## List webhooks

`listWebhooks`
Get a list of all webhooks belonging to the project. You can use the query params to filter your results. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `webhookList`

## Create webhook

`createWebhook`
Create a new webhook. Use this endpoint to configure a URL that will receive events from Appwrite when specific events occur. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `name` | string | Yes | Webhook name. Max length: 128 chars. |
| `events` | array\<string\> | Yes | Events list. Maximum of 100 events are allowed. |
| `url` | string | Yes | Webhook URL. |
| `security` | boolean | Yes | Certificate verification, false for disabled or true for enabled. |
| `enabled` | boolean | No | Enable or disable a webhook. (default: `1`) |
| `httpUser` | string | No | Webhook HTTP user. Max length: 256 chars. |
| `httpPass` | string | No | Webhook HTTP password. Max length: 256 chars. |

**Response:** `webhook`

## Get webhook

`getWebhook`
Get a webhook by its unique ID. This endpoint returns details about a specific webhook configured for a project. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `webhookId` | string | Yes | Webhook unique ID. |

**Response:** `webhook`

## Update webhook

`updateWebhook`
Update a webhook by its unique ID. Use this endpoint to update the URL, events, or status of an existing webhook. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `webhookId` | string | Yes | Webhook unique ID. |
| `name` | string | Yes | Webhook name. Max length: 128 chars. |
| `events` | array\<string\> | Yes | Events list. Maximum of 100 events are allowed. |
| `url` | string | Yes | Webhook URL. |
| `security` | boolean | Yes | Certificate verification, false for disabled or true for enabled. |
| `enabled` | boolean | No | Enable or disable a webhook. (default: `1`) |
| `httpUser` | string | No | Webhook HTTP user. Max length: 256 chars. |
| `httpPass` | string | No | Webhook HTTP password. Max length: 256 chars. |

**Response:** `webhook`

## Delete webhook

`deleteWebhook`
Delete a webhook by its unique ID. Once deleted, the webhook will no longer receive project events. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `webhookId` | string | Yes | Webhook unique ID. |


## Update webhook signature key

`updateWebhookSignature`
Update the webhook signature key. This endpoint can be used to regenerate the signature key used to sign and validate payload deliveries for a specific webhook. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `projectId` | string | Yes | Project unique ID. |
| `webhookId` | string | Yes | Webhook unique ID. |

**Response:** `webhook`

