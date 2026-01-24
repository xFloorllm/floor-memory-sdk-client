# Model400ErrorCode


### Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**code** | **str** | Validation Error | 
**message** | **str** | Error Message | 
**path** | **str** | REST api path | 
**timestamp** | **str** | Time stamp | 

### Example

```python
from xfloor_memory_sdk.models.model400_error_code import Model400ErrorCode

# TODO update the JSON string below
json = "{}"
# create an instance of Model400ErrorCode from a JSON string
model400_error_code_instance = Model400ErrorCode.from_json(json)
# print the JSON string representation of the object
print(Model400ErrorCode.to_json())

# convert the object into a dict
model400_error_code_dict = model400_error_code_instance.to_dict()
# create an instance of Model400ErrorCode from a dict
model400_error_code_from_dict = Model400ErrorCode.from_dict(model400_error_code_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


