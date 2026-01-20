
# UserDetails


## Properties

Name | Type
------------ | -------------
`podInfo` | [FloorInfo](FloorInfo.md)
`profile` | [SignInWithEmail200ResponseProfile](SignInWithEmail200ResponseProfile.md)
`appId` | string

## Example

```typescript
import type { UserDetails } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "podInfo": null,
  "profile": null,
  "appId": null,
} satisfies UserDetails

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as UserDetails
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


