# Event400Response


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**error**

| [**Event400ResponseError**](Event400ResponseError.md) |
|

### Example

```python
from xfloor_memory_sdk.models.event400_response import Event400Response

# TODO update the JSON string below
json = "{}"
# create an instance of Event400Response from a JSON string
event400_response_instance = Event400Response.from_json(json)
# print the JSON string representation of the object
print(Event400Response.to_json())

# convert the object into a dict
event400_response_dict = event400_response_instance.to_dict()
# create an instance of Event400Response from a dict
event400_response_from_dict = Event400Response.from_dict(event400_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


