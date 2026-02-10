# Functions

The Functions Service allows you view, create and manage your Cloud Functions.

## List functions

`list`
Get a list of all the project&#039;s functions. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: name, enabled, runtime, deploymentId, schedule, scheduleNext, schedulePrevious, timeout, entrypoint, commands, installationId (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `functionList`

## Create function

`create`
Create a new function. You can pass a list of [permissions](https://appwrite.io/docs/permissions) to allow different project users or team with access to execute the function using the client API.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Function name. Max length: 128 chars. |
| `runtime` | string | Yes | Execution runtime. |
| `execute` | array\<string\> | No | An array of role strings with execution permissions. By default no user is granted with any execute permissions. [learn more about roles](https://appwrite.io/docs/permissions#permission-roles). Maximum of 100 roles are allowed, each 64 characters long. (default: `[]`) |
| `events` | array\<string\> | No | Events list. Maximum of 100 events are allowed. (default: `[]`) |
| `schedule` | string | No | Schedule CRON syntax. |
| `timeout` | integer | No | Function maximum execution time in seconds. (default: `15`) |
| `enabled` | boolean | No | Is function enabled? When set to &#039;disabled&#039;, users cannot access the function but Server SDKs with and API key can still access the function. No data is lost when this is toggled. (default: `1`) |
| `logging` | boolean | No | When disabled, executions will exclude logs and errors, and will be slightly faster. (default: `1`) |
| `entrypoint` | string | No | Entrypoint File. This path is relative to the &quot;providerRootDirectory&quot;. |
| `commands` | string | No | Build Commands. |
| `scopes` | array\<string\> | No | List of scopes allowed for API key auto-generated for every execution. Maximum of 100 scopes are allowed. (default: `[]`) |
| `installationId` | string | No | Appwrite Installation ID for VCS (Version Control System) deployment. |
| `providerRepositoryId` | string | No | Repository ID of the repo linked to the function. |
| `providerBranch` | string | No | Production branch for the repo linked to the function. |
| `providerSilentMode` | boolean | No | Is the VCS (Version Control System) connection in silent mode for the repo linked to the function? In silent mode, comments will not be made on commits and pull requests. |
| `providerRootDirectory` | string | No | Path to function code in the linked repo. |
| `specification` | string | No | Runtime specification for the function and builds. (default: `[]`) |

**Response:** `function`

## List runtimes

`listRuntimes`
Get a list of all runtimes that are currently active on your instance.


**Response:** `runtimeList`

## List specifications

`listSpecifications`
List allowed function specifications for this instance.


**Response:** `specificationList`

## List templates

`listTemplates`
List available function templates. You can use template details in [createFunction](/docs/references/cloud/server-nodejs/functions#create) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `runtimes` | array\<string\> | No | List of runtimes allowed for filtering function templates. Maximum of 100 runtimes are allowed. (default: `[]`) |
| `useCases` | array\<string\> | No | List of use cases allowed for filtering function templates. Maximum of 100 use cases are allowed. (default: `[]`) |
| `limit` | integer | No | Limit the number of templates returned in the response. Default limit is 25, and maximum limit is 5000. (default: `25`) |
| `offset` | integer | No | Offset the list of returned templates. Maximum offset is 5000. (default: `0`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `templateFunctionList`

## Get function template

`getTemplate`
Get a function template using ID. You can use template details in [createFunction](/docs/references/cloud/server-nodejs/functions#create) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `templateId` | string | Yes | Template ID. |

**Response:** `templateFunction`

## Get functions usage

`listUsage`
Get usage metrics and statistics for all functions in the project. View statistics including total deployments, builds, logs, storage usage, and compute time. The response includes both current totals and historical data for each metric. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, defaults to 30 days.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageFunctions`

## Get function

`get`
Get a function by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |

**Response:** `function`

## Update function

`update`
Update function by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `name` | string | Yes | Function name. Max length: 128 chars. |
| `runtime` | string | No | Execution runtime. |
| `execute` | array\<string\> | No | An array of role strings with execution permissions. By default no user is granted with any execute permissions. [learn more about roles](https://appwrite.io/docs/permissions#permission-roles). Maximum of 100 roles are allowed, each 64 characters long. (default: `[]`) |
| `events` | array\<string\> | No | Events list. Maximum of 100 events are allowed. (default: `[]`) |
| `schedule` | string | No | Schedule CRON syntax. |
| `timeout` | integer | No | Maximum execution time in seconds. (default: `15`) |
| `enabled` | boolean | No | Is function enabled? When set to &#039;disabled&#039;, users cannot access the function but Server SDKs with and API key can still access the function. No data is lost when this is toggled. (default: `1`) |
| `logging` | boolean | No | When disabled, executions will exclude logs and errors, and will be slightly faster. (default: `1`) |
| `entrypoint` | string | No | Entrypoint File. This path is relative to the &quot;providerRootDirectory&quot;. |
| `commands` | string | No | Build Commands. |
| `scopes` | array\<string\> | No | List of scopes allowed for API Key auto-generated for every execution. Maximum of 100 scopes are allowed. (default: `[]`) |
| `installationId` | string | No | Appwrite Installation ID for VCS (Version Controle System) deployment. |
| `providerRepositoryId` | string | No | Repository ID of the repo linked to the function |
| `providerBranch` | string | No | Production branch for the repo linked to the function |
| `providerSilentMode` | boolean | No | Is the VCS (Version Control System) connection in silent mode for the repo linked to the function? In silent mode, comments will not be made on commits and pull requests. |
| `providerRootDirectory` | string | No | Path to function code in the linked repo. |
| `specification` | string | No | Runtime specification for the function and builds. (default: `[]`) |

**Response:** `function`

## Delete function

`delete`
Delete a function by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |


## Update function&#039;s deployment

`updateFunctionDeployment`
Update the function active deployment. Use this endpoint to switch the code deployment that should be used when visitor opens your function.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `deploymentId` | string | Yes | Deployment ID. |

**Response:** `function`

## List deployments

`listDeployments`
Get a list of all the function&#039;s code deployments. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: buildSize, sourceSize, totalSize, buildDuration, status, activate, type (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `deploymentList`

## Create deployment

`createDeployment`
Create a new function code deployment. Use this endpoint to upload a new version of your code function. To execute your newly uploaded code, you&#039;ll need to update the function&#039;s deployment to use your new deployment UID.

This endpoint accepts a tar.gz file compressed with your code. Make sure to include any dependencies your code has within the compressed file. You can learn more about code packaging in the [Appwrite Cloud Functions tutorial](https://appwrite.io/docs/functions).

Use the &quot;command&quot; param to set the entrypoint used to execute your code.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `code` | file | Yes | Gzip file with your code package. When used with the Appwrite CLI, pass the path to your code directory, and the CLI will automatically package your code. Use a path that is within the current directory. |
| `activate` | boolean | Yes | Automatically activate the deployment when it is finished building. |
| `entrypoint` | string | No | Entrypoint File. |
| `commands` | string | No | Build Commands. |

**Response:** `deployment`

## Create duplicate deployment

`createDuplicateDeployment`
Create a new build for an existing function deployment. This endpoint allows you to rebuild a deployment with the updated function configuration, including its entrypoint and build commands if they have been modified. The build process will be queued and executed asynchronously. The original deployment&#039;s code will be preserved and used for the new build.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `deploymentId` | string | Yes | Deployment ID. |
| `buildId` | string | No | Build unique ID. |

**Response:** `deployment`

## Create template deployment

`createTemplateDeployment`
Create a deployment based on a template.

Use this endpoint with combination of [listTemplates](https://appwrite.io/docs/products/functions/templates) to find the template details.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `repository` | string | Yes | Repository name of the template. |
| `owner` | string | Yes | The name of the owner of the template. |
| `rootDirectory` | string | Yes | Path to function code in the template repo. |
| `type` | string | Yes | Type for the reference provided. Can be commit, branch, or tag |
| `reference` | string | Yes | Reference value, can be a commit hash, branch name, or release tag |
| `activate` | boolean | No | Automatically activate the deployment when it is finished building. |

**Response:** `deployment`

## Create VCS deployment

`createVcsDeployment`
Create a deployment when a function is connected to VCS.

This endpoint lets you create deployment from a branch, commit, or a tag.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `type` | string | Yes | Type of reference passed. Allowed values are: branch, commit |
| `reference` | string | Yes | VCS reference to create deployment from. Depending on type this can be: branch name, commit hash |
| `activate` | boolean | No | Automatically activate the deployment when it is finished building. |

**Response:** `deployment`

## Get deployment

`getDeployment`
Get a function deployment by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `deploymentId` | string | Yes | Deployment ID. |

**Response:** `deployment`

## Delete deployment

`deleteDeployment`
Delete a code deployment by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `deploymentId` | string | Yes | Deployment ID. |


## Get deployment download

`getDeploymentDownload`
Get a function deployment content by its unique ID. The endpoint response return with a &#039;Content-Disposition: attachment&#039; header that tells the browser to start downloading the file to user downloads directory.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `deploymentId` | string | Yes | Deployment ID. |
| `type` | string | No | Deployment file to download. Can be: &quot;source&quot;, &quot;output&quot;. (default: `source`) |


## Update deployment status

`updateDeploymentStatus`
Cancel an ongoing function deployment build. If the build is already in progress, it will be stopped and marked as canceled. If the build hasn&#039;t started yet, it will be marked as canceled without executing. You cannot cancel builds that have already completed (status &#039;ready&#039;) or failed. The response includes the final build status and details.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `deploymentId` | string | Yes | Deployment ID. |

**Response:** `deployment`

## List executions

`listExecutions`
Get a list of all the current user function execution logs. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: trigger, status, responseStatusCode, duration, requestMethod, requestPath, deploymentId (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `executionList`

## Create execution

`createExecution`
Trigger a function execution. The returned object will return you the current execution status. You can ping the `Get Execution` endpoint to get updates on the current execution status. Once this endpoint is called, your function execution process will start asynchronously.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `body` | string | No | HTTP body of execution. Default value is empty string. |
| `async` | boolean | No | Execute code in the background. Default value is false. |
| `path` | string | No | HTTP path of execution. Path can include query params. Default value is / (default: `/`) |
| `method` | string | No | HTTP method of execution. Default value is POST. (default: `POST`) |
| `headers` | object | No | HTTP headers of execution. Defaults to empty. (default: `{}`) |
| `scheduledAt` | string | No | Scheduled execution time in [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format. DateTime value must be in future with precision in minutes. |

**Response:** `execution`

## Get execution

`getExecution`
Get a function execution log by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `executionId` | string | Yes | Execution ID. |

**Response:** `execution`

## Delete execution

`deleteExecution`
Delete a function execution by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `executionId` | string | Yes | Execution ID. |


## Get function usage

`getUsage`
Get usage metrics and statistics for a for a specific function. View statistics including total deployments, builds, executions, storage usage, and compute time. The response includes both current totals and historical data for each metric. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, defaults to 30 days.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function ID. |
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageFunction`

## List variables

`listVariables`
Get a list of all variables of a specific function.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function unique ID. |

**Response:** `variableList`

## Create variable

`createVariable`
Create a new function environment variable. These variables can be accessed in the function at runtime as environment variables.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function unique ID. |
| `key` | string | Yes | Variable key. Max length: 255 chars. |
| `value` | string | Yes | Variable value. Max length: 8192 chars. |
| `secret` | boolean | No | Secret variables can be updated or deleted, but only functions can read them during build and runtime. (default: `1`) |

**Response:** `variable`

## Get variable

`getVariable`
Get a variable by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function unique ID. |
| `variableId` | string | Yes | Variable unique ID. |

**Response:** `variable`

## Update variable

`updateVariable`
Update variable by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function unique ID. |
| `variableId` | string | Yes | Variable unique ID. |
| `key` | string | Yes | Variable key. Max length: 255 chars. |
| `value` | string | No | Variable value. Max length: 8192 chars. |
| `secret` | boolean | No | Secret variables can be updated or deleted, but only functions can read them during build and runtime. |

**Response:** `variable`

## Delete variable

`deleteVariable`
Delete a variable by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `functionId` | string | Yes | Function unique ID. |
| `variableId` | string | Yes | Variable unique ID. |


