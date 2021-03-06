{{{
  "title": "Delete Anti-Affinity Policy",
  "date": "11-20-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Deletes a given anti-affinity policy by ID. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to delete a specific anti-affinity policy within a given account.

## URL

### Structure

    DELETE https://api.ctl.io/v2/antiAffinityPolicies/{accountAlias}/{policyId}

### Example

    DELETE https://api.ctl.io/v2/antiAffinityPolicies/ALIAS/80a7bf90b199454b859399bff54f4173

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |
| PolicyId | string | ID of the anti-affinity policy being queried. | Yes |

## Response

The response will not contain JSON content, but should return the HTTP `204 No Content` response upon deletion of the policy.
