
# GetConversations200ResponseConversationInnerUser


### Properties

Name | Type
------------ | -------------
`context` | [GetConversations200ResponseConversationInnerUserContext](GetConversations200ResponseConversationInnerUserContext.md)
`userQuery` | string
`userId` | string
`userThread` | string
`recordedContent` | string

### Example

```typescript
import type { GetConversations200ResponseConversationInnerUser } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "context": null,
  "userQuery": null,
  "userId": null,
  "userThread": null,
  "recordedContent": null,
} satisfies GetConversations200ResponseConversationInnerUser

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as GetConversations200ResponseConversationInnerUser
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


