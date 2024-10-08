# LlamaGen.Ai REST API 

The LlamaGen Comic API allows you to generate and retrieve comic artwork using AI-powered image generation. This API provides endpoints to create comic artwork based on prompts and retrieve the generated comic panels with different style.

## Authentication 

To use the LlamaGen Comic API, you need to include your API key in the Authorization header of each request. Replace "YOUR_API_KEY" with your actual API key.

```typescript
const API_KEY = "YOUR_API_KEY";
```

## Endpoints

### Create Comic Artwork

Creates a new comic artwork based on the provided prompt, image URL, and other parameters.

```bash
curl -X POST "https://llamagen.ai/api/openapi/artworks" \
-H "Authorization: Bearer YOUR_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "prompt": "flexibility"
}'
```

```bash
curl -X POST "https://llamagen.ai/api/openapi/artworks" \
-H "Authorization: Bearer YOUR_API_KEY" \
-F "prompt=flexibility" \
```


#### Example Response

```json
{
  "artwork": {
    "id": "artwork_id"
  }
}
```

The response includes the ID of the created comic artwork, which can be used to retrieve the comic panels later.

### Retrieve Comic Artwork

Retrieves the generated comic panels for a specific artwork ID.

```bash
curl -X GET "https://llamagen.ai/api/openapi/artworks/YOUR_ARTWORK_ID" \
-H "Authorization: Bearer YOUR_API_KEY"
```


#### Example Response

```json
{
  "status": "PROCESSED",
  "comicData": "{\"panels\":[{\"assetUrl\":\"https://example.com/panel1.png\"},{\"assetUrl\":\"https://example.com/panel2.png\"}]}"
}
```

The response includes the status of the comic artwork ("LOADING", "PROCESSED", or "FAILED") and the `comicData` field containing a JSON-encoded string representing the comic panels. The `comicData` can be parsed to obtain the asset URLs of the generated comic panels.

## Types

### ArtworkStatus

Represents the status of a comic artwork.

- `"LOADING"`: The comic artwork is still being generated.
- `"PROCESSED"`: The comic artwork has been successfully generated.
- `"FAILED"`: The comic artwork generation failed.

### ArtworkResult

Represents the result of retrieving a comic artwork.

- `status` (ArtworkStatus): The status of the comic artwork.
- `comicData` (string): A JSON-encoded string containing the comic panel data.

### ComicData

Represents the data of the generated comic panels.

- `panels` (array): An array of objects representing the comic panels.
- `assetUrl` (string): The URL of the comic panel image asset.

## Error Handling

LlamaGen uses conventional HTTP response codes to indicate the success or failure of an API request. Codes in the `2xx` range indicate success. Codes in the `4xx` range indicate an error that failed given the information provided (e.g., a required parameter was omitted). Codes in the `5xx` range indicate an error with LlamaGen's servers.

Some `4xx` errors that could be handled programmatically include an error code that briefly explains the error reported.

| HTTP Status Code | Summary |
|------------------|---------|
| 200 - OK | Everything worked as expected. |
| 400 - Bad Request | The request was unacceptable, often due to missing a required parameter. |
| 401 - Unauthorized | No valid API key provided. |
| 404 - Not Found | The requested resource doesn't exist. |
| 500, 502, 503, 504 - Server Errors | Something went wrong on LlamaGen's end. |

## Versioning

This documentation refers to version 1.0 of the LlamaGen Comic API. Future updates and changes will be documented here.

---

For more information or support, please contact our API support team at [support@llamagen.ai](mailto:support@llamagen.ai).
