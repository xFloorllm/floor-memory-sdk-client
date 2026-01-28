
# PostAdd


### Properties

Name | Type
------------ | -------------
`floorId` | string
`bID` | string
`userId` | string
`title` | string
`description` | string

### Example

```typescript
import type { PostAdd } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "floorId": null,
  "bID": null,
  "userId": null,
  "title": null,
  "description": null,
} satisfies PostAdd

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as PostAdd
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


