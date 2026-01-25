# ValidateCode400ResponseError


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**code**

| **str** | error code |
**message**

| **str** | The signup failed or wrong user_id |
**path**

| **str** |
|
**timestamp**

| **str** |
|

### Example

```python
from xfloor_memory_sdk.models.validate_code400_response_error import ValidateCode400ResponseError

# TODO update the JSON string below
json = "{}"
# create an instance of ValidateCode400ResponseError from a JSON string
validate_code400_response_error_instance = ValidateCode400ResponseError.from_json(json)
# print the JSON string representation of the object
print(ValidateCode400ResponseError.to_json())

# convert the object into a dict
validate_code400_response_error_dict = validate_code400_response_error_instance.to_dict()
# create an instance of ValidateCode400ResponseError from a dict
validate_code400_response_error_from_dict = ValidateCode400ResponseError.from_dict(validate_code400_response_error_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


