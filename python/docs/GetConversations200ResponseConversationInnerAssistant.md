# GetConversations200ResponseConversationInnerAssistant


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**id**

| **str** |
|
**object**

| **str** |
|
**created**

| **int** |
|
**floor_mode**

| **str** |
|
**model**

| **str** |
|
**choices**

| [**List[GetConversations200ResponseConversationInnerAssistantChoicesInner]**](GetConversations200ResponseConversationInnerAssistantChoicesInner.md) |
|
**fetch_multiple_posts**

| [**GetConversations200ResponseConversationInnerAssistantFetchMultiplePosts**](GetConversations200ResponseConversationInnerAssistantFetchMultiplePosts.md) |
|
**content_type**

| **str** |
|

### Example

```python
from xfloor_memory_sdk.models.get_conversations200_response_conversation_inner_assistant import GetConversations200ResponseConversationInnerAssistant

# TODO update the JSON string below
json = "{}"
# create an instance of GetConversations200ResponseConversationInnerAssistant from a JSON string
get_conversations200_response_conversation_inner_assistant_instance = GetConversations200ResponseConversationInnerAssistant.from_json(json)
# print the JSON string representation of the object
print(GetConversations200ResponseConversationInnerAssistant.to_json())

# convert the object into a dict
get_conversations200_response_conversation_inner_assistant_dict = get_conversations200_response_conversation_inner_assistant_instance.to_dict()
# create an instance of GetConversations200ResponseConversationInnerAssistant from a dict
get_conversations200_response_conversation_inner_assistant_from_dict = GetConversations200ResponseConversationInnerAssistant.from_dict(get_conversations200_response_conversation_inner_assistant_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


