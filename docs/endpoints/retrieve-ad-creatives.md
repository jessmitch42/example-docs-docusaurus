---
sidebar_position: 4
---

# Retrieve ad creative list

### GET `https://api.adcreative.com/v1/ad-creative`

Retrieve a list of existing ad creative using a `GET` request to this endpoint.

## Requests

### Parameters

No body or path parameters are required (or permitted) for this endpoint.

### Request examples

#### cURL

```bash
curl 'https://api.adcreative.com/v1/ad-creative' \
  -H 'Authorization: Bearer '"$X_TOKEN"'' \
  -H "Content-Type: application/json"
```

#### JavaScript

```jsx
async function getAdCreativeList() {
  const token = process.env.X_TOKEN;
  const baseURL = "https://api.adcreative.com/v1/ad-creative";

  // Make GET request
  try {
    const response = await fetch(baseURL, {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${token}`,
      },
    });

    return await response.json();
  } catch (error) {
    console.error("Error:", error);
    return error;
  }
}

const existingACs = getAdCreativeList();
```

## Responses

### Success (`200` )

#### Response body

Successful requests will respond with a `200` status code, as well as an array of ad creative objects associated with the developer's account.

| Field               | Type     |
| ------------------- | -------- |
| `id`                | `string` |
| `name`              | `string` |
| `type`              | `string` |
| `content`           | `string` |
| `additional_data`   | `array`  |
| `created_at`        | `string` |
| `last_updated_time` | `string` |

#### Response example

```json
[
  {
    "id": "jess1",
    "name": "First Ad Creative",
    "type": "image",
    "content": "/images/first_ad_creative.png",
    "additional_data": [{ "client": "TBD" }],
    "created_time": "2024-01-31 23:59:58",
    "last_updated_time": "2024-01-31 23:59:58"
  },
  {
    "id": "bob1",
    "name": "Another Ad Creative",
    "type": "text",
    "content": "Here is some text for an ad!",
    "additional_data": [],
    "created_time": "2024-01-31 23:59:59",
    "last_updated_time": "2024-01-31 23:59:59"
  }
]
```

### Error (`400` )

Errors while creating ad creatives can occur for different reasons, such as a missing or invalid token or required parameter.

If creating any ad creative in the array results in an error, the request will fail. The response body will include an array of `error_msg`s to help developers debug their requests.

```json
{
  "error": [
    { "error_msg": null },
    {
      "error_msg": "AC with the provided ID 'bob1' did not include a required field: 'name'"
    }
  ]
}
```
