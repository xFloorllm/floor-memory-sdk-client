# ValidateCode400Response


## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**error** | [**ValidateCode400ResponseError**](ValidateCode400ResponseError.md) |  | 

## Example

```python
from xfloor_memory_sdk.models.validate_code400_response import ValidateCode400Response

# TODO update the JSON string below
json = "{}"
# create an instance of ValidateCode400Response from a JSON string
validate_code400_response_instance = ValidateCode400Response.from_json(json)
# print the JSON string representation of the object
print(ValidateCode400Response.to_json())

# convert the object into a dict
validate_code400_response_dict = validate_code400_response_instance.to_dict()
# create an instance of ValidateCode400Response from a dict
validate_code400_response_from_dict = ValidateCode400Response.from_dict(validate_code400_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


