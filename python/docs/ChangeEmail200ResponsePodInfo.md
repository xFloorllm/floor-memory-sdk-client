# ChangeEmail200ResponsePodInfo


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
from xfloor_memory_sdk.models.change_email200_response_pod_info import ChangeEmail200ResponsePodInfo

# TODO update the JSON string below
json = "{}"
# create an instance of ChangeEmail200ResponsePodInfo from a JSON string
change_email200_response_pod_info_instance = ChangeEmail200ResponsePodInfo.from_json(json)
# print the JSON string representation of the object
print(ChangeEmail200ResponsePodInfo.to_json())

# convert the object into a dict
change_email200_response_pod_info_dict = change_email200_response_pod_info_instance.to_dict()
# create an instance of ChangeEmail200ResponsePodInfo from a dict
change_email200_response_pod_info_from_dict = ChangeEmail200ResponsePodInfo.from_dict(change_email200_response_pod_info_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


