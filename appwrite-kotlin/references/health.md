# Health

The Health service allows you to both validate and monitor your Appwrite server&#039;s health.

## Get HTTP

`get`
Check the Appwrite HTTP server is up and responsive.


**Response:** `healthStatus`

## Get antivirus

`getAntivirus`
Check the Appwrite Antivirus server is up and connection is successful.


**Response:** `healthAntivirus`

## Get cache

`getCache`
Check the Appwrite in-memory cache servers are up and connection is successful.


**Response:** `healthStatusList`

## Get the SSL certificate for a domain

`getCertificate`
Get the SSL certificate for a domain

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `domain` | string | No | string |

**Response:** `healthCertificate`

## Get DB

`getDB`
Check the Appwrite database servers are up and connection is successful.


**Response:** `healthStatusList`

## Get pubsub

`getPubSub`
Check the Appwrite pub-sub servers are up and connection is successful.


**Response:** `healthStatusList`

## Get audits queue

`getQueueAudits`
Get the number of audit logs that are waiting to be processed in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get builds queue

`getQueueBuilds`
Get the number of builds that are waiting to be processed in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get certificates queue

`getQueueCertificates`
Get the number of certificates that are waiting to be issued against [Letsencrypt](https://letsencrypt.org/) in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get databases queue

`getQueueDatabases`
Get the number of database changes that are waiting to be processed in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `name` | string | No | Queue name for which to check the queue size (default: `database_db_main`) |
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get deletes queue

`getQueueDeletes`
Get the number of background destructive changes that are waiting to be processed in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get number of failed queue jobs

`getFailedJobs`
Returns the amount of failed jobs in a given queue.


| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `name` | string | Yes | The name of the queue |
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get functions queue

`getQueueFunctions`
Get the number of function executions that are waiting to be processed in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get logs queue

`getQueueLogs`
Get the number of logs that are waiting to be processed in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get mails queue

`getQueueMails`
Get the number of mails that are waiting to be processed in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get messaging queue

`getQueueMessaging`
Get the number of messages that are waiting to be processed in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get migrations queue

`getQueueMigrations`
Get the number of migrations that are waiting to be processed in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get stats resources queue

`getQueueStatsResources`
Get the number of metrics that are waiting to be processed in the Appwrite stats resources queue.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get stats usage queue

`getQueueUsage`
Get the number of metrics that are waiting to be processed in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get webhooks queue

`getQueueWebhooks`
Get the number of webhooks that are waiting to be processed in the Appwrite internal queue server.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `threshold` | integer | No | Queue size threshold. When hit (equal or higher), endpoint returns server error. Default value is 5000. (default: `5000`) |

**Response:** `healthQueue`

## Get storage

`getStorage`
Check the Appwrite storage device is up and connection is successful.


**Response:** `healthStatus`

## Get local storage

`getStorageLocal`
Check the Appwrite local storage device is up and connection is successful.


**Response:** `healthStatus`

## Get time

`getTime`
Check the Appwrite server time is synced with Google remote NTP server. We use this technology to smoothly handle leap seconds with no disruptive events. The [Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol) (NTP) is used by hundreds of millions of computers and devices to synchronize their clocks over the Internet. If your computer sets its own clock, it likely uses NTP.


**Response:** `healthTime`

