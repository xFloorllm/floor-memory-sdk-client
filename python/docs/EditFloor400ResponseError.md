# EditFloor400ResponseError


### Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**code** | **str** | Error code | 
**message** | **str** | Error message | 
**path** | **str** | API path | 
**timestamp** | **str** | Time stamp | 

### Example

```python
from xfloor_memory_sdk.models.edit_floor400_response_error import EditFloor400ResponseError

# TODO update the JSON string below
json = "{}"
# create an instance of EditFloor400ResponseError from a JSON string
edit_floor400_response_error_instance = EditFloor400ResponseError.from_json(json)
# print the JSON string representation of the object
print(EditFloor400ResponseError.to_json())

# convert the object into a dict
edit_floor400_response_error_dict = edit_floor400_response_error_instance.to_dict()
# create an instance of EditFloor400ResponseError from a dict
edit_floor400_response_error_from_dict = EditFloor400ResponseError.from_dict(edit_floor400_response_error_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


