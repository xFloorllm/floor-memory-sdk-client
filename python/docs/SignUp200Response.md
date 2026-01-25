# SignUp200Response


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**user_id**

| **str** | User ID |
**success**

| **str** | Success string - \"Enter Validation code\" |

### Example

```python
from xfloor_memory_sdk.models.sign_up200_response import SignUp200Response

# TODO update the JSON string below
json = "{}"
# create an instance of SignUp200Response from a JSON string
sign_up200_response_instance = SignUp200Response.from_json(json)
# print the JSON string representation of the object
print(SignUp200Response.to_json())

# convert the object into a dict
sign_up200_response_dict = sign_up200_response_instance.to_dict()
# create an instance of SignUp200Response from a dict
sign_up200_response_from_dict = SignUp200Response.from_dict(sign_up200_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


