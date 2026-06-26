# Response Validation Beyond Status Codes

## Problem

API tests that only check `status_code == 200` verify that the server responded, not that it responded correctly. A response with a 200 status that contains the wrong data, missing fields, or invalid types will pass the test and ship broken.

## Solution

Response validation has three layers: status, schema, and content.

**Status validation** confirms the right HTTP status code for the operation. A successful creation returns 201, not 200. An unauthorized request returns 401, not 403. The specific code matters.

**Schema validation** confirms that the response has the expected shape. Required fields are present, data types match, and no unexpected fields indicate a breaking change has slipped through.

```python
from jsonschema import validate

user_schema = {
    "type": "object",
    "required": ["id", "email", "role", "created_at"],
    "properties": {
        "id": {"type": "integer"},
        "email": {"type": "string", "format": "email"},
        "role": {"type": "string", "enum": ["ADMIN", "USER", "LIMITED"]},
        "created_at": {"type": "string", "format": "date-time"}
    },
    "additionalProperties": False
}

def test_create_user_returns_valid_schema(api):
    response = api.create_user({"email": "user@example.com"})
    validate(instance=response, schema=user_schema)
```

**Content validation** confirms that the specific values returned match expectations. Not just that `role` exists, but that a newly created standard user has `role == "USER"`.

## Real-world example

An API returned `200 OK` with an empty `data` array when a search query matched no results. A test checking only the status code passed. The UI rendered a blank screen instead of a "no results" message because the shape was different from the documented response.

Schema validation would have caught the `data` field missing from the documented response. Content validation would have caught that empty results had a different structure than non-empty ones.

## Key takeaways

- Status code validation is necessary but not sufficient
- Schema validation catches structural changes before they reach the UI
- Content validation catches logic errors that produce the right shape but wrong values
- `jsonschema` provides declarative schema validation without external dependencies
- Test error responses as rigorously as success responses — error shapes are frequently undocumented and inconsistent
