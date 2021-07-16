# Locations

## JSON:API paths and responses

Endpoint: `/jsonapi/node/location`

Output: `jsonapi_node_location.json`

Response contains all fields of every *location*, including the relationship with the *bikes*, but not the data of that related resource.

### Specify fields

Append to endpoint: `?fields[node--location]=title`

Output: `jsonapi_node_location_fields.json`

Response contains only the "flat" fields in the resource, leaving out the relationship.

### Include related resource

Append to fields: `&include=field_bikes`

Output: `jsonapi_node_location_fields_include.json`

Response includes the related resources even without a visible relationship. However the relationships of the related resources are visible.

### Specify fields in related resource

Append to include: `&fields[node--bicycle]=title,field_brand,field_gear_ratio,field_wheel_size`

Output: `jsonapi_node_location_fields_include_fields.json`

Response contains only the "flat" fields in the related resource.

### Filter by field value in related resource

Append to fields: `&filter[field_bikes.field_wheel_size]=28`

Output: `jsonapi_node_location_fields_filter_related.json`

Response contains only resources with specified field value in the related resource.

### Filter by field value in related resource's related resource

Append to fields: `&filter[field_bikes.field_type.name]=MTB`

Output: `jsonapi_node_location_fields_filter_related_chained.json`

Response contains only resources with specified field value in the related resource field's related resource.

## Limitations

When we request _locations_ that have _bikes_ of a certain _type_ we obtain a correct response. **However** if we include the _bikes_ in the response, those includes are not filtered. Which sucks.

  - original endpoint:  `/jsonapi/node/location`
  - location fields:    `?fields[node--location]=title`
  - include bicycle:    `&include=field_bikes`
  - bicycle fields:     `&fields[node--bicycle]=title,field_brand,field_gear_ratio,field_wheel_size`
  - filter by type:     `&filter[field_bikes.field_type.name]=MTB`
  - include type:       `&include=field_bikes.field_type`
  - type fields:        `&fields[taxonomy_term--bicycle_type]=name`

Output: `jsonapi_node_location_kitchen_sink.json`

Response contains the only _location_ where _bikes_ of _type_ "MTB" are present. **However** when we include the _bikes_ we can see **every bike** at that _location_ and when we include the _type_ we can see **every type** of _bikes_ at that _location_.

**In conclusion** the filters only apply to the targeted resource, which means filtering the includes must be done _after_ receiving the response.
