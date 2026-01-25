# SendValidationCode200Response


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**success**

| **str** | Validation code sent successfully |

### Example

```python
from xfloor_memory_sdk.models.send_validation_code200_response import SendValidationCode200Response

# TODO update the JSON string below
json = "{}"
# create an instance of SendValidationCode200Response from a JSON string
send_validation_code200_response_instance = SendValidationCode200Response.from_json(json)
# print the JSON string representation of the object
print(SendValidationCode200Response.to_json())

# convert the object into a dict
send_validation_code200_response_dict = send_validation_code200_response_instance.to_dict()
# create an instance of SendValidationCode200Response from a dict
send_validation_code200_response_from_dict = SendValidationCode200Response.from_dict(send_validation_code200_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


