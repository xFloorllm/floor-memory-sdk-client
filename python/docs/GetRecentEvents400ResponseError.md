# GetRecentEvents400ResponseError


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**code**

| **str** |
|
**message**

| **str** |
|
**path**

| **str** |
|
**timestamp**

| **str** |
|

### Example

```python
from xfloor_memory_sdk.models.get_recent_events400_response_error import GetRecentEvents400ResponseError

# TODO update the JSON string below
json = "{}"
# create an instance of GetRecentEvents400ResponseError from a JSON string
get_recent_events400_response_error_instance = GetRecentEvents400ResponseError.from_json(json)
# print the JSON string representation of the object
print(GetRecentEvents400ResponseError.to_json())

# convert the object into a dict
get_recent_events400_response_error_dict = get_recent_events400_response_error_instance.to_dict()
# create an instance of GetRecentEvents400ResponseError from a dict
get_recent_events400_response_error_from_dict = GetRecentEvents400ResponseError.from_dict(get_recent_events400_response_error_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


