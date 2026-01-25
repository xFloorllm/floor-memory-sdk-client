# GetRecentEvents400Response


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**error**

| [**GetRecentEvents400ResponseError**](GetRecentEvents400ResponseError.md) |
|

### Example

```python
from xfloor_memory_sdk.models.get_recent_events400_response import GetRecentEvents400Response

# TODO update the JSON string below
json = "{}"
# create an instance of GetRecentEvents400Response from a JSON string
get_recent_events400_response_instance = GetRecentEvents400Response.from_json(json)
# print the JSON string representation of the object
print(GetRecentEvents400Response.to_json())

# convert the object into a dict
get_recent_events400_response_dict = get_recent_events400_response_instance.to_dict()
# create an instance of GetRecentEvents400Response from a dict
get_recent_events400_response_from_dict = GetRecentEvents400Response.from_dict(get_recent_events400_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


