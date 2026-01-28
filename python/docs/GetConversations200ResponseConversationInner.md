# GetConversations200ResponseConversationInner


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**user**

| [**GetConversations200ResponseConversationInnerUser**](GetConversations200ResponseConversationInnerUser.md) |
|

[optional]
**assistant**

| [**GetConversations200ResponseConversationInnerAssistant**](GetConversations200ResponseConversationInnerAssistant.md) |
|

[optional]

### Example

```python
from xfloor_memory_sdk.models.get_conversations200_response_conversation_inner import GetConversations200ResponseConversationInner

# TODO update the JSON string below
json = "{}"
# create an instance of GetConversations200ResponseConversationInner from a JSON string
get_conversations200_response_conversation_inner_instance = GetConversations200ResponseConversationInner.from_json(json)
# print the JSON string representation of the object
print(GetConversations200ResponseConversationInner.to_json())

# convert the object into a dict
get_conversations200_response_conversation_inner_dict = get_conversations200_response_conversation_inner_instance.to_dict()
# create an instance of GetConversations200ResponseConversationInner from a dict
get_conversations200_response_conversation_inner_from_dict = GetConversations200ResponseConversationInner.from_dict(get_conversations200_response_conversation_inner_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


