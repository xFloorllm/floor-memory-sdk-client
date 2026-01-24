
# QueryResponseItemsInner

Each item description

### Properties

Name | Type
------------ | -------------
`blockType` | number
`blockId` | string
`floorUid` | string
`eventId` | string
`text` | string
`score` | number
`blockTitle` | string
`blockDetails` | string
`fromFloorUid` | string
`userId` | string
`matchType` | string

### Example

```typescript
import type { QueryResponseItemsInner } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "blockType": null,
  "blockId": null,
  "floorUid": null,
  "eventId": null,
  "text": null,
  "score": null,
  "blockTitle": null,
  "blockDetails": null,
  "fromFloorUid": null,
  "userId": null,
  "matchType": null,
} satisfies QueryResponseItemsInner

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as QueryResponseItemsInner
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


