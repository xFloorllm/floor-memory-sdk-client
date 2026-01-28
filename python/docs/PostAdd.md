# PostAdd


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**floor_id**

| **str** | Floor ID to which the post needs to be added |
**bid**

| **str** | Block type (0 or 1) |
**user_id**

| **str** | User Identifcation who has added the post |
**title**

| **str** | Title of the post |
**description**

| **str** | Description or Details |

### Example

```python
from xfloor_memory_sdk.models.post_add import PostAdd

# TODO update the JSON string below
json = "{}"
# create an instance of PostAdd from a JSON string
post_add_instance = PostAdd.from_json(json)
# print the JSON string representation of the object
print(PostAdd.to_json())

# convert the object into a dict
post_add_dict = post_add_instance.to_dict()
# create an instance of PostAdd from a dict
post_add_from_dict = PostAdd.from_dict(post_add_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


