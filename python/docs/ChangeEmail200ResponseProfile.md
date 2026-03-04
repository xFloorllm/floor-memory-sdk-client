# ChangeEmail200ResponseProfile

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

| [**ChangeEmail200ResponseProfileAvatar**](ChangeEmail200ResponseProfileAvatar.md) |
|

[optional]

### Example

```python
from xfloor_memory_sdk.models.change_email200_response_profile import ChangeEmail200ResponseProfile

# TODO update the JSON string below
json = "{}"
# create an instance of ChangeEmail200ResponseProfile from a JSON string
change_email200_response_profile_instance = ChangeEmail200ResponseProfile.from_json(json)
# print the JSON string representation of the object
print(ChangeEmail200ResponseProfile.to_json())

# convert the object into a dict
change_email200_response_profile_dict = change_email200_response_profile_instance.to_dict()
# create an instance of ChangeEmail200ResponseProfile from a dict
change_email200_response_profile_from_dict = ChangeEmail200ResponseProfile.from_dict(change_email200_response_profile_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


