# Event400ResponseError


## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**code** | **str** |  | 
**message** | **str** | Invalid block type or Invalid Bid type | 
**path** | **str** |  | 
**timestamp** | **str** |  | 

## Example

```python
from xfloor_memory_sdk.models.event400_response_error import Event400ResponseError

# TODO update the JSON string below
json = "{}"
# create an instance of Event400ResponseError from a JSON string
event400_response_error_instance = Event400ResponseError.from_json(json)
# print the JSON string representation of the object
print(Event400ResponseError.to_json())

# convert the object into a dict
event400_response_error_dict = event400_response_error_instance.to_dict()
# create an instance of Event400ResponseError from a dict
event400_response_error_from_dict = Event400ResponseError.from_dict(event400_response_error_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


