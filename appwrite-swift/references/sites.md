# Sites

The Sites Service allows you view, create and manage your web applications.

## List sites

`list`
Get a list of all the project&#039;s sites. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: name, enabled, framework, deploymentId, buildCommand, installCommand, outputDirectory, installationId (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `siteList`

## Create site

`create`
Create a new site.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. Choose a custom ID or generate a random ID with `ID.unique()`. Valid chars are a-z, A-Z, 0-9, period, hyphen, and underscore. Can&#039;t start with a special char. Max length is 36 chars. |
| `name` | string | Yes | Site name. Max length: 128 chars. |
| `framework` | string | Yes | Sites framework. |
| `buildRuntime` | string | Yes | Runtime to use during build step. |
| `enabled` | boolean | No | Is site enabled? When set to &#039;disabled&#039;, users cannot access the site but Server SDKs with and API key can still access the site. No data is lost when this is toggled. (default: `1`) |
| `logging` | boolean | No | When disabled, request logs will exclude logs and errors, and site responses will be slightly faster. (default: `1`) |
| `timeout` | integer | No | Maximum request time in seconds. (default: `30`) |
| `installCommand` | string | No | Install Command. |
| `buildCommand` | string | No | Build Command. |
| `outputDirectory` | string | No | Output Directory for site. |
| `adapter` | string | No | Framework adapter defining rendering strategy. Allowed values are: static, ssr |
| `installationId` | string | No | Appwrite Installation ID for VCS (Version Control System) deployment. |
| `fallbackFile` | string | No | Fallback file for single page application sites. |
| `providerRepositoryId` | string | No | Repository ID of the repo linked to the site. |
| `providerBranch` | string | No | Production branch for the repo linked to the site. |
| `providerSilentMode` | boolean | No | Is the VCS (Version Control System) connection in silent mode for the repo linked to the site? In silent mode, comments will not be made on commits and pull requests. |
| `providerRootDirectory` | string | No | Path to site code in the linked repo. |
| `specification` | string | No | Framework specification for the site and builds. (default: `[]`) |

**Response:** `site`

## List frameworks

`listFrameworks`
Get a list of all frameworks that are currently available on the server instance.


**Response:** `frameworkList`

## List specifications

`listSpecifications`
List allowed site specifications for this instance.


**Response:** `specificationList`

## List templates

`listTemplates`
List available site templates. You can use template details in [createSite](/docs/references/cloud/server-nodejs/sites#create) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `frameworks` | array\<string\> | No | List of frameworks allowed for filtering site templates. Maximum of 100 frameworks are allowed. (default: `[]`) |
| `useCases` | array\<string\> | No | List of use cases allowed for filtering site templates. Maximum of 100 use cases are allowed. (default: `[]`) |
| `limit` | integer | No | Limit the number of templates returned in the response. Default limit is 25, and maximum limit is 5000. (default: `25`) |
| `offset` | integer | No | Offset the list of returned templates. Maximum offset is 5000. (default: `0`) |

**Response:** `templateSiteList`

## Get site template

`getTemplate`
Get a site template using ID. You can use template details in [createSite](/docs/references/cloud/server-nodejs/sites#create) method.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `templateId` | string | Yes | Template ID. |

**Response:** `templateSite`

## Get sites usage

`listUsage`
Get usage metrics and statistics for all sites in the project. View statistics including total deployments, builds, logs, storage usage, and compute time. The response includes both current totals and historical data for each metric. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, defaults to 30 days.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageSites`

## Get site

`get`
Get a site by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |

**Response:** `site`

## Update site

`update`
Update site by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `name` | string | Yes | Site name. Max length: 128 chars. |
| `framework` | string | Yes | Sites framework. |
| `enabled` | boolean | No | Is site enabled? When set to &#039;disabled&#039;, users cannot access the site but Server SDKs with and API key can still access the site. No data is lost when this is toggled. (default: `1`) |
| `logging` | boolean | No | When disabled, request logs will exclude logs and errors, and site responses will be slightly faster. (default: `1`) |
| `timeout` | integer | No | Maximum request time in seconds. (default: `30`) |
| `installCommand` | string | No | Install Command. |
| `buildCommand` | string | No | Build Command. |
| `outputDirectory` | string | No | Output Directory for site. |
| `buildRuntime` | string | No | Runtime to use during build step. |
| `adapter` | string | No | Framework adapter defining rendering strategy. Allowed values are: static, ssr |
| `fallbackFile` | string | No | Fallback file for single page application sites. |
| `installationId` | string | No | Appwrite Installation ID for VCS (Version Control System) deployment. |
| `providerRepositoryId` | string | No | Repository ID of the repo linked to the site. |
| `providerBranch` | string | No | Production branch for the repo linked to the site. |
| `providerSilentMode` | boolean | No | Is the VCS (Version Control System) connection in silent mode for the repo linked to the site? In silent mode, comments will not be made on commits and pull requests. |
| `providerRootDirectory` | string | No | Path to site code in the linked repo. |
| `specification` | string | No | Framework specification for the site and builds. (default: `[]`) |

**Response:** `site`

## Delete site

`delete`
Delete a site by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |


## Update site&#039;s deployment

`updateSiteDeployment`
Update the site active deployment. Use this endpoint to switch the code deployment that should be used when visitor opens your site.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `deploymentId` | string | Yes | Deployment ID. |

**Response:** `site`

## List deployments

`listDeployments`
Get a list of all the site&#039;s code deployments. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: buildSize, sourceSize, totalSize, buildDuration, status, activate, type (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `deploymentList`

## Create deployment

`createDeployment`
Create a new site code deployment. Use this endpoint to upload a new version of your site code. To activate your newly uploaded code, you&#039;ll need to update the site&#039;s deployment to use your new deployment ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `code` | file | Yes | Gzip file with your code package. When used with the Appwrite CLI, pass the path to your code directory, and the CLI will automatically package your code. Use a path that is within the current directory. |
| `activate` | boolean | Yes | Automatically activate the deployment when it is finished building. |
| `installCommand` | string | No | Install Commands. |
| `buildCommand` | string | No | Build Commands. |
| `outputDirectory` | string | No | Output Directory. |

**Response:** `deployment`

## Create duplicate deployment

`createDuplicateDeployment`
Create a new build for an existing site deployment. This endpoint allows you to rebuild a deployment with the updated site configuration, including its commands and output directory if they have been modified. The build process will be queued and executed asynchronously. The original deployment&#039;s code will be preserved and used for the new build.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `deploymentId` | string | Yes | Deployment ID. |

**Response:** `deployment`

## Create template deployment

`createTemplateDeployment`
Create a deployment based on a template.

Use this endpoint with combination of [listTemplates](https://appwrite.io/docs/products/sites/templates) to find the template details.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `repository` | string | Yes | Repository name of the template. |
| `owner` | string | Yes | The name of the owner of the template. |
| `rootDirectory` | string | Yes | Path to site code in the template repo. |
| `type` | string | Yes | Type for the reference provided. Can be commit, branch, or tag |
| `reference` | string | Yes | Reference value, can be a commit hash, branch name, or release tag |
| `activate` | boolean | No | Automatically activate the deployment when it is finished building. |

**Response:** `deployment`

## Create VCS deployment

`createVcsDeployment`
Create a deployment when a site is connected to VCS.

This endpoint lets you create deployment from a branch, commit, or a tag.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `type` | string | Yes | Type of reference passed. Allowed values are: branch, commit |
| `reference` | string | Yes | VCS reference to create deployment from. Depending on type this can be: branch name, commit hash |
| `activate` | boolean | No | Automatically activate the deployment when it is finished building. |

**Response:** `deployment`

## Get deployment

`getDeployment`
Get a site deployment by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `deploymentId` | string | Yes | Deployment ID. |

**Response:** `deployment`

## Delete deployment

`deleteDeployment`
Delete a site deployment by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `deploymentId` | string | Yes | Deployment ID. |


## Get deployment download

`getDeploymentDownload`
Get a site deployment content by its unique ID. The endpoint response return with a &#039;Content-Disposition: attachment&#039; header that tells the browser to start downloading the file to user downloads directory.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `deploymentId` | string | Yes | Deployment ID. |
| `type` | string | No | Deployment file to download. Can be: &quot;source&quot;, &quot;output&quot;. (default: `source`) |


## Update deployment status

`updateDeploymentStatus`
Cancel an ongoing site deployment build. If the build is already in progress, it will be stopped and marked as canceled. If the build hasn&#039;t started yet, it will be marked as canceled without executing. You cannot cancel builds that have already completed (status &#039;ready&#039;) or failed. The response includes the final build status and details.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `deploymentId` | string | Yes | Deployment ID. |

**Response:** `deployment`

## List logs

`listLogs`
Get a list of all site logs. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/queries). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: trigger, status, responseStatusCode, duration, requestMethod, requestPath, deploymentId (default: `[]`) |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `executionList`

## Get log

`getLog`
Get a site request log by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `logId` | string | Yes | Log ID. |

**Response:** `execution`

## Delete log

`deleteLog`
Delete a site log by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `logId` | string | Yes | Log ID. |


## Get site usage

`getUsage`
Get usage metrics and statistics for a for a specific site. View statistics including total deployments, builds, executions, storage usage, and compute time. The response includes both current totals and historical data for each metric. Use the optional range parameter to specify the time window for historical data: 24h (last 24 hours), 30d (last 30 days), or 90d (last 90 days). If not specified, defaults to 30 days.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site ID. |
| `range` | string | No | Date range. (default: `30d`) |

**Response:** `usageSite`

## List variables

`listVariables`
Get a list of all variables of a specific site.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site unique ID. |

**Response:** `variableList`

## Create variable

`createVariable`
Create a new site variable. These variables can be accessed during build and runtime (server-side rendering) as environment variables.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site unique ID. |
| `key` | string | Yes | Variable key. Max length: 255 chars. |
| `value` | string | Yes | Variable value. Max length: 8192 chars. |
| `secret` | boolean | No | Secret variables can be updated or deleted, but only sites can read them during build and runtime. (default: `1`) |

**Response:** `variable`

## Get variable

`getVariable`
Get a variable by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site unique ID. |
| `variableId` | string | Yes | Variable unique ID. |

**Response:** `variable`

## Update variable

`updateVariable`
Update variable by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site unique ID. |
| `variableId` | string | Yes | Variable unique ID. |
| `key` | string | Yes | Variable key. Max length: 255 chars. |
| `value` | string | No | Variable value. Max length: 8192 chars. |
| `secret` | boolean | No | Secret variables can be updated or deleted, but only sites can read them during build and runtime. |

**Response:** `variable`

## Delete variable

`deleteVariable`
Delete a variable by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `siteId` | string | Yes | Site unique ID. |
| `variableId` | string | Yes | Variable unique ID. |


