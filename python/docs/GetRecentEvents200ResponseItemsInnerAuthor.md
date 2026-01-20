# GetRecentEvents200ResponseItemsInnerAuthor

Author details

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**name** | **str** | Name of the author | [optional] 
**floor_id** | **str** | Profile floor of the auther | [optional] 
**avatar** | [**Media**](Media.md) |  | [optional] 
**floor_uid** | **str** | Unique 13 digit id of the profile floor | [optional] 

## Example

```python
from xfloor_memory_sdk.models.get_recent_events200_response_items_inner_author import GetRecentEvents200ResponseItemsInnerAuthor

# TODO update the JSON string below
json = "{}"
# create an instance of GetRecentEvents200ResponseItemsInnerAuthor from a JSON string
get_recent_events200_response_items_inner_author_instance = GetRecentEvents200ResponseItemsInnerAuthor.from_json(json)
# print the JSON string representation of the object
print(GetRecentEvents200ResponseItemsInnerAuthor.to_json())

# convert the object into a dict
get_recent_events200_response_items_inner_author_dict = get_recent_events200_response_items_inner_author_instance.to_dict()
# create an instance of GetRecentEvents200ResponseItemsInnerAuthor from a dict
get_recent_events200_response_items_inner_author_from_dict = GetRecentEvents200ResponseItemsInnerAuthor.from_dict(get_recent_events200_response_items_inner_author_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


