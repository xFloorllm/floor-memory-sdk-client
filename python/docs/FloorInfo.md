# FloorInfo

User's Pod floor Infomation

### Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**floor_id** | **str** | Pod floor ID | 
**title** | **str** | Title | 
**details** | **str** | Brief description about the Pod floor | [optional] 
**fid** | **str** | Unique numeric ID of the pod floor | 
**blocks** | [**List[BlockDetails]**](BlockDetails.md) | List of blocks | [optional] 
**avatar** | [**Media**](Media.md) |  | [optional] 

### Example

```python
from xfloor_memory_sdk.models.floor_info import FloorInfo

# TODO update the JSON string below
json = "{}"
# create an instance of FloorInfo from a JSON string
floor_info_instance = FloorInfo.from_json(json)
# print the JSON string representation of the object
print(FloorInfo.to_json())

# convert the object into a dict
floor_info_dict = floor_info_instance.to_dict()
# create an instance of FloorInfo from a dict
floor_info_from_dict = FloorInfo.from_dict(floor_info_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


