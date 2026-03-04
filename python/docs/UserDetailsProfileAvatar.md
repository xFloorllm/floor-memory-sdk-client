# UserDetailsProfileAvatar

Profile Pick details

### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**url**

| **str** | Image URL |
**type**

| **str** | Image ID |

### Example

```python
from xfloor_memory_sdk.models.user_details_profile_avatar import UserDetailsProfileAvatar

# TODO update the JSON string below
json = "{}"
# create an instance of UserDetailsProfileAvatar from a JSON string
user_details_profile_avatar_instance = UserDetailsProfileAvatar.from_json(json)
# print the JSON string representation of the object
print(UserDetailsProfileAvatar.to_json())

# convert the object into a dict
user_details_profile_avatar_dict = user_details_profile_avatar_instance.to_dict()
# create an instance of UserDetailsProfileAvatar from a dict
user_details_profile_avatar_from_dict = UserDetailsProfileAvatar.from_dict(user_details_profile_avatar_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


