# SendSignInValidationCode200Response


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**success**

| **str** | Operation successful |
**mobile_number**

| **str** | Mobile number if signed in through mobile number |

[optional]
**email_id**

| **str** | Email ID if signed through email |

### Example

```python
from xfloor_memory_sdk.models.send_sign_in_validation_code200_response import SendSignInValidationCode200Response

# TODO update the JSON string below
json = "{}"
# create an instance of SendSignInValidationCode200Response from a JSON string
send_sign_in_validation_code200_response_instance = SendSignInValidationCode200Response.from_json(json)
# print the JSON string representation of the object
print(SendSignInValidationCode200Response.to_json())

# convert the object into a dict
send_sign_in_validation_code200_response_dict = send_sign_in_validation_code200_response_instance.to_dict()
# create an instance of SendSignInValidationCode200Response from a dict
send_sign_in_validation_code200_response_from_dict = SendSignInValidationCode200Response.from_dict(send_sign_in_validation_code200_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


