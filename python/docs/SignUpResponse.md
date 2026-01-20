# SignUpResponse


## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**user_id** | **str** | User ID | 
**success** | **str** | Success string - \&quot;Enter Validation code\&quot; | 

## Example

```python
from xfloor_memory_sdk.models.sign_up_response import SignUpResponse

# TODO update the JSON string below
json = "{}"
# create an instance of SignUpResponse from a JSON string
sign_up_response_instance = SignUpResponse.from_json(json)
# print the JSON string representation of the object
print(SignUpResponse.to_json())

# convert the object into a dict
sign_up_response_dict = sign_up_response_instance.to_dict()
# create an instance of SignUpResponse from a dict
sign_up_response_from_dict = SignUpResponse.from_dict(sign_up_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


