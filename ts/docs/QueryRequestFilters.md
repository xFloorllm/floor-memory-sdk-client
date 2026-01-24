
# QueryRequestFilters

JSON format filters

### Properties

Name | Type
------------ | -------------
`timeFrom` | string
`timeTo` | string
`filterTypes` | string
`filterTags` | string

### Example

```typescript
import type { QueryRequestFilters } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "timeFrom": null,
  "timeTo": null,
  "filterTypes": null,
  "filterTags": null,
} satisfies QueryRequestFilters

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as QueryRequestFilters
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


