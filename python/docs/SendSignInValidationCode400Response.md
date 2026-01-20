# SendSignInValidationCode400Response


## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**code** | **str** | Validation Error | 
**message** | **str** | Error Message | 
**path** | **str** | REST api path | 
**timestamp** | **str** | Time stamp | 

## Example

```python
from xfloor_memory_sdk.models.send_sign_in_validation_code400_response import SendSignInValidationCode400Response

# TODO update the JSON string below
json = "{}"
# create an instance of SendSignInValidationCode400Response from a JSON string
send_sign_in_validation_code400_response_instance = SendSignInValidationCode400Response.from_json(json)
# print the JSON string representation of the object
print(SendSignInValidationCode400Response.to_json())

# convert the object into a dict
send_sign_in_validation_code400_response_dict = send_sign_in_validation_code400_response_instance.to_dict()
# create an instance of SendSignInValidationCode400Response from a dict
send_sign_in_validation_code400_response_from_dict = SendSignInValidationCode400Response.from_dict(send_sign_in_validation_code400_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


