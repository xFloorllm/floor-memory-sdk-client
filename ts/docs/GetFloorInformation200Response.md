
# GetFloorInformation200Response


### Properties

Name | Type
------------ | -------------
`floorId` | string
`title` | string
`details` | string
`floorUid` | string
`blocks` | [Array&lt;BlockDetails&gt;](BlockDetails.md)
`avatar` | [Media](Media.md)
`isOwner` | string
`floorType` | string

### Example

```typescript
import type { GetFloorInformation200Response } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "floorId": null,
  "title": null,
  "details": null,
  "floorUid": null,
  "blocks": null,
  "avatar": null,
  "isOwner": null,
  "floorType": null,
} satisfies GetFloorInformation200Response

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as GetFloorInformation200Response
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


