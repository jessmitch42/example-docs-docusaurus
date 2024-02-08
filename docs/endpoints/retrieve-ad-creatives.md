---
sidebar_position: 3
---

# Retrieve ad creative list

### GET `https://api.adcreative.com/v1/ad-creative?ids=<id1>,<id2>,...`

Retrieve a list of existing ad creative using a `GET` request to this endpoint. To retrieve specific ad creatives, include their IDs as a list under the `ids` query parameter.

## Requests

### Query parameters

| Param | Type     | Required | Example  |
| ----- | -------- | -------- | -------- |
| `ids` | `string` | yes ✅   | `"jyh7"` |

### Request examples

#### cURL

```bash
curl 'https://api.adcreative.com/v1/ad-creative?ids=<id1>,<id2>' \
  -H 'Authorization: Bearer '"$X_TOKEN"'' \
  -H "Content-Type: application/json"
```

#### JavaScript

```jsx
async function getAdCreativeList(idArray) {
  const token = process.env.X_TOKEN;
  // add
  const queryParams = idArray.map((id) => id).join(",");
  const url = `https://api.adcreative.com/v1/ad-creative?ids=${queryParams}`;

  // Make GET request
  try {
    const response = await fetch(url, {
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

const existingACs = getAdCreativeList(["jyh7", "h7g0"]);
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
    "id": "jyh7",
    "name": "First Ad Creative",
    "type": "image",
    "content": "/images/first_ad_creative.png",
    "additional_data": [{ "client": "TBD" }],
    "created_time": "2024-01-31 23:59:58",
    "last_updated_time": "2024-01-31 23:59:58"
  },
  {
    "id": "h7g0",
    "name": "Another Ad Creative",
    "type": "text",
    "content": "Here is some text for an ad!",
    "additional_data": [],
    "created_time": "2024-01-31 23:59:59",
    "last_updated_time": "2024-01-31 23:59:59"
  }
]
```

### Error (`400`)

Unsuccessful requests will respond with a status code of `400`.

Errors while creating ad creatives can occur for various reasons, such as a missing or invalid token or required parameter.

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
