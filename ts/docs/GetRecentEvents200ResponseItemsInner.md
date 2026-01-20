
# GetRecentEvents200ResponseItemsInner

Each post item

## Properties

Name | Type
------------ | -------------
`eventId` | string
`blockType` | string
`author` | [GetRecentEvents200ResponseItemsInnerAuthor](GetRecentEvents200ResponseItemsInnerAuthor.md)
`media` | [Array&lt;Media&gt;](Media.md)
`floorUid` | string
`title` | string
`text` | string
`createdAtMs` | string
`blockId` | string

## Example

```typescript
import type { GetRecentEvents200ResponseItemsInner } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "eventId": null,
  "blockType": null,
  "author": null,
  "media": null,
  "floorUid": null,
  "title": null,
  "text": null,
  "createdAtMs": null,
  "blockId": null,
} satisfies GetRecentEvents200ResponseItemsInner

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as GetRecentEvents200ResponseItemsInner
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


