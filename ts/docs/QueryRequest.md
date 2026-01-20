
# QueryRequest


## Properties

Name | Type
------------ | -------------
`userId` | string
`query` | string
`floorIds` | Array&lt;string&gt;
`includeMetadata` | string
`summaryNeeded` | string
`appId` | string
`filters` | [QueryRequestFilters](QueryRequestFilters.md)

## Example

```typescript
import type { QueryRequest } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "userId": null,
  "query": null,
  "floorIds": null,
  "includeMetadata": null,
  "summaryNeeded": null,
  "appId": null,
  "filters": null,
} satisfies QueryRequest

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as QueryRequest
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


