# UserDetailsProfile

User profile details

### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**floor_id**

| **str** | Associated floor ID |
**floor_count_info**

| [**Remaining**](Remaining.md) |
|

[optional]
**block_count_info**

| [**Remaining**](Remaining.md) |
|

[optional]
**fid**

| **str** | Unique ID of floor |
**title**

| **str** |
|

[optional]
**name**

| **str** | User Name |

[optional]
**email**

| **str** | Email ID |

[optional]
**mobile_number**

| **str** | Mobile number |

[optional]
**user_id**

| **str** | Unique User ID |
**avatar**

| [**UserDetailsProfileAvatar**](UserDetailsProfileAvatar.md) |
|

[optional]

### Example

```python
from xfloor_memory_sdk.models.user_details_profile import UserDetailsProfile

# TODO update the JSON string below
json = "{}"
# create an instance of UserDetailsProfile from a JSON string
user_details_profile_instance = UserDetailsProfile.from_json(json)
# print the JSON string representation of the object
print(UserDetailsProfile.to_json())

# convert the object into a dict
user_details_profile_dict = user_details_profile_instance.to_dict()
# create an instance of UserDetailsProfile from a dict
user_details_profile_from_dict = UserDetailsProfile.from_dict(user_details_profile_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


