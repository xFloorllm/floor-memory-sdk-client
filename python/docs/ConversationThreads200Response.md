# ConversationThreads200Response


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**user_id**

| **str** |
|
**threads**

| [**List[ConversationThreads200ResponseThreadsInner]**](ConversationThreads200ResponseThreadsInner.md) |
|

### Example

```python
from xfloor_memory_sdk.models.conversation_threads200_response import ConversationThreads200Response

# TODO update the JSON string below
json = "{}"
# create an instance of ConversationThreads200Response from a JSON string
conversation_threads200_response_instance = ConversationThreads200Response.from_json(json)
# print the JSON string representation of the object
print(ConversationThreads200Response.to_json())

# convert the object into a dict
conversation_threads200_response_dict = conversation_threads200_response_instance.to_dict()
# create an instance of ConversationThreads200Response from a dict
conversation_threads200_response_from_dict = ConversationThreads200Response.from_dict(conversation_threads200_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


