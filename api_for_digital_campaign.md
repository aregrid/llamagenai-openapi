# LlamaGen Comic API

 The LlamaGen Comic API allows you to generate and retrieve comic artwork using AI-powered image generation. This API provides endpoints to create comic artwork based on prompts and retrieve the generated comic panels.

## Authentication

 To use the LlamaGen Comic API, you need to include your API key in the Authorization header of each request. Replace "YOUR_API_KEY" with your actual API key.

 ```
 const API_KEY = "YOUR_API_KEY";
 ```

## Endpoints

### Generate Comic Artwork

 Generates a new comic artwork based on the provided prompt and image URL.

- **URL**: `https://llamagen.ai/api/openapi/artworks`
- **Method**: `POST`
- **Headers**:
  - `Authorization`: `Bearer YOUR_API_KEY`
- **Request Body**:
  - `prompt` (string): The prompt for generating the comic artwork. Accepted values: `running`, `flexibility`,  `flying`, `laser_speed`, `laser_flexibility`, `laser_flying`， `castle_speed`, `castle_flexibility`, `castle_flying`.
  - `imageUrl` (string): The URL of the image to use as a reference for generating the comic artwork.
  - `gender` (string): The gender of the person in the image. Accepted values: "male", "female", "other".
  - `age` (number): The age of the person in the image. Must be a number between 0 and 150.

#### Example Request

 ```typescript
 const formdata = new FormData();
 formdata.append("prompt", "running");
 formdata.append("imageUrl", "https://example.com/image.png");
 formdata.append("gender", "male");
 formdata.append("age", 30);

 const headers = new Headers();
 headers.append("Authorization", `Bearer ${API_KEY}`);

 const res = await fetch("https://llamagen.ai/api/openapi/artworks", {
   method: "POST",
   body: formdata,
   headers: headers,
 });
 ```

```bash
curl -X POST "https://llamagen.ai/api/openapi/artworks" \
-H "Authorization: Bearer YOUR_API_KEY" \
-F "prompt=flexibility" \
-F "imageUrl=https://example.com/image.png" \
-F "gender=male" \
-F "age=12"
```

```python
import requests
import json
base_url = "https://llamagen.ai"
def post_artwork(api_token: str, prompt: str, imageUrl: str, gender: str, age: int) -> dict:
    api_url = f"{base_url}/api/openapi/artworks"
    headers = {
        'Authorization': f'Bearer {api_token}'
    }
    data = {
        'prompt': prompt,
        'imageUrl': imageUrl,
        'gender': gender,
        'age': age
    }

    response = requests.post(api_url, headers=headers, data=data)

    if response.status_code == 200:
        return response.json()
    else:
        response.raise_for_status()
```

#### Example Response

 ```json
 {
   "artwork": {
     "id": "artwork_id"
   }
 }
 ```

 The response includes the ID of the generated comic artwork, which can be used to retrieve the comic panels later.

### Retrieve Comic Artwork

 Retrieves the generated comic panels for a specific artwork ID.

- **URL**: `https://llamagen.ai/api/openapi/artworks/{id}`
- **Method**: `GET`
- **Headers**:
  - `Authorization`: `Bearer YOUR_API_KEY`
- **Path Parameters**:
  - `id` (string): The ID of the comic artwork to retrieve.

#### Example Request

 ```typescript
 const headers = new Headers();
 headers.append("Authorization", `Bearer ${API_KEY}`);

 const response = await fetch("https://llamagen.ai/api/artworks/" + id, {
   headers: headers,
 });
 ```

```bash
curl -X GET "https://llamagen.ai/api/openapi/artworks/YOUR_ARTWORK_ID" \
-H "Authorization: Bearer YOUR_API_KEY"
```

```python
import requests
import json
base_url = "https://llamagen.ai"
def get_artwork(artwork_id, api_token):
    api_url = f"{base_url}/api/openapi/artworks"
    headers = {
        'Authorization': f'Bearer {api_token}',
    }

    response = requests.get(f"{api_url}/{artwork_id}", headers=headers)

    if response.status_code == 401:
        print("Unauthorized request.")
        return None
    elif response.status_code == 404:
        print("Artwork not found.")
        return None
    elif response.status_code == 500:
        print("Server error.")
        return None

    return response.json()
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

 If an error occurs during the API request or if the comic artwork generation fails, the API will return an appropriate error response with details about the error.

### Common Error Responses

- `400 Bad Request`: The request was invalid or cannot be otherwise served.
- `401 Unauthorized`: Authentication credentials were missing or incorrect.
- `404 Not Found`: The requested resource could not be found.
- `500 Internal Server Error`: An error occurred on the server.

 Each error response will include a JSON object with an `error` field containing details about the error.

#### Example Error Response

 ```json
 {
   "error": "Invalid API key."
 }
 ```

## Versioning

 This documentation refers to version 1.0 of the LlamaGen Comic API. Future updates and changes will be documented here.

 ---

 For more information or support, please contact our API support team at [support@llamagen.ai](mailto:support@llamagen.ai).
