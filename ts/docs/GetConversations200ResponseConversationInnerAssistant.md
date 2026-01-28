
# GetConversations200ResponseConversationInnerAssistant


### Properties

Name | Type
------------ | -------------
`id` | string
`object` | string
`created` | number
`floorMode` | string
`model` | string
`choices` | [Array<GetConversations200ResponseConversationInnerAssistantChoicesInner>](GetConversations200ResponseConversationInnerAssistantChoicesInner.md)
`fetchMultiplePosts` | [GetConversations200ResponseConversationInnerAssistantFetchMultiplePosts](GetConversations200ResponseConversationInnerAssistantFetchMultiplePosts.md)
`contentType` | string

### Example

```typescript
import type { GetConversations200ResponseConversationInnerAssistant } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "id": null,
  "object": null,
  "created": null,
  "floorMode": null,
  "model": null,
  "choices": null,
  "fetchMultiplePosts": null,
  "contentType": null,
} satisfies GetConversations200ResponseConversationInnerAssistant

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as GetConversations200ResponseConversationInnerAssistant
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


