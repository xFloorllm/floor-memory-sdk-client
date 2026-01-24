
# SignInWithEmail200ResponseProfile

User profile details

### Properties

Name | Type
------------ | -------------
`floorId` | string
`fid` | string
`blocks` | [Array&lt;BlockDetails&gt;](BlockDetails.md)
`name` | string
`email` | string
`mobileNumber` | string
`userId` | string
`avatar` | [SignInWithEmail200ResponseProfileAvatar](SignInWithEmail200ResponseProfileAvatar.md)

### Example

```typescript
import type { SignInWithEmail200ResponseProfile } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "floorId": null,
  "fid": null,
  "blocks": null,
  "name": null,
  "email": null,
  "mobileNumber": null,
  "userId": null,
  "avatar": null,
} satisfies SignInWithEmail200ResponseProfile

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SignInWithEmail200ResponseProfile
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


