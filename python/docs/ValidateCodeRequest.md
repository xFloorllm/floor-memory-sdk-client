# ValidateCodeRequest


## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**user_id** | **str** | User ID | 
**activation_code** | **str** | Validation code | 
**app_id** | **str** | App ID which is given while registering as developer | 
**mode** | **str** | 4 for sign up, 5 for login | 

## Example

```python
from xfloor_memory_sdk.models.validate_code_request import ValidateCodeRequest

# TODO update the JSON string below
json = "{}"
# create an instance of ValidateCodeRequest from a JSON string
validate_code_request_instance = ValidateCodeRequest.from_json(json)
# print the JSON string representation of the object
print(ValidateCodeRequest.to_json())

# convert the object into a dict
validate_code_request_dict = validate_code_request_instance.to_dict()
# create an instance of ValidateCodeRequest from a dict
validate_code_request_from_dict = ValidateCodeRequest.from_dict(validate_code_request_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


