# ResetPassword400Response


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**code**

| **str** | Validation Error |
**message**

| **str** | Error Message |
**path**

| **str** | REST api path |
**timestamp**

| **str** | Time stamp |

### Example

```python
from xfloor_memory_sdk.models.reset_password400_response import ResetPassword400Response

# TODO update the JSON string below
json = "{}"
# create an instance of ResetPassword400Response from a JSON string
reset_password400_response_instance = ResetPassword400Response.from_json(json)
# print the JSON string representation of the object
print(ResetPassword400Response.to_json())

# convert the object into a dict
reset_password400_response_dict = reset_password400_response_instance.to_dict()
# create an instance of ResetPassword400Response from a dict
reset_password400_response_from_dict = ResetPassword400Response.from_dict(reset_password400_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


