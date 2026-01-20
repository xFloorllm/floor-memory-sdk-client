# GetRecentEvents200ResponseItemsInner

Each post item

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**event_id** | **str** |  Post ID | [optional] 
**block_type** | **str** | Block Type | [optional] 
**author** | [**GetRecentEvents200ResponseItemsInnerAuthor**](GetRecentEvents200ResponseItemsInnerAuthor.md) |  | [optional] 
**media** | [**List[Media]**](Media.md) | Any media attached | [optional] 
**floor_uid** | **str** | 13 digit ID of the floor in which the post is residing | [optional] 
**title** | **str** | Post title | [optional] 
**text** | **str** | Post details | [optional] 
**created_at_ms** | **str** | Created time in milli seconds | [optional] 
**block_id** | **str** | Numeric ID of the block | [optional] 

## Example

```python
from xfloor_memory_sdk.models.get_recent_events200_response_items_inner import GetRecentEvents200ResponseItemsInner

# TODO update the JSON string below
json = "{}"
# create an instance of GetRecentEvents200ResponseItemsInner from a JSON string
get_recent_events200_response_items_inner_instance = GetRecentEvents200ResponseItemsInner.from_json(json)
# print the JSON string representation of the object
print(GetRecentEvents200ResponseItemsInner.to_json())

# convert the object into a dict
get_recent_events200_response_items_inner_dict = get_recent_events200_response_items_inner_instance.to_dict()
# create an instance of GetRecentEvents200ResponseItemsInner from a dict
get_recent_events200_response_items_inner_from_dict = GetRecentEvents200ResponseItemsInner.from_dict(get_recent_events200_response_items_inner_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


