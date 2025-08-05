# API Documentation

This directory contains documentation for all public APIs in the project.

## Documentation Template

When documenting APIs, use the following template:

### API Endpoint Template

```markdown
## [HTTP_METHOD] /api/endpoint-name

Brief description of what this endpoint does.

### Parameters

#### Path Parameters
- `id` (string, required) - Description of the parameter
- `category` (string, optional) - Description of optional parameter

#### Query Parameters
- `limit` (integer, optional) - Maximum number of items to return (default: 10, max: 100)
- `offset` (integer, optional) - Number of items to skip (default: 0)
- `sort` (string, optional) - Sort order: `asc` or `desc` (default: `asc`)

#### Request Body
```json
{
  "name": "string (required) - Name of the resource",
  "description": "string (optional) - Description of the resource",
  "tags": ["array of strings (optional) - Tags associated with the resource"]
}
```

### Response

#### Success Response (200 OK)
```json
{
  "id": "string - Unique identifier",
  "name": "string - Name of the resource",
  "description": "string - Description of the resource",
  "tags": ["array of strings - Tags"],
  "created_at": "string (ISO 8601) - Creation timestamp",
  "updated_at": "string (ISO 8601) - Last update timestamp"
}
```

#### Error Responses

**400 Bad Request**
```json
{
  "error": "Invalid request parameters",
  "details": {
    "field": "name",
    "message": "Name is required"
  }
}
```

**404 Not Found**
```json
{
  "error": "Resource not found",
  "message": "No resource found with the specified ID"
}
```

**500 Internal Server Error**
```json
{
  "error": "Internal server error",
  "message": "An unexpected error occurred"
}
```

### Usage Examples

#### cURL
```bash
# Create a new resource
curl -X POST \
  http://localhost:3000/api/resources \
  -H "Content-Type: application/json" \
  -d '{
    "name": "My Resource",
    "description": "A sample resource",
    "tags": ["example", "demo"]
  }'

# Get a resource by ID
curl -X GET \
  http://localhost:3000/api/resources/123 \
  -H "Accept: application/json"

# Update a resource
curl -X PUT \
  http://localhost:3000/api/resources/123 \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Updated Resource",
    "description": "Updated description"
  }'

# Delete a resource
curl -X DELETE \
  http://localhost:3000/api/resources/123
```

#### JavaScript (Fetch API)
```javascript
// Create a new resource
const response = await fetch('/api/resources', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    name: 'My Resource',
    description: 'A sample resource',
    tags: ['example', 'demo']
  })
});
const data = await response.json();

// Get a resource by ID
const getResponse = await fetch('/api/resources/123');
const resource = await getResponse.json();

// Update a resource
const updateResponse = await fetch('/api/resources/123', {
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    name: 'Updated Resource',
    description: 'Updated description'
  })
});

// Delete a resource
const deleteResponse = await fetch('/api/resources/123', {
  method: 'DELETE'
});
```

#### Python (requests)
```python
import requests
import json

# Create a new resource
response = requests.post(
    'http://localhost:3000/api/resources',
    headers={'Content-Type': 'application/json'},
    json={
        'name': 'My Resource',
        'description': 'A sample resource',
        'tags': ['example', 'demo']
    }
)
data = response.json()

# Get a resource by ID
response = requests.get('http://localhost:3000/api/resources/123')
resource = response.json()

# Update a resource
response = requests.put(
    'http://localhost:3000/api/resources/123',
    headers={'Content-Type': 'application/json'},
    json={
        'name': 'Updated Resource',
        'description': 'Updated description'
    }
)

# Delete a resource
response = requests.delete('http://localhost:3000/api/resources/123')
```

### Rate Limiting

This API implements rate limiting to ensure fair usage:
- **Rate Limit**: 100 requests per minute per IP address
- **Headers**: Rate limit information is included in response headers:
  - `X-RateLimit-Limit`: Maximum requests per window
  - `X-RateLimit-Remaining`: Remaining requests in current window
  - `X-RateLimit-Reset`: Unix timestamp when the rate limit resets

### Authentication

If the API requires authentication, document it here:

#### API Key Authentication
Include the API key in the request header:
```
Authorization: Bearer YOUR_API_KEY
```

#### OAuth 2.0
For OAuth 2.0 authentication, follow these steps:
1. Redirect user to authorization URL
2. Exchange authorization code for access token
3. Include access token in subsequent requests

### Error Handling Best Practices

1. **Always check the HTTP status code** before processing the response
2. **Handle common error scenarios**:
   - Network errors (connection timeout, DNS resolution)
   - HTTP errors (4xx client errors, 5xx server errors)
   - Invalid JSON responses
3. **Implement retry logic** for transient errors (5xx errors)
4. **Log errors appropriately** for debugging and monitoring

### SDK and Client Libraries

If SDKs or client libraries are available, list them here:
- **JavaScript/Node.js**: `npm install project-api-client`
- **Python**: `pip install project-api-client`
- **Go**: `go get github.com/project/api-client-go`

## API Versioning

This project follows semantic versioning for APIs:
- **Major version** (v1, v2): Breaking changes
- **Minor version** (v1.1, v1.2): New features, backward compatible
- **Patch version** (v1.1.1, v1.1.2): Bug fixes, backward compatible

Current API version: **v1.0.0**

## Testing

All APIs should be thoroughly tested. Include:
- Unit tests for individual functions
- Integration tests for API endpoints
- Load tests for performance validation
- Security tests for vulnerability assessment

## Support

For API support and questions:
- **Documentation**: Check this documentation first
- **Issues**: Report bugs and feature requests on GitHub
- **Community**: Join our community forum for discussions
