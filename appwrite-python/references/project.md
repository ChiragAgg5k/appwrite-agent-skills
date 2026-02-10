# Project

The Project service allows you to manage all the projects in your Appwrite server.

## Get project usage stats

`getUsage`
Get comprehensive usage statistics for your project. View metrics including network requests, bandwidth, storage, function executions, database usage, and user activity. Specify a time range with startDate and endDate, and optionally set the data granularity with period (1h or 1d). The response includes both total counts and detailed breakdowns by resource, along with historical data over the specified period.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `startDate` | string | Yes | Starting date for the usage |
| `endDate` | string | Yes | End date for the usage |
| `period` | string | No | Period used (default: `1d`) |

**Response:** `usageProject`

## List variables

`listVariables`
Get a list of all project variables. These variables will be accessible in all Appwrite Functions at runtime.


**Response:** `variableList`

## Create variable

`createVariable`
Create a new project variable. This variable will be accessible in all Appwrite Functions at runtime.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `key` | string | Yes | Variable key. Max length: 255 chars. |
| `value` | string | Yes | Variable value. Max length: 8192 chars. |
| `secret` | boolean | No | Secret variables can be updated or deleted, but only projects can read them during build and runtime. (default: `1`) |

**Response:** `variable`

## Get variable

`getVariable`
Get a project variable by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `variableId` | string | Yes | Variable unique ID. |

**Response:** `variable`

## Update variable

`updateVariable`
Update project variable by its unique ID. This variable will be accessible in all Appwrite Functions at runtime.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `variableId` | string | Yes | Variable unique ID. |
| `key` | string | Yes | Variable key. Max length: 255 chars. |
| `value` | string | No | Variable value. Max length: 8192 chars. |
| `secret` | boolean | No | Secret variables can be updated or deleted, but only projects can read them during build and runtime. |

**Response:** `variable`

## Delete variable

`deleteVariable`
Delete a project variable by its unique ID. 

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `variableId` | string | Yes | Variable unique ID. |


