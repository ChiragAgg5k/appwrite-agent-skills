# Proxy

The Proxy Service allows you to configure actions for your domains beyond DNS configuration.

## List rules

`listRules`
Get a list of all the proxy rules. You can use the query params to filter your results.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `queries` | array\<string\> | No | Array of query strings generated using the Query class provided by the SDK. [Learn more about queries](https://appwrite.io/docs/databases#querying-documents). Maximum of 100 queries are allowed, each 4096 characters long. You may filter on the following attributes: domain, type, trigger, deploymentResourceType, deploymentResourceId, deploymentId, deploymentVcsProviderBranch (default: `[]`) |
| `search` | string | No | Search term to filter your list results. Max length: 256 chars. |
| `total` | boolean | No | When set to false, the total count returned will be 0 and will not be calculated. (default: `1`) |

**Response:** `proxyRuleList`

## Create API rule

`createAPIRule`
Create a new proxy rule for serving Appwrite&#039;s API on custom domain.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `domain` | string | Yes | Domain name. |

**Response:** `proxyRule`

## Create function rule

`createFunctionRule`
Create a new proxy rule for executing Appwrite Function on custom domain.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `domain` | string | Yes | Domain name. |
| `functionId` | string | Yes | ID of function to be executed. |
| `branch` | string | No | Name of VCS branch to deploy changes automatically |

**Response:** `proxyRule`

## Create Redirect rule

`createRedirectRule`
Create a new proxy rule for to redirect from custom domain to another domain.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `domain` | string | Yes | Domain name. |
| `url` | string | Yes | Target URL of redirection |
| `statusCode` | string | Yes | Status code of redirection |
| `resourceId` | string | Yes | ID of parent resource. |
| `resourceType` | string | Yes | Type of parent resource. |

**Response:** `proxyRule`

## Create site rule

`createSiteRule`
Create a new proxy rule for serving Appwrite Site on custom domain.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `domain` | string | Yes | Domain name. |
| `siteId` | string | Yes | ID of site to be executed. |
| `branch` | string | No | Name of VCS branch to deploy changes automatically |

**Response:** `proxyRule`

## Get rule

`getRule`
Get a proxy rule by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `ruleId` | string | Yes | Rule ID. |

**Response:** `proxyRule`

## Delete rule

`deleteRule`
Delete a proxy rule by its unique ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `ruleId` | string | Yes | Rule ID. |


## Update rule verification status

`updateRuleVerification`
Retry getting verification process of a proxy rule. This endpoint triggers domain verification by checking DNS records (CNAME) against the configured target domain. If verification is successful, a TLS certificate will be automatically provisioned for the domain.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `ruleId` | string | Yes | Rule ID. |

**Response:** `proxyRule`

