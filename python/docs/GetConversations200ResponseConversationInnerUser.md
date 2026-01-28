# GetConversations200ResponseConversationInnerUser


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**context**

| [**GetConversations200ResponseConversationInnerUserContext**](GetConversations200ResponseConversationInnerUserContext.md) |
|
**user_query**

| **str** |
|
**user_id**

| **str** |
|
**user_thread**

| **str** |
|
**recorded_content**

| **str** |
|

### Example

```python
from xfloor_memory_sdk.models.get_conversations200_response_conversation_inner_user import GetConversations200ResponseConversationInnerUser

# TODO update the JSON string below
json = "{}"
# create an instance of GetConversations200ResponseConversationInnerUser from a JSON string
get_conversations200_response_conversation_inner_user_instance = GetConversations200ResponseConversationInnerUser.from_json(json)
# print the JSON string representation of the object
print(GetConversations200ResponseConversationInnerUser.to_json())

# convert the object into a dict
get_conversations200_response_conversation_inner_user_dict = get_conversations200_response_conversation_inner_user_instance.to_dict()
# create an instance of GetConversations200ResponseConversationInnerUser from a dict
get_conversations200_response_conversation_inner_user_from_dict = GetConversations200ResponseConversationInnerUser.from_dict(get_conversations200_response_conversation_inner_user_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


