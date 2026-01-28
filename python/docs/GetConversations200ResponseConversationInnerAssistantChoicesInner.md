# GetConversations200ResponseConversationInnerAssistantChoicesInner


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**index**

| **int** |
|

[optional]
**message**

| [**GetConversations200ResponseConversationInnerAssistantChoicesInnerMessage**](GetConversations200ResponseConversationInnerAssistantChoicesInnerMessage.md) |
|

[optional]
**finish_reason**

| **str** |
|

[optional]
**ai_model_details**

| [**GetConversations200ResponseConversationInnerAssistantChoicesInnerAiModelDetails**](GetConversations200ResponseConversationInnerAssistantChoicesInnerAiModelDetails.md) |
|

[optional]
**prompt_details**

| [**GetConversations200ResponseConversationInnerAssistantChoicesInnerPromptDetails**](GetConversations200ResponseConversationInnerAssistantChoicesInnerPromptDetails.md) |
|

[optional]

### Example

```python
from xfloor_memory_sdk.models.get_conversations200_response_conversation_inner_assistant_choices_inner import GetConversations200ResponseConversationInnerAssistantChoicesInner

# TODO update the JSON string below
json = "{}"
# create an instance of GetConversations200ResponseConversationInnerAssistantChoicesInner from a JSON string
get_conversations200_response_conversation_inner_assistant_choices_inner_instance = GetConversations200ResponseConversationInnerAssistantChoicesInner.from_json(json)
# print the JSON string representation of the object
print(GetConversations200ResponseConversationInnerAssistantChoicesInner.to_json())

# convert the object into a dict
get_conversations200_response_conversation_inner_assistant_choices_inner_dict = get_conversations200_response_conversation_inner_assistant_choices_inner_instance.to_dict()
# create an instance of GetConversations200ResponseConversationInnerAssistantChoicesInner from a dict
get_conversations200_response_conversation_inner_assistant_choices_inner_from_dict = GetConversations200ResponseConversationInnerAssistantChoicesInner.from_dict(get_conversations200_response_conversation_inner_assistant_choices_inner_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


