# SignInResponse


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**profile**

| [**UserDetailsProfile**](UserDetailsProfile.md) |
|
**pod_info**

| [**UserDetailsPodInfo**](UserDetailsPodInfo.md) |
|
**app_id**

| **str** | App ID |

[optional]

### Example

```python
from xfloor_memory_sdk.models.sign_in_response import SignInResponse

# TODO update the JSON string below
json = "{}"
# create an instance of SignInResponse from a JSON string
sign_in_response_instance = SignInResponse.from_json(json)
# print the JSON string representation of the object
print(SignInResponse.to_json())

# convert the object into a dict
sign_in_response_dict = sign_in_response_instance.to_dict()
# create an instance of SignInResponse from a dict
sign_in_response_from_dict = SignInResponse.from_dict(sign_in_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


