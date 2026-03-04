
# SignInResponse


### Properties

Name | Type
------------ | -------------
`profile` | [ChangeEmail200ResponseProfile](ChangeEmail200ResponseProfile.md)
`podInfo` | [ChangeEmail200ResponsePodInfo](ChangeEmail200ResponsePodInfo.md)
`appId` | string

### Example

```typescript
import type { SignInResponse } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "profile": null,
  "podInfo": null,
  "appId": null,
} satisfies SignInResponse

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SignInResponse
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


