
# BlockDetails

Block Details

### Properties

Name | Type
------------ | -------------
`blockId` | string
`type` | string
`title` | string

### Example

```typescript
import type { BlockDetails } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "blockId": null,
  "type": null,
  "title": null,
} satisfies BlockDetails

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as BlockDetails
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


