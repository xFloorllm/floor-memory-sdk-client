# GetConversations200ResponseConversationInnerAssistantFetchMultiplePosts


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**content_type**

| **str** |
|
**query**

| **str** |
|
**status**

| **str** |
|
**message**

| **str** |
|
**results**

| [**List[GetConversations200ResponseConversationInnerAssistantFetchMultiplePostsResultsInner]**](GetConversations200ResponseConversationInnerAssistantFetchMultiplePostsResultsInner.md) |
|

### Example

```python
from xfloor_memory_sdk.models.get_conversations200_response_conversation_inner_assistant_fetch_multiple_posts import GetConversations200ResponseConversationInnerAssistantFetchMultiplePosts

# TODO update the JSON string below
json = "{}"
# create an instance of GetConversations200ResponseConversationInnerAssistantFetchMultiplePosts from a JSON string
get_conversations200_response_conversation_inner_assistant_fetch_multiple_posts_instance = GetConversations200ResponseConversationInnerAssistantFetchMultiplePosts.from_json(json)
# print the JSON string representation of the object
print(GetConversations200ResponseConversationInnerAssistantFetchMultiplePosts.to_json())

# convert the object into a dict
get_conversations200_response_conversation_inner_assistant_fetch_multiple_posts_dict = get_conversations200_response_conversation_inner_assistant_fetch_multiple_posts_instance.to_dict()
# create an instance of GetConversations200ResponseConversationInnerAssistantFetchMultiplePosts from a dict
get_conversations200_response_conversation_inner_assistant_fetch_multiple_posts_from_dict = GetConversations200ResponseConversationInnerAssistantFetchMultiplePosts.from_dict(get_conversations200_response_conversation_inner_assistant_fetch_multiple_posts_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


