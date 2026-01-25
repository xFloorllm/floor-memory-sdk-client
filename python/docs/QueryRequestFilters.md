# QueryRequestFilters

JSON format filters

### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**time_from**

| **str** | Start timestamp for filtering content by creation or update time. |
**time_to**

| **str** | End timestamp for filtering content by creation or update time. |
**filter_types**

| **str** | Content types to include (e.g., post, forum). |
**filter_tags**

| **str** | Tags used to further refine the query results. |

### Example

```python
from xfloor_memory_sdk.models.query_request_filters import QueryRequestFilters

# TODO update the JSON string below
json = "{}"
# create an instance of QueryRequestFilters from a JSON string
query_request_filters_instance = QueryRequestFilters.from_json(json)
# print the JSON string representation of the object
print(QueryRequestFilters.to_json())

# convert the object into a dict
query_request_filters_dict = query_request_filters_instance.to_dict()
# create an instance of QueryRequestFilters from a dict
query_request_filters_from_dict = QueryRequestFilters.from_dict(query_request_filters_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


