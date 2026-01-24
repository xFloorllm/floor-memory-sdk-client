# SignInWithEmail200ResponsePodInfo


### Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**floor_id** | **str** |  | 
**title** | **str** |  | 
**details** | **str** |  | [optional] 
**fid** | **str** |  | 
**blocks** | [**List[BlockDetails]**](BlockDetails.md) |  | 
**avatar** | [**Media**](Media.md) |  | [optional] 

### Example

```python
from xfloor_memory_sdk.models.sign_in_with_email200_response_pod_info import SignInWithEmail200ResponsePodInfo

# TODO update the JSON string below
json = "{}"
# create an instance of SignInWithEmail200ResponsePodInfo from a JSON string
sign_in_with_email200_response_pod_info_instance = SignInWithEmail200ResponsePodInfo.from_json(json)
# print the JSON string representation of the object
print(SignInWithEmail200ResponsePodInfo.to_json())

# convert the object into a dict
sign_in_with_email200_response_pod_info_dict = sign_in_with_email200_response_pod_info_instance.to_dict()
# create an instance of SignInWithEmail200ResponsePodInfo from a dict
sign_in_with_email200_response_pod_info_from_dict = SignInWithEmail200ResponsePodInfo.from_dict(sign_in_with_email200_response_pod_info_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


