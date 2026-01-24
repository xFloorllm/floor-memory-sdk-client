# SendValidationCodeRequest


### Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**user_id** | **str** | user id | [optional] 
**mode** | **str** | Mode - 0 for getting activation code to change email or mobile number, 1 for password change | 
**mobiles_number** | **str** |  | [optional] 
**email_id** | **str** |  | [optional] 

### Example

```python
from xfloor_memory_sdk.models.send_validation_code_request import SendValidationCodeRequest

# TODO update the JSON string below
json = "{}"
# create an instance of SendValidationCodeRequest from a JSON string
send_validation_code_request_instance = SendValidationCodeRequest.from_json(json)
# print the JSON string representation of the object
print(SendValidationCodeRequest.to_json())

# convert the object into a dict
send_validation_code_request_dict = send_validation_code_request_instance.to_dict()
# create an instance of SendValidationCodeRequest from a dict
send_validation_code_request_from_dict = SendValidationCodeRequest.from_dict(send_validation_code_request_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


