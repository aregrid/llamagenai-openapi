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

URL: <https://www.llamagen.ai/api/openapi/artworks>

Method: POST

Request Body:

prompt (string): The prompt for generating the comic artwork. Accepted values: "running", "flexibility", or "flying".

imageUrl (string): The URL of the image to use as a reference for generating the comic artwork.

Example Request:

```
const formdata = new FormData();
formdata.append("prompt", "running");
formdata.append("imageUrl", "https://example.com/image.png");
```

const headers = new Headers();
headers.append("Authorization", `Bearer ${API_KEY}`);

const res = await fetch("<https://www.llamagen.ai/api/openapi/artworks>", {
  method: "POST",
  body: formdata,
  headers: headers,
});
Example Response:

```
{
  "artwork": {
    "id": "artwork_id"
  }
}
```

The response includes the ID of the generated comic artwork, which can be used to retrieve the comic panels later.

Retrieve Comic Artwork
Retrieves the generated comic panels for a specific artwork ID.

URL: <https://llamagen.ai/api/artworks/{id}>

Method: GET

### Path Parameters

id (string): The ID of the comic artwork to retrieve.

Example Request:

```
const headers = new Headers();
headers.append("Authorization", `Bearer ${API_KEY}`);

const response = await fetch("https://llamagen.ai/api/artworks/" + id, {
  headers: headers,
});
```

Example Response:

```
{
  "status": "PROCESSED",
  "comicData": "{\"panels\":[{\"assetUrl\":\"https://example.com/panel1.png\"},{\"assetUrl\":\"https://example.com/panel2.png\"}]}"
}
```

The response includes the status of the comic artwork ("LOADING", "PROCESSED", or "FAILED") and the comicData field containing a JSON-encoded string representing the comic panels. The comicData can be parsed to obtain the asset URLs of the generated comic panels.

## Types

### ArtworkStatus

Represents the status of a comic artwork.

"LOADING": The comic artwork is still being generated.

"PROCESSED": The comic artwork has been successfully generated.

"FAILED": The comic artwork generation failed.

### ArtworkResult

Represents the result of retrieving a comic artwork.

status (ArtworkStatus): The status of the comic artwork.

comicData (string): A JSON-encoded string containing the comic panel data.

### ComicData

Represents the data of the generated comic panels.

panels (array): An array of objects representing the comic panels.

assetUrl (string): The URL of the comic panel image asset.

## Error Handling

If an error occurs during the API request or if the comic artwork generation fails, the API will return an appropriate error response with details about the error.
