
# FloorInfo

User\'s Pod floor Infomation

### Properties

Name | Type
------------ | -------------
`floorId` | string
`title` | string
`details` | string
`fid` | string
`blocks` | [Array&lt;BlockDetails&gt;](BlockDetails.md)
`avatar` | [Media](Media.md)

### Example

```typescript
import type { FloorInfo } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "floorId": null,
  "title": null,
  "details": null,
  "fid": null,
  "blocks": null,
  "avatar": null,
} satisfies FloorInfo

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as FloorInfo
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


