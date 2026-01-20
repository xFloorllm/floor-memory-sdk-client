# GetFloorInformation200Response


## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**floor_id** | **str** | Pod floor ID | 
**title** | **str** | Title | 
**details** | **str** | Brief description about the Pod floor | [optional] 
**fid** | **str** | Unique numeric ID of the pod floor | 
**blocks** | [**List[BlockDetails]**](BlockDetails.md) | List of blocks | [optional] 
**avatar** | [**Media**](Media.md) |  | [optional] 

## Example

```python
from xfloor_memory_sdk.models.get_floor_information200_response import GetFloorInformation200Response

# TODO update the JSON string below
json = "{}"
# create an instance of GetFloorInformation200Response from a JSON string
get_floor_information200_response_instance = GetFloorInformation200Response.from_json(json)
# print the JSON string representation of the object
print(GetFloorInformation200Response.to_json())

# convert the object into a dict
get_floor_information200_response_dict = get_floor_information200_response_instance.to_dict()
# create an instance of GetFloorInformation200Response from a dict
get_floor_information200_response_from_dict = GetFloorInformation200Response.from_dict(get_floor_information200_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


