# Bicycles

## JSON:API paths and responses

Endpoint: `/jsonapi/node/bicycle`

Output: `jsonapi_node_bicycle.json`

Response contains all fields of every *bicycle*, including the relationship with the *bicycle type*, but not the data of that related resource.

### Specify fields

Append to endpoint: `?fields[node--bicycle]=title,field_brand,field_gear_ratio,field_wheel_size`

Output: `jsonapi_node_bicycle_fields.json`

Response contains only the "flat" fields in the resource, leaving out the relationship.

### Include related resource

Append to fields: `&include=field_type`

Output: `jsonapi_node_bicycle_fields_include.json`

Response includes the related resources even without a visible relationship.

### Specify fields in related resource

Append to include: `&fields[taxonomy_term--bicycle_type]=name`

Output: `jsonapi_node_bicycle_fields_include_fields.json`

Response contains only the "flat" fields in the related resource.

### Filter by field value

Append to fields: `&filter[field_wheel_size]=28`

Output: `jsonapi_node_bicycle_fields_filter.json`

Response contains only resources with specified field value.

### Filter by field value in related resource

Append to fields: `&filter[field_type.name]=MTB`

Output: `jsonapi_node_bicycle_fields_filter_related.json`

Response contains only resources with specified field value in the related resource.
