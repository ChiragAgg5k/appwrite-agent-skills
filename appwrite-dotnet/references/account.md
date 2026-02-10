# Account

The Account service allows you to authenticate and manage a user account.

## Get account

`get`
Get the currently logged in user.


**Response:** `user`

## Create account

`create`
Use this endpoint to allow a new user to register a new account in your project. After the user registration completes successfully, you can use the [/account/verfication](https://appwrite.io/docs/references/cloud/client-web/account#createVerification) route to start verifying the user email address. To allow the new user to login to their new account, you need to create a new [account session](https://appwrite.io/docs/references/cloud/client-web/account#createEmailSession).

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `email` | string | Yes | User email. |
| `password` | string | Yes | New user password. Must be between 8 and 256 chars. |
| `name` | string | No | User name. Max length: 128 chars. |

**Response:** `user`

## Delete account

`delete`
Delete the currently logged in user.



## Update email

`updateEmail`
Update currently logged in user account email address. After changing user address, the user confirmation status will get reset. A new confirmation email is not sent automatically however you can use the send confirmation email endpoint again to send the confirmation email. For security measures, user password is required to complete this request.
This endpoint can also be used to convert an anonymous account to a normal one, by passing an email address and a new password.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `email` | string | Yes | User email. |
| `password` | string | Yes | User password. Must be at least 8 chars. |

**Response:** `user`

## List identities

`listIdentities`
Get the list of identities for the currently logged in user.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: userId, provider, providerUid, providerEmail, providerAccessTokenExpiry (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `identityList`

## Delete identity

`deleteIdentity`
Delete an identity by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `identityId` | string | Yes | Identity ID. |


## Create JWT

`createJWT`
Use this endpoint to create a JSON Web Token. You can use the resulting JWT to authenticate on behalf of the current user when working with the Appwrite server-side API and SDKs. The JWT secret is valid for 15 minutes from its creation and will be invalid if the user will logout in that time frame.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `duration` | integer | No | Time in seconds before JWT expires. Default duration is 900 seconds, and maximum is 3600 seconds. (default: `900`) |

**Response:** `jwt`

## List logs

`listLogs`
Get the list of latest security activity logs for the currently logged in user. Each log returns user IP address, location and date and time of log.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Only supported methods are limit and offset (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `logList`

## Update MFA

`updateMFA`
Enable or disable MFA on an account.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `mfa` | boolean | Yes | Enable or disable MFA. |

**Response:** `user`

## createMfaAuthenticator

`createMfaAuthenticator` **(DEPRECATED — use `account.createMFAAuthenticator` instead)**
Add an authenticator app to be used as an MFA factor. Verify the authenticator using the [verify authenticator](/docs/references/cloud/client-web/account#updateMfaAuthenticator) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `type` | string | Yes | Type of authenticator. Must be `totp` |

**Response:** `mfaType`

## createMFAAuthenticator

`createMFAAuthenticator`
Add an authenticator app to be used as an MFA factor. Verify the authenticator using the [verify authenticator](/docs/references/cloud/client-web/account#updateMfaAuthenticator) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `type` | string | Yes | Type of authenticator. Must be `totp` |

**Response:** `mfaType`

## updateMfaAuthenticator

`updateMfaAuthenticator` **(DEPRECATED — use `account.updateMFAAuthenticator` instead)**
Verify an authenticator app after adding it using the [add authenticator](/docs/references/cloud/client-web/account#createMfaAuthenticator) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `type` | string | Yes | Type of authenticator. |
| `otp` | string | Yes | Valid verification token. |

**Response:** `user`

## updateMFAAuthenticator

`updateMFAAuthenticator`
Verify an authenticator app after adding it using the [add authenticator](/docs/references/cloud/client-web/account#createMfaAuthenticator) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `type` | string | Yes | Type of authenticator. |
| `otp` | string | Yes | Valid verification token. |

**Response:** `user`

## deleteMfaAuthenticator

`deleteMfaAuthenticator` **(DEPRECATED — use `account.deleteMFAAuthenticator` instead)**
Delete an authenticator for a user by ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `type` | string | Yes | Type of authenticator. |


## deleteMFAAuthenticator

`deleteMFAAuthenticator`
Delete an authenticator for a user by ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `type` | string | Yes | Type of authenticator. |


## createMfaChallenge

`createMfaChallenge` **(DEPRECATED — use `account.createMFAChallenge` instead)**
Begin the process of MFA verification after sign-in. Finish the flow with [updateMfaChallenge](/docs/references/cloud/client-web/account#updateMfaChallenge) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `factor` | string | Yes | Factor used for verification. Must be one of following: `email`, `phone`, `totp`, `recoveryCode`. |

**Response:** `mfaChallenge`

## createMFAChallenge

`createMFAChallenge`
Begin the process of MFA verification after sign-in. Finish the flow with [updateMfaChallenge](/docs/references/cloud/client-web/account#updateMfaChallenge) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `factor` | string | Yes | Factor used for verification. Must be one of following: `email`, `phone`, `totp`, `recoveryCode`. |

**Response:** `mfaChallenge`

## updateMfaChallenge

`updateMfaChallenge` **(DEPRECATED — use `account.updateMFAChallenge` instead)**
Complete the MFA challenge by providing the one-time password. Finish the process of MFA verification by providing the one-time password. To begin the flow, use [createMfaChallenge](/docs/references/cloud/client-web/account#createMfaChallenge) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `challengeId` | string | Yes | ID of the challenge. |
| `otp` | string | Yes | Valid verification token. |

**Response:** `session`

## updateMFAChallenge

`updateMFAChallenge`
Complete the MFA challenge by providing the one-time password. Finish the process of MFA verification by providing the one-time password. To begin the flow, use [createMfaChallenge](/docs/references/cloud/client-web/account#createMfaChallenge) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `challengeId` | string | Yes | ID of the challenge. |
| `otp` | string | Yes | Valid verification token. |

**Response:** `session`

## listMfaFactors

`listMfaFactors` **(DEPRECATED — use `account.listMFAFactors` instead)**
List the factors available on the account to be used as a MFA challange.


**Response:** `mfaFactors`

## listMFAFactors

`listMFAFactors`
List the factors available on the account to be used as a MFA challange.


**Response:** `mfaFactors`

## getMfaRecoveryCodes

`getMfaRecoveryCodes` **(DEPRECATED — use `account.getMFARecoveryCodes` instead)**
Get recovery codes that can be used as backup for MFA flow. Before getting codes, they must be generated using [createMfaRecoveryCodes](/docs/references/cloud/client-web/account#createMfaRecoveryCodes) method. An OTP challenge is required to read recovery codes.


**Response:** `mfaRecoveryCodes`

## getMFARecoveryCodes

`getMFARecoveryCodes`
Get recovery codes that can be used as backup for MFA flow. Before getting codes, they must be generated using [createMfaRecoveryCodes](/docs/references/cloud/client-web/account#createMfaRecoveryCodes) method. An OTP challenge is required to read recovery codes.


**Response:** `mfaRecoveryCodes`

## createMfaRecoveryCodes

`createMfaRecoveryCodes` **(DEPRECATED — use `account.createMFARecoveryCodes` instead)**
Generate recovery codes as backup for MFA flow. It&#039;s recommended to generate and show then immediately after user successfully adds their authehticator. Recovery codes can be used as a MFA verification type in [createMfaChallenge](/docs/references/cloud/client-web/account#createMfaChallenge) method.


**Response:** `mfaRecoveryCodes`

## createMFARecoveryCodes

`createMFARecoveryCodes`
Generate recovery codes as backup for MFA flow. It&#039;s recommended to generate and show then immediately after user successfully adds their authehticator. Recovery codes can be used as a MFA verification type in [createMfaChallenge](/docs/references/cloud/client-web/account#createMfaChallenge) method.


**Response:** `mfaRecoveryCodes`

## updateMfaRecoveryCodes

`updateMfaRecoveryCodes` **(DEPRECATED — use `account.updateMFARecoveryCodes` instead)**
Regenerate recovery codes that can be used as backup for MFA flow. Before regenerating codes, they must be first generated using [createMfaRecoveryCodes](/docs/references/cloud/client-web/account#createMfaRecoveryCodes) method. An OTP challenge is required to regenreate recovery codes.


**Response:** `mfaRecoveryCodes`

## updateMFARecoveryCodes

`updateMFARecoveryCodes`
Regenerate recovery codes that can be used as backup for MFA flow. Before regenerating codes, they must be first generated using [createMfaRecoveryCodes](/docs/references/cloud/client-web/account#createMfaRecoveryCodes) method. An OTP challenge is required to regenreate recovery codes.


**Response:** `mfaRecoveryCodes`

## Update name

`updateName`
Update currently logged in user account name.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `name` | string | Yes | User name. Max length: 128 chars. |

**Response:** `user`

## Update password

`updatePassword`
Update currently logged in user password. For validation, user is required to pass in the new password, and the old password. For users created with OAuth, Team Invites and Magic URL, oldPassword is optional.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `password` | string | Yes | New user password. Must be at least 8 chars. |
| `oldPassword` | string | No | Current user password. Must be at least 8 chars. |

**Response:** `user`

## Update phone

`updatePhone`
Update the currently logged in user&#039;s phone number. After updating the phone number, the phone verification status will be reset. A confirmation SMS is not sent automatically, however you can use the [POST /account/verification/phone](https://appwrite.io/docs/references/cloud/client-web/account#createPhoneVerification) endpoint to send a confirmation SMS.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `phone` | string | Yes | Phone number. Format this number with a leading &#039;+&#039; and a country code, e.g., +16175551212. |
| `password` | string | Yes | User password. Must be at least 8 chars. |

**Response:** `user`

## Get account preferences

`getPrefs`
Get the preferences as a key-value object for the currently logged in user.


**Response:** `preferences`

## Update preferences

`updatePrefs`
Update currently logged in user account preferences. The object you pass is stored as is, and replaces any previous value. The maximum allowed prefs size is 64kB and throws error if exceeded.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `prefs` | object | Yes | Prefs key-value JSON object. (default: `{}`) |

**Response:** `user`

## Create password recovery

`createRecovery`
Sends the user an email with a temporary secret key for password reset. When the user clicks the confirmation link he is redirected back to your app password reset URL with the secret key and email address values attached to the URL query string. Use the query string params to submit a request to the [PUT /account/recovery](https://appwrite.io/docs/references/cloud/client-web/account#updateRecovery) endpoint to complete the process. The verification link sent to the user&#039;s email address is valid for 1 hour.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `email` | string | Yes | User email. |
| `url` | string | Yes | URL to redirect the user back to your app from the recovery email. Only URLs from hostnames in your project platform list are allowed. This requirement helps to prevent an [open redirect](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html) attack against your project API. |

**Response:** `token`

## Update password recovery (confirmation)

`updateRecovery`
Use this endpoint to complete the user account password reset. Both the **userId** and **secret** arguments will be passed as query parameters to the redirect URL you have provided when sending your request to the [POST /account/recovery](https://appwrite.io/docs/references/cloud/client-web/account#createRecovery) endpoint.

Please note that in order to avoid a [Redirect Attack](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.md) the only valid redirect URLs are the ones from domains you have set when adding your platforms in the console interface.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `secret` | string | Yes | Valid reset token. |
| `password` | string | Yes | New user password. Must be between 8 and 256 chars. |

**Response:** `token`

## List sessions

`listSessions`
Get the list of active sessions across different devices for the currently logged in user.


**Response:** `sessionList`

## Delete sessions

`deleteSessions`
Delete all sessions from the user account and remove any sessions cookies from the end client.



## Create anonymous session

`createAnonymousSession`
Use this endpoint to allow a new user to register an anonymous account in your project. This route will also create a new session for the user. To allow the new user to convert an anonymous account to a normal account, you need to update its [email and password](https://appwrite.io/docs/references/cloud/client-web/account#updateEmail) or create an [OAuth2 session](https://appwrite.io/docs/references/cloud/client-web/account#CreateOAuth2Session).


**Response:** `session`

## Create email password session

`createEmailPasswordSession`
Allow the user to login into their account by providing a valid email and password combination. This route will create a new session for the user.

A user is limited to 10 active sessions at a time by default. [Learn more about session limits](https://appwrite.io/docs/authentication-security#limits).

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `email` | string | Yes | User email. |
| `password` | string | Yes | User password. Must be at least 8 chars. |

**Response:** `session`

## Update magic URL session

`updateMagicURLSession` **(DEPRECATED — use `account.createSession` instead)**
Use this endpoint to create a session from token. Provide the **userId** and **secret** parameters from the successful response of authentication flows initiated by token creation. For example, magic URL and phone login.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `secret` | string | Yes | Valid verification token. |

**Response:** `session`

## Create OAuth2 session

`createOAuth2Session`
Allow the user to login to their account using the OAuth2 provider of their choice. Each OAuth2 provider should be enabled from the Appwrite console first. Use the success and failure arguments to provide a redirect URL&#039;s back to your app when login is completed.

If there is already an active session, the new session will be attached to the logged-in account. If there are no active sessions, the server will attempt to look for a user with the same email address as the email received from the OAuth2 provider and attach the new session to the existing user. If no matching user is found - the server will create a new user.

A user is limited to 10 active sessions at a time by default. [Learn more about session limits](https://appwrite.io/docs/authentication-security#limits).


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `provider` | string | Yes | OAuth2 Provider. Currently, supported providers are: amazon, apple, auth0, authentik, autodesk, bitbucket, bitly, box, dailymotion, discord, disqus, dropbox, etsy, facebook, figma, github, gitlab, google, linkedin, microsoft, notion, oidc, okta, paypal, paypalSandbox, podio, salesforce, slack, spotify, stripe, tradeshift, tradeshiftBox, twitch, wordpress, yahoo, yammer, yandex, zoho, zoom. |
| `success` | string | No | URL to redirect back to your app after a successful login attempt.  Only URLs from hostnames in your project&#039;s platform list are allowed. This requirement helps to prevent an [open redirect](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html) attack against your project API. |
| `failure` | string | No | URL to redirect back to your app after a failed login attempt.  Only URLs from hostnames in your project&#039;s platform list are allowed. This requirement helps to prevent an [open redirect](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html) attack against your project API. |
| `scopes` | array\<string\> | No | A list of custom OAuth2 scopes. Check each provider internal docs for a list of supported scopes. Maximum of 100 scopes are allowed, each 4096 characters long. (default: `[]`) |


## Update phone session

`updatePhoneSession` **(DEPRECATED — use `account.createSession` instead)**
Use this endpoint to create a session from token. Provide the **userId** and **secret** parameters from the successful response of authentication flows initiated by token creation. For example, magic URL and phone login.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `secret` | string | Yes | Valid verification token. |

**Response:** `session`

## Create session

`createSession`
Use this endpoint to create a session from token. Provide the **userId** and **secret** parameters from the successful response of authentication flows initiated by token creation. For example, magic URL and phone login.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `secret` | string | Yes | Secret of a token generated by login methods. For example, the `createMagicURLToken` or `createPhoneToken` methods. |

**Response:** `session`

## Get session

`getSession`
Use this endpoint to get a logged in user&#039;s session using a Session ID. Inputting &#039;current&#039; will return the current session being used.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `sessionId` | string | Yes | Session ID. Use the string &#039;current&#039; to get the current device session. |

**Response:** `session`

## Update session

`updateSession`
Use this endpoint to extend a session&#039;s length. Extending a session is useful when session expiry is short. If the session was created using an OAuth provider, this endpoint refreshes the access token from the provider.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `sessionId` | string | Yes | Session ID. Use the string &#039;current&#039; to update the current device session. |

**Response:** `session`

## Delete session

`deleteSession`
Logout the user. Use &#039;current&#039; as the session ID to logout on this device, use a session ID to logout on another device. If you&#039;re looking to logout the user on all devices, use [Delete Sessions](https://appwrite.io/docs/references/cloud/client-web/account#deleteSessions) instead.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `sessionId` | string | Yes | Session ID. Use the string &#039;current&#039; to delete the current device session. |


## Update status

`updateStatus`
Block the currently logged in user account. Behind the scene, the user record is not deleted but permanently blocked from any access. To completely delete a user, use the Users API instead.


**Response:** `user`

## Create push target

`createPushTarget`
Use this endpoint to register a device for push notifications. Provide a target ID (custom or generated using ID.unique()), a device identifier (usually a device token), and optionally specify which provider should send notifications to this target. The target is automatically linked to the current session and includes device information like brand and model.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `targetId` | string | Yes | Target ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `identifier` | string | Yes | The target identifier (token, email, phone etc.) |
| `providerId` | string | No | Provider ID. Message will be sent to this target from the specified provider ID. If no provider ID is set the first setup provider will be used. |

**Response:** `target`

## Update push target

`updatePushTarget`
Update the currently logged in user&#039;s push notification target. You can modify the target&#039;s identifier (device token) and provider ID (token, email, phone etc.). The target must exist and belong to the current user. If you change the provider ID, notifications will be sent through the new messaging provider instead.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `targetId` | string | Yes | Target ID. |
| `identifier` | string | Yes | The target identifier (token, email, phone etc.) |

**Response:** `target`

## Delete push target

`deletePushTarget`
Delete a push notification target for the currently logged in user. After deletion, the device will no longer receive push notifications. The target must exist and belong to the current user.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `targetId` | string | Yes | Target ID. |


## Create email token (OTP)

`createEmailToken`
Sends the user an email with a secret key for creating a session. If the email address has never been used, a **new account is created** using the provided `userId`. Otherwise, if the email address is already attached to an account, the **user ID is ignored**. Then, the user will receive an email with the one-time password. Use the returned user ID and secret and submit a request to the [POST /v1/account/sessions/token](https://appwrite.io/docs/references/cloud/client-web/account#createSession) endpoint to complete the login process. The secret sent to the user&#039;s email is valid for 15 minutes.

A user is limited to 10 active sessions at a time by default. [Learn more about session limits](https://appwrite.io/docs/authentication-security#limits).


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. If the email address has never been used, a new account is created using the provided userId. Otherwise, if the email address is already attached to an account, the user ID is ignored. |
| `email` | string | Yes | User email. |
| `phrase` | boolean | No | Toggle for security phrase. If enabled, email will be send with a randomly generated phrase and the phrase will also be included in the response. Confirming phrases match increases the security of your authentication flow. |

**Response:** `token`

## Create magic URL token

`createMagicURLToken`
Sends the user an email with a secret key for creating a session. If the provided user ID has not been registered, a new user will be created. When the user clicks the link in the email, the user is redirected back to the URL you provided with the secret key and userId values attached to the URL query string. Use the query string parameters to submit a request to the [POST /v1/account/sessions/token](https://appwrite.io/docs/references/cloud/client-web/account#createSession) endpoint to complete the login process. The link sent to the user&#039;s email address is valid for 1 hour.

A user is limited to 10 active sessions at a time by default. [Learn more about session limits](https://appwrite.io/docs/authentication-security#limits).


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | Unique Id. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. If the email address has never been used, a new account is created using the provided userId. Otherwise, if the email address is already attached to an account, the user ID is ignored. |
| `email` | string | Yes | User email. |
| `url` | string | No | URL to redirect the user back to your app from the magic URL login. Only URLs from hostnames in your project platform list are allowed. This requirement helps to prevent an [open redirect](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html) attack against your project API. |
| `phrase` | boolean | No | Toggle for security phrase. If enabled, email will be send with a randomly generated phrase and the phrase will also be included in the response. Confirming phrases match increases the security of your authentication flow. |

**Response:** `token`

## Create OAuth2 token

`createOAuth2Token`
Allow the user to login to their account using the OAuth2 provider of their choice. Each OAuth2 provider should be enabled from the Appwrite console first. Use the success and failure arguments to provide a redirect URL&#039;s back to your app when login is completed. 

If authentication succeeds, `userId` and `secret` of a token will be appended to the success URL as query parameters. These can be used to create a new session using the [Create session](https://appwrite.io/docs/references/cloud/client-web/account#createSession) endpoint.

A user is limited to 10 active sessions at a time by default. [Learn more about session limits](https://appwrite.io/docs/authentication-security#limits).

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `provider` | string | Yes | OAuth2 Provider. Currently, supported providers are: amazon, apple, auth0, authentik, autodesk, bitbucket, bitly, box, dailymotion, discord, disqus, dropbox, etsy, facebook, figma, github, gitlab, google, linkedin, microsoft, notion, oidc, okta, paypal, paypalSandbox, podio, salesforce, slack, spotify, stripe, tradeshift, tradeshiftBox, twitch, wordpress, yahoo, yammer, yandex, zoho, zoom. |
| `success` | string | No | URL to redirect back to your app after a successful login attempt.  Only URLs from hostnames in your project&#039;s platform list are allowed. This requirement helps to prevent an [open redirect](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html) attack against your project API. |
| `failure` | string | No | URL to redirect back to your app after a failed login attempt.  Only URLs from hostnames in your project&#039;s platform list are allowed. This requirement helps to prevent an [open redirect](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html) attack against your project API. |
| `scopes` | array\<string\> | No | A list of custom OAuth2 scopes. Check each provider internal docs for a list of supported scopes. Maximum of 100 scopes are allowed, each 4096 characters long. (default: `[]`) |


## Create phone token

`createPhoneToken`
Sends the user an SMS with a secret key for creating a session. If the provided user ID has not be registered, a new user will be created. Use the returned user ID and secret and submit a request to the [POST /v1/account/sessions/token](https://appwrite.io/docs/references/cloud/client-web/account#createSession) endpoint to complete the login process. The secret sent to the user&#039;s phone is valid for 15 minutes.

A user is limited to 10 active sessions at a time by default. [Learn more about session limits](https://appwrite.io/docs/authentication-security#limits).

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | Unique Id. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. If the phone number has never been used, a new account is created using the provided userId. Otherwise, if the phone number is already attached to an account, the user ID is ignored. |
| `phone` | string | Yes | Phone number. Format this number with a leading &#039;+&#039; and a country code, e.g., +16175551212. |

**Response:** `token`

## createEmailVerification

`createEmailVerification`
Use this endpoint to send a verification message to your user email address to confirm they are the valid owners of that address. Both the **userId** and **secret** arguments will be passed as query parameters to the URL you have provided to be attached to the verification email. The provided URL should redirect the user back to your app and allow you to complete the verification process by verifying both the **userId** and **secret** parameters. Learn more about how to [complete the verification process](https://appwrite.io/docs/references/cloud/client-web/account#updateVerification). The verification link sent to the user&#039;s email address is valid for 7 days.

Please note that in order to avoid a [Redirect Attack](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.md), the only valid redirect URLs are the ones from domains you have set when adding your platforms in the console interface.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `url` | string | Yes | URL to redirect the user back to your app from the verification email. Only URLs from hostnames in your project platform list are allowed. This requirement helps to prevent an [open redirect](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html) attack against your project API. |

**Response:** `token`

## createVerification

`createVerification` **(DEPRECATED — use `account.createEmailVerification` instead)**
Use this endpoint to send a verification message to your user email address to confirm they are the valid owners of that address. Both the **userId** and **secret** arguments will be passed as query parameters to the URL you have provided to be attached to the verification email. The provided URL should redirect the user back to your app and allow you to complete the verification process by verifying both the **userId** and **secret** parameters. Learn more about how to [complete the verification process](https://appwrite.io/docs/references/cloud/client-web/account#updateVerification). The verification link sent to the user&#039;s email address is valid for 7 days.

Please note that in order to avoid a [Redirect Attack](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.md), the only valid redirect URLs are the ones from domains you have set when adding your platforms in the console interface.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `url` | string | Yes | URL to redirect the user back to your app from the verification email. Only URLs from hostnames in your project platform list are allowed. This requirement helps to prevent an [open redirect](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html) attack against your project API. |

**Response:** `token`

## updateEmailVerification

`updateEmailVerification`
Use this endpoint to complete the user email verification process. Use both the **userId** and **secret** parameters that were attached to your app URL to verify the user email ownership. If confirmed this route will return a 200 status code.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `secret` | string | Yes | Valid verification token. |

**Response:** `token`

## updateVerification

`updateVerification` **(DEPRECATED — use `account.updateEmailVerification` instead)**
Use this endpoint to complete the user email verification process. Use both the **userId** and **secret** parameters that were attached to your app URL to verify the user email ownership. If confirmed this route will return a 200 status code.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `secret` | string | Yes | Valid verification token. |

**Response:** `token`

## Create phone verification

`createPhoneVerification`
Use this endpoint to send a verification SMS to the currently logged in user. This endpoint is meant for use after updating a user&#039;s phone number using the [accountUpdatePhone](https://appwrite.io/docs/references/cloud/client-web/account#updatePhone) endpoint. Learn more about how to [complete the verification process](https://appwrite.io/docs/references/cloud/client-web/account#updatePhoneVerification). The verification code sent to the user&#039;s phone number is valid for 15 minutes.


**Response:** `token`

## Update phone verification (confirmation)

`updatePhoneVerification`
Use this endpoint to complete the user phone verification process. Use the **userId** and **secret** that were sent to your user&#039;s phone number to verify the user email ownership. If confirmed this route will return a 200 status code.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `userId` | string | Yes | User ID. |
| `secret` | string | Yes | Valid verification token. |

**Response:** `token`

