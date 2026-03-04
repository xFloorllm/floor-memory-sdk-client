# UserDetailsPodInfo


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**floor_id**

| **str** |
|
**is_owner**

| **str** |
|

[optional]
**app_id**

| **str** |
|

[optional]
**title**

| **str** |
|
**details**

| **str** |
|

[optional]
**floor_uid**

| **str** |
|
**blocks**

| [**List[BlockDetails]**](BlockDetails.md) |
|
**avatar**

| [**Media**](Media.md) |
|

[optional]

### Example

```python
from xfloor_memory_sdk.models.user_details_pod_info import UserDetailsPodInfo

# TODO update the JSON string below
json = "{}"
# create an instance of UserDetailsPodInfo from a JSON string
user_details_pod_info_instance = UserDetailsPodInfo.from_json(json)
# print the JSON string representation of the object
print(UserDetailsPodInfo.to_json())

# convert the object into a dict
user_details_pod_info_dict = user_details_pod_info_instance.to_dict()
# create an instance of UserDetailsPodInfo from a dict
user_details_pod_info_from_dict = UserDetailsPodInfo.from_dict(user_details_pod_info_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


