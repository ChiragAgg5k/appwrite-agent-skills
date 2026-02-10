# Messaging

The Messaging service allows you to send messages to any provider type (SMTP, push notification, SMS, etc.).

## List messages

`listMessages`
Get a list of all messages from the current Appwrite project.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: scheduledAt, deliveredAt, deliveredTotal, status, description, providerType (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `messageList`

## Create email

`createEmail`
Create a new email message.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `subject` | string | Yes | Email Subject. |
| `content` | string | Yes | Email Content. |
| `topics` | array\<string\> | No | List of Topic IDs. (default: `[]`) |
| `users` | array\<string\> | No | List of User IDs. (default: `[]`) |
| `targets` | array\<string\> | No | List of Targets IDs. (default: `[]`) |
| `cc` | array\<string\> | No | Array of target IDs to be added as CC. (default: `[]`) |
| `bcc` | array\<string\> | No | Array of target IDs to be added as BCC. (default: `[]`) |
| `attachments` | array\<string\> | No | Array of compound ID strings of bucket IDs and file IDs to be attached to the email. They should be formatted as &lt;BUCKET_ID&gt;:&lt;FILE_ID&gt;. (default: `[]`) |
| `draft` | boolean | No | Is message a draft |
| `html` | boolean | No | Is content of type HTML |
| `scheduledAt` | string | No | Scheduled delivery time for message in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. DateTime value must be in future. |

**Response:** `message`

## Update email

`updateEmail`
Update an email message by its unique ID. This endpoint only works on messages that are in draft status. Messages that are already processing, sent, or failed cannot be updated.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. |
| `topics` | array\<string\> | No | List of Topic IDs. |
| `users` | array\<string\> | No | List of User IDs. |
| `targets` | array\<string\> | No | List of Targets IDs. |
| `subject` | string | No | Email Subject. |
| `content` | string | No | Email Content. |
| `draft` | boolean | No | Is message a draft |
| `html` | boolean | No | Is content of type HTML |
| `cc` | array\<string\> | No | Array of target IDs to be added as CC. |
| `bcc` | array\<string\> | No | Array of target IDs to be added as BCC. |
| `scheduledAt` | string | No | Scheduled delivery time for message in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. DateTime value must be in future. |
| `attachments` | array\<string\> | No | Array of compound ID strings of bucket IDs and file IDs to be attached to the email. They should be formatted as &lt;BUCKET_ID&gt;:&lt;FILE_ID&gt;. |

**Response:** `message`

## Create push notification

`createPush`
Create a new push notification.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `title` | string | No | Title for push notification. |
| `body` | string | No | Body for push notification. |
| `topics` | array\<string\> | No | List of Topic IDs. (default: `[]`) |
| `users` | array\<string\> | No | List of User IDs. (default: `[]`) |
| `targets` | array\<string\> | No | List of Targets IDs. (default: `[]`) |
| `data` | object | No | Additional key-value pair data for push notification. (default: `{}`) |
| `action` | string | No | Action for push notification. |
| `image` | string | No | Image for push notification. Must be a compound bucket ID to file ID of a jpeg, png, or bmp image in Appwrite Storage. It should be formatted as &lt;BUCKET_ID&gt;:&lt;FILE_ID&gt;. |
| `icon` | string | No | Icon for push notification. Available only for Android and Web Platform. |
| `sound` | string | No | Sound for push notification. Available only for Android and iOS Platform. |
| `color` | string | No | Color for push notification. Available only for Android Platform. |
| `tag` | string | No | Tag for push notification. Available only for Android Platform. |
| `badge` | integer | No | Badge for push notification. Available only for iOS Platform. (default: `-1`) |
| `draft` | boolean | No | Is message a draft |
| `scheduledAt` | string | No | Scheduled delivery time for message in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. DateTime value must be in future. |
| `contentAvailable` | boolean | No | If set to true, the notification will be delivered in the background. Available only for iOS Platform. |
| `critical` | boolean | No | If set to true, the notification will be marked as critical. This requires the app to have the critical notification entitlement. Available only for iOS Platform. |
| `priority` | string | No | Set the notification priority. &quot;normal&quot; will consider device state and may not deliver notifications immediately. &quot;high&quot; will always attempt to immediately deliver the notification. (default: `high`) |

**Response:** `message`

## Update push notification

`updatePush`
Update a push notification by its unique ID. This endpoint only works on messages that are in draft status. Messages that are already processing, sent, or failed cannot be updated.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. |
| `topics` | array\<string\> | No | List of Topic IDs. |
| `users` | array\<string\> | No | List of User IDs. |
| `targets` | array\<string\> | No | List of Targets IDs. |
| `title` | string | No | Title for push notification. |
| `body` | string | No | Body for push notification. |
| `data` | object | No | Additional Data for push notification. (default: `{}`) |
| `action` | string | No | Action for push notification. |
| `image` | string | No | Image for push notification. Must be a compound bucket ID to file ID of a jpeg, png, or bmp image in Appwrite Storage. It should be formatted as &lt;BUCKET_ID&gt;:&lt;FILE_ID&gt;. |
| `icon` | string | No | Icon for push notification. Available only for Android and Web platforms. |
| `sound` | string | No | Sound for push notification. Available only for Android and iOS platforms. |
| `color` | string | No | Color for push notification. Available only for Android platforms. |
| `tag` | string | No | Tag for push notification. Available only for Android platforms. |
| `badge` | integer | No | Badge for push notification. Available only for iOS platforms. |
| `draft` | boolean | No | Is message a draft |
| `scheduledAt` | string | No | Scheduled delivery time for message in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. DateTime value must be in future. |
| `contentAvailable` | boolean | No | If set to true, the notification will be delivered in the background. Available only for iOS Platform. |
| `critical` | boolean | No | If set to true, the notification will be marked as critical. This requires the app to have the critical notification entitlement. Available only for iOS Platform. |
| `priority` | string | No | Set the notification priority. &quot;normal&quot; will consider device battery state and may send notifications later. &quot;high&quot; will always attempt to immediately deliver the notification. |

**Response:** `message`

## createSms

`createSms` **(DEPRECATED — use `messaging.createSMS` instead)**
Create a new SMS message.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `content` | string | Yes | SMS Content. |
| `topics` | array\<string\> | No | List of Topic IDs. (default: `[]`) |
| `users` | array\<string\> | No | List of User IDs. (default: `[]`) |
| `targets` | array\<string\> | No | List of Targets IDs. (default: `[]`) |
| `draft` | boolean | No | Is message a draft |
| `scheduledAt` | string | No | Scheduled delivery time for message in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. DateTime value must be in future. |

**Response:** `message`

## createSMS

`createSMS`
Create a new SMS message.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `content` | string | Yes | SMS Content. |
| `topics` | array\<string\> | No | List of Topic IDs. (default: `[]`) |
| `users` | array\<string\> | No | List of User IDs. (default: `[]`) |
| `targets` | array\<string\> | No | List of Targets IDs. (default: `[]`) |
| `draft` | boolean | No | Is message a draft |
| `scheduledAt` | string | No | Scheduled delivery time for message in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. DateTime value must be in future. |

**Response:** `message`

## updateSms

`updateSms` **(DEPRECATED — use `messaging.updateSMS` instead)**
Update an SMS message by its unique ID. This endpoint only works on messages that are in draft status. Messages that are already processing, sent, or failed cannot be updated.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. |
| `topics` | array\<string\> | No | List of Topic IDs. |
| `users` | array\<string\> | No | List of User IDs. |
| `targets` | array\<string\> | No | List of Targets IDs. |
| `content` | string | No | Email Content. |
| `draft` | boolean | No | Is message a draft |
| `scheduledAt` | string | No | Scheduled delivery time for message in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. DateTime value must be in future. |

**Response:** `message`

## updateSMS

`updateSMS`
Update an SMS message by its unique ID. This endpoint only works on messages that are in draft status. Messages that are already processing, sent, or failed cannot be updated.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. |
| `topics` | array\<string\> | No | List of Topic IDs. |
| `users` | array\<string\> | No | List of User IDs. |
| `targets` | array\<string\> | No | List of Targets IDs. |
| `content` | string | No | Email Content. |
| `draft` | boolean | No | Is message a draft |
| `scheduledAt` | string | No | Scheduled delivery time for message in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. DateTime value must be in future. |

**Response:** `message`

## Get message

`getMessage`
Get a message by its unique ID.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. |

**Response:** `message`

## Delete message

`delete`
Delete a message. If the message is not a draft or scheduled, but has been sent, this will not recall the message.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. |


## List message logs

`listMessageLogs`
Get the message activity logs listed by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `logList`

## List message targets

`listTargets`
Get a list of the targets associated with a message.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `messageId` | string | Yes | Message ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: userId, providerId, identifier, providerType (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `targetList`

## List providers

`listProviders`
Get a list of all providers from the current Appwrite project.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: name, provider, type, enabled (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `providerList`

## createApnsProvider

`createApnsProvider` **(DEPRECATED — use `messaging.createAPNSProvider` instead)**
Create a new Apple Push Notification service provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `authKey` | string | No | APNS authentication key. |
| `authKeyId` | string | No | APNS authentication key ID. |
| `teamId` | string | No | APNS team ID. |
| `bundleId` | string | No | APNS bundle ID. |
| `sandbox` | boolean | No | Use APNS sandbox environment. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## createAPNSProvider

`createAPNSProvider`
Create a new Apple Push Notification service provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `authKey` | string | No | APNS authentication key. |
| `authKeyId` | string | No | APNS authentication key ID. |
| `teamId` | string | No | APNS team ID. |
| `bundleId` | string | No | APNS bundle ID. |
| `sandbox` | boolean | No | Use APNS sandbox environment. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## updateApnsProvider

`updateApnsProvider` **(DEPRECATED — use `messaging.updateAPNSProvider` instead)**
Update a Apple Push Notification service provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `enabled` | boolean | No | Set as enabled. |
| `authKey` | string | No | APNS authentication key. |
| `authKeyId` | string | No | APNS authentication key ID. |
| `teamId` | string | No | APNS team ID. |
| `bundleId` | string | No | APNS bundle ID. |
| `sandbox` | boolean | No | Use APNS sandbox environment. |

**Response:** `provider`

## updateAPNSProvider

`updateAPNSProvider`
Update a Apple Push Notification service provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `enabled` | boolean | No | Set as enabled. |
| `authKey` | string | No | APNS authentication key. |
| `authKeyId` | string | No | APNS authentication key ID. |
| `teamId` | string | No | APNS team ID. |
| `bundleId` | string | No | APNS bundle ID. |
| `sandbox` | boolean | No | Use APNS sandbox environment. |

**Response:** `provider`

## createFcmProvider

`createFcmProvider` **(DEPRECATED — use `messaging.createFCMProvider` instead)**
Create a new Firebase Cloud Messaging provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `serviceAccountJSON` | object | No | FCM service account JSON. (default: `{}`) |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## createFCMProvider

`createFCMProvider`
Create a new Firebase Cloud Messaging provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `serviceAccountJSON` | object | No | FCM service account JSON. (default: `{}`) |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## updateFcmProvider

`updateFcmProvider` **(DEPRECATED — use `messaging.updateFCMProvider` instead)**
Update a Firebase Cloud Messaging provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `enabled` | boolean | No | Set as enabled. |
| `serviceAccountJSON` | object | No | FCM service account JSON. (default: `{}`) |

**Response:** `provider`

## updateFCMProvider

`updateFCMProvider`
Update a Firebase Cloud Messaging provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `enabled` | boolean | No | Set as enabled. |
| `serviceAccountJSON` | object | No | FCM service account JSON. (default: `{}`) |

**Response:** `provider`

## Create Mailgun provider

`createMailgunProvider`
Create a new Mailgun provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `apiKey` | string | No | Mailgun API Key. |
| `domain` | string | No | Mailgun Domain. |
| `isEuRegion` | boolean | No | Set as EU region. |
| `fromName` | string | No | Sender Name. |
| `fromEmail` | string | No | Sender email address. |
| `replyToName` | string | No | Name set in the reply to field for the mail. Default value is sender name. Reply to name must have reply to email as well. |
| `replyToEmail` | string | No | Email set in the reply to field for the mail. Default value is sender email. Reply to email must have reply to name as well. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## Update Mailgun provider

`updateMailgunProvider`
Update a Mailgun provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `apiKey` | string | No | Mailgun API Key. |
| `domain` | string | No | Mailgun Domain. |
| `isEuRegion` | boolean | No | Set as EU region. |
| `enabled` | boolean | No | Set as enabled. |
| `fromName` | string | No | Sender Name. |
| `fromEmail` | string | No | Sender email address. |
| `replyToName` | string | No | Name set in the reply to field for the mail. Default value is sender name. |
| `replyToEmail` | string | No | Email set in the reply to field for the mail. Default value is sender email. |

**Response:** `provider`

## Create Msg91 provider

`createMsg91Provider`
Create a new MSG91 provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `templateId` | string | No | Msg91 template ID |
| `senderId` | string | No | Msg91 sender ID. |
| `authKey` | string | No | Msg91 auth key. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## Update Msg91 provider

`updateMsg91Provider`
Update a MSG91 provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `enabled` | boolean | No | Set as enabled. |
| `templateId` | string | No | Msg91 template ID. |
| `senderId` | string | No | Msg91 sender ID. |
| `authKey` | string | No | Msg91 auth key. |

**Response:** `provider`

## Create Resend provider

`createResendProvider`
Create a new Resend provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `apiKey` | string | No | Resend API key. |
| `fromName` | string | No | Sender Name. |
| `fromEmail` | string | No | Sender email address. |
| `replyToName` | string | No | Name set in the reply to field for the mail. Default value is sender name. |
| `replyToEmail` | string | No | Email set in the reply to field for the mail. Default value is sender email. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## Update Resend provider

`updateResendProvider`
Update a Resend provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `enabled` | boolean | No | Set as enabled. |
| `apiKey` | string | No | Resend API key. |
| `fromName` | string | No | Sender Name. |
| `fromEmail` | string | No | Sender email address. |
| `replyToName` | string | No | Name set in the Reply To field for the mail. Default value is Sender Name. |
| `replyToEmail` | string | No | Email set in the Reply To field for the mail. Default value is Sender Email. |

**Response:** `provider`

## Create Sendgrid provider

`createSendgridProvider`
Create a new Sendgrid provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `apiKey` | string | No | Sendgrid API key. |
| `fromName` | string | No | Sender Name. |
| `fromEmail` | string | No | Sender email address. |
| `replyToName` | string | No | Name set in the reply to field for the mail. Default value is sender name. |
| `replyToEmail` | string | No | Email set in the reply to field for the mail. Default value is sender email. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## Update Sendgrid provider

`updateSendgridProvider`
Update a Sendgrid provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `enabled` | boolean | No | Set as enabled. |
| `apiKey` | string | No | Sendgrid API key. |
| `fromName` | string | No | Sender Name. |
| `fromEmail` | string | No | Sender email address. |
| `replyToName` | string | No | Name set in the Reply To field for the mail. Default value is Sender Name. |
| `replyToEmail` | string | No | Email set in the Reply To field for the mail. Default value is Sender Email. |

**Response:** `provider`

## createSmtpProvider

`createSmtpProvider` **(DEPRECATED — use `messaging.createSMTPProvider` instead)**
Create a new SMTP provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `host` | string | Yes | SMTP hosts. Either a single hostname or multiple semicolon-delimited hostnames. You can also specify a different port for each host such as `smtp1.example.com:25;smtp2.example.com`. You can also specify encryption type, for example: `tls://smtp1.example.com:587;ssl://smtp2.example.com:465&quot;`. Hosts will be tried in order. |
| `port` | integer | No | The default SMTP server port. (default: `587`) |
| `username` | string | No | Authentication username. |
| `password` | string | No | Authentication password. |
| `encryption` | string | No | Encryption type. Can be omitted, &#039;ssl&#039;, or &#039;tls&#039; |
| `autoTLS` | boolean | No | Enable SMTP AutoTLS feature. (default: `1`) |
| `mailer` | string | No | The value to use for the X-Mailer header. |
| `fromName` | string | No | Sender Name. |
| `fromEmail` | string | No | Sender email address. |
| `replyToName` | string | No | Name set in the reply to field for the mail. Default value is sender name. |
| `replyToEmail` | string | No | Email set in the reply to field for the mail. Default value is sender email. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## createSMTPProvider

`createSMTPProvider`
Create a new SMTP provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `host` | string | Yes | SMTP hosts. Either a single hostname or multiple semicolon-delimited hostnames. You can also specify a different port for each host such as `smtp1.example.com:25;smtp2.example.com`. You can also specify encryption type, for example: `tls://smtp1.example.com:587;ssl://smtp2.example.com:465&quot;`. Hosts will be tried in order. |
| `port` | integer | No | The default SMTP server port. (default: `587`) |
| `username` | string | No | Authentication username. |
| `password` | string | No | Authentication password. |
| `encryption` | string | No | Encryption type. Can be omitted, &#039;ssl&#039;, or &#039;tls&#039; |
| `autoTLS` | boolean | No | Enable SMTP AutoTLS feature. (default: `1`) |
| `mailer` | string | No | The value to use for the X-Mailer header. |
| `fromName` | string | No | Sender Name. |
| `fromEmail` | string | No | Sender email address. |
| `replyToName` | string | No | Name set in the reply to field for the mail. Default value is sender name. |
| `replyToEmail` | string | No | Email set in the reply to field for the mail. Default value is sender email. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## updateSmtpProvider

`updateSmtpProvider` **(DEPRECATED — use `messaging.updateSMTPProvider` instead)**
Update a SMTP provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `host` | string | No | SMTP hosts. Either a single hostname or multiple semicolon-delimited hostnames. You can also specify a different port for each host such as `smtp1.example.com:25;smtp2.example.com`. You can also specify encryption type, for example: `tls://smtp1.example.com:587;ssl://smtp2.example.com:465&quot;`. Hosts will be tried in order. |
| `port` | integer | No | SMTP port. |
| `username` | string | No | Authentication username. |
| `password` | string | No | Authentication password. |
| `encryption` | string | No | Encryption type. Can be &#039;ssl&#039; or &#039;tls&#039; |
| `autoTLS` | boolean | No | Enable SMTP AutoTLS feature. |
| `mailer` | string | No | The value to use for the X-Mailer header. |
| `fromName` | string | No | Sender Name. |
| `fromEmail` | string | No | Sender email address. |
| `replyToName` | string | No | Name set in the Reply To field for the mail. Default value is Sender Name. |
| `replyToEmail` | string | No | Email set in the Reply To field for the mail. Default value is Sender Email. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## updateSMTPProvider

`updateSMTPProvider`
Update a SMTP provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `host` | string | No | SMTP hosts. Either a single hostname or multiple semicolon-delimited hostnames. You can also specify a different port for each host such as `smtp1.example.com:25;smtp2.example.com`. You can also specify encryption type, for example: `tls://smtp1.example.com:587;ssl://smtp2.example.com:465&quot;`. Hosts will be tried in order. |
| `port` | integer | No | SMTP port. |
| `username` | string | No | Authentication username. |
| `password` | string | No | Authentication password. |
| `encryption` | string | No | Encryption type. Can be &#039;ssl&#039; or &#039;tls&#039; |
| `autoTLS` | boolean | No | Enable SMTP AutoTLS feature. |
| `mailer` | string | No | The value to use for the X-Mailer header. |
| `fromName` | string | No | Sender Name. |
| `fromEmail` | string | No | Sender email address. |
| `replyToName` | string | No | Name set in the Reply To field for the mail. Default value is Sender Name. |
| `replyToEmail` | string | No | Email set in the Reply To field for the mail. Default value is Sender Email. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## Create Telesign provider

`createTelesignProvider`
Create a new Telesign provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `from` | string | No | Sender Phone number. Format this number with a leading &#039;+&#039; and a country code, e.g., +16175551212. |
| `customerId` | string | No | Telesign customer ID. |
| `apiKey` | string | No | Telesign API key. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## Update Telesign provider

`updateTelesignProvider`
Update a Telesign provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `enabled` | boolean | No | Set as enabled. |
| `customerId` | string | No | Telesign customer ID. |
| `apiKey` | string | No | Telesign API key. |
| `from` | string | No | Sender number. |

**Response:** `provider`

## Create Textmagic provider

`createTextmagicProvider`
Create a new Textmagic provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `from` | string | No | Sender Phone number. Format this number with a leading &#039;+&#039; and a country code, e.g., +16175551212. |
| `username` | string | No | Textmagic username. |
| `apiKey` | string | No | Textmagic apiKey. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## Update Textmagic provider

`updateTextmagicProvider`
Update a Textmagic provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `enabled` | boolean | No | Set as enabled. |
| `username` | string | No | Textmagic username. |
| `apiKey` | string | No | Textmagic apiKey. |
| `from` | string | No | Sender number. |

**Response:** `provider`

## Create Twilio provider

`createTwilioProvider`
Create a new Twilio provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `from` | string | No | Sender Phone number. Format this number with a leading &#039;+&#039; and a country code, e.g., +16175551212. |
| `accountSid` | string | No | Twilio account secret ID. |
| `authToken` | string | No | Twilio authentication token. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## Update Twilio provider

`updateTwilioProvider`
Update a Twilio provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `enabled` | boolean | No | Set as enabled. |
| `accountSid` | string | No | Twilio account secret ID. |
| `authToken` | string | No | Twilio authentication token. |
| `from` | string | No | Sender number. |

**Response:** `provider`

## Create Vonage provider

`createVonageProvider`
Create a new Vonage provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Provider name. |
| `from` | string | No | Sender Phone number. Format this number with a leading &#039;+&#039; and a country code, e.g., +16175551212. |
| `apiKey` | string | No | Vonage API key. |
| `apiSecret` | string | No | Vonage API secret. |
| `enabled` | boolean | No | Set as enabled. |

**Response:** `provider`

## Update Vonage provider

`updateVonageProvider`
Update a Vonage provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `name` | string | No | Provider name. |
| `enabled` | boolean | No | Set as enabled. |
| `apiKey` | string | No | Vonage API key. |
| `apiSecret` | string | No | Vonage API secret. |
| `from` | string | No | Sender number. |

**Response:** `provider`

## Get provider

`getProvider`
Get a provider by its unique ID.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |

**Response:** `provider`

## Delete provider

`deleteProvider`
Delete a provider by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |


## List provider logs

`listProviderLogs`
Get the provider activity logs listed by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `providerId` | string | Yes | Provider ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `logList`

## List subscriber logs

`listSubscriberLogs`
Get the subscriber activity logs listed by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `subscriberId` | string | Yes | Subscriber ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `logList`

## List topics

`listTopics`
Get a list of all topics from the current Appwrite project.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: name, description, emailTotal, smsTotal, pushTotal (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `topicList`

## Create topic

`createTopic`
Create a new topic.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `topicId` | string | Yes | Topic ID. Choose a custom Topic ID or a new Topic ID. |
| `name` | string | Yes | Topic Name. |
| `subscribe` | array\<string\> | No | An array of role strings with subscribe permission. By default all users are granted with any subscribe permission. [learn more about roles](https://appwrite.io/docs/permissions#permission-roles). Maximum of 100 roles are allowed, each 64 characters long. (default: `[&quot;users&quot;]`) |

**Response:** `topic`

## Get topic

`getTopic`
Get a topic by its unique ID.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `topicId` | string | Yes | Topic ID. |

**Response:** `topic`

## Update topic

`updateTopic`
Update a topic by its unique ID.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `topicId` | string | Yes | Topic ID. |
| `name` | string | No | Topic Name. |
| `subscribe` | array\<string\> | No | An array of role strings with subscribe permission. By default all users are granted with any subscribe permission. [learn more about roles](https://appwrite.io/docs/permissions#permission-roles). Maximum of 100 roles are allowed, each 64 characters long. |

**Response:** `topic`

## Delete topic

`deleteTopic`
Delete a topic by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `topicId` | string | Yes | Topic ID. |


## List topic logs

`listTopicLogs`
Get the topic activity logs listed by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `topicId` | string | Yes | Topic ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `logList`

## List subscribers

`listSubscribers`
Get a list of all subscribers from the current Appwrite project.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `topicId` | string | Yes | Topic ID. The topic ID subscribed to. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: name, provider, type, enabled (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `subscriberList`

## Create subscriber

`createSubscriber`
Create a new subscriber.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `topicId` | string | Yes | Topic ID. The topic ID to subscribe to. |
| `subscriberId` | string | Yes | Subscriber ID. Choose a custom Subscriber ID or a new Subscriber ID. |
| `targetId` | string | Yes | Target ID. The target ID to link to the specified Topic ID. |

**Response:** `subscriber`

## Get subscriber

`getSubscriber`
Get a subscriber by its unique ID.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `topicId` | string | Yes | Topic ID. The topic ID subscribed to. |
| `subscriberId` | string | Yes | Subscriber ID. |

**Response:** `subscriber`

## Delete subscriber

`deleteSubscriber`
Delete a subscriber by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `topicId` | string | Yes | Topic ID. The topic ID subscribed to. |
| `subscriberId` | string | Yes | Subscriber ID. |


