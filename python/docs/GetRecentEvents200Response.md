# GetRecentEvents200Response


### Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**post_count** | **str** | Number of posts | 
**items** | [**List[GetRecentEvents200ResponseItemsInner]**](GetRecentEvents200ResponseItemsInner.md) | List of posts | 

### Example

```python
from xfloor_memory_sdk.models.get_recent_events200_response import GetRecentEvents200Response

# TODO update the JSON string below
json = "{}"
# create an instance of GetRecentEvents200Response from a JSON string
get_recent_events200_response_instance = GetRecentEvents200Response.from_json(json)
# print the JSON string representation of the object
print(GetRecentEvents200Response.to_json())

# convert the object into a dict
get_recent_events200_response_dict = get_recent_events200_response_instance.to_dict()
# create an instance of GetRecentEvents200Response from a dict
get_recent_events200_response_from_dict = GetRecentEvents200Response.from_dict(get_recent_events200_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


