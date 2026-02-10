# Console

The Console service allows you to interact with console relevant information.

## Check resource ID availability

`getResource`
Check if a resource ID is available.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `value` | string | Yes | Resource value. |
| `type` | string | Yes | Resource type. |


## Get variables

`variables`
Get all Environment Variables that are relevant for the console.


**Response:** `consoleVariables`

