# LlamaGen.Ai REST API

The LlamaGen Comic API allows you to generate and retrieve comic artwork using AI-powered image generation. This API provides endpoints to create comic artwork based on prompts and retrieve the generated comic panels with different styles.

## Introduction

The LlamaGen Comic API offers three main methods for interacting with comic images:

1. Creating comic panels from scratch based on a text prompt
2. Retrieving generated comic artwork
3. (Future feature) Creating variations of existing comic panels

This guide covers the basics of using these API endpoints with useful code samples.

## Usage

### Create Comic Artwork

Creates a new comic artwork based on the provided prompt and other parameters.

```bash
curl -X POST "https://api.llamagen.ai/v1/comics/generations" \
-H "Content-Type: application/json" \
-H "Authorization: Bearer $LLAMAGENAI_API_KEY" \
-d '{
  "model": "cyani-model",
  "prompt": "a comic about a cat and a dog",
  "size": "1024x1024"
}'
```

#### Parameters

- `model` (string): The AI model to use for generation (e.g., "cyani-model")
- `prompt` (string): A text description of the desired comic scene
- `size` (string): The size of the generated image (e.g., "1024x1024")

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
curl -X GET "https://api.llamagen.ai/v1/comics/generations/YOUR_ARTWORK_ID" \
-H "Authorization: Bearer YOUR_API_KEY"
```

#### Example Response

```json
{
  "status": "PROCESSED",
  "comicData": "{\"panels\":[{\"assetUrl\":\"https://example.com/panel1.png\"},{\"assetUrl\":\"https://example.com/panel2.png\"}]}"
}
```

The response includes the status of the comic artwork and the `comicData` field containing a JSON-encoded string representing the comic panels.

// ... existing code for Types and Error Handling ...

## Versioning

This documentation refers to version 1.0 of the LlamaGen Comic API. Future updates and changes will be documented here.

---

For more information or support, please contact our API support team at [support@llamagen.ai](mailto:support@llamagen.ai).