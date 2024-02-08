---
sidebar_position: 1
---

# Create an ad creative

### POST `https://api.adcreative.com/v1/ad-creative`

Create a new ad creative with a `POST` request to this endpoint.

> 💡 To create multiple ad creatives with a single request, see the [Create bulk ad creatives](./create-bulk-ad-creatives) endpoint.

## Requests

### Body parameters

The body parameters for this `POST` request must include the customizable fields of an [ad creative object](/docs/intro#ad-creative-object).

| Param             | Type                                                                                       | Required | Example                                                                       |
| ----------------- | ------------------------------------------------------------------------------------------ | -------- | ----------------------------------------------------------------------------- |
| `id`              | `string`                                                                                   | yes ✅   | `"jyh7"`                                                                      |
| `name`            | `string`                                                                                   | yes ✅   | `"Ad Creative 1"  `                                                           |
| `type`            | `string`                                                                                   | yes ✅   | `"text"`                                                                      |
| `content`         | `string`                                                                                   | yes ✅   | `"Here is some text for an ad"`                                               |
| `additional_data` | `array` of `{ key: value }` objects where the key is a string and the value is `any` type. | no ❌    | `[{ "example1": 15 },{ "example2": "another value" },{ "example3": false },]` |

### Request examples

#### cURL

```bash
curl -X POST 'https://api.adcreative.com/v1/ad-creative' \
  -H 'Authorization: Bearer '"$X_TOKEN"'' \
  -H "Content-Type: application/json" \
  --data '{
  "id": "jess1",
  "name": "First Ad Creative",
  "content": "/images/first_ad_creative.png",
  "additional_data": [
    {
      "client": "Sigma"
    },
  ]
}'
```

#### JavaScript

```jsx
async function createAdCreative(options) {
  const { id, name, type, content, additional_data } = options;

  // Return early if required data is not included
  if (!id || !name || !type || !content) {
    console.error("Error: A required field is missing");
    // (Add additional error handling as needed)
    return;
  }

  const baseURL = "https://api.adcreative.com/v1/ad-creative";
  const data = { id, name, type, content, additional_data };
  const token = process.env.X_TOKEN;

  // Make POST request
  try {
    const response = await fetch(baseURL, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${token}`,
      },
      body: JSON.stringify(data),
    });

    return await response.json();
  } catch (error) {
    console.error("Error:", error);
    return error;
  }
}

const data = {
  id: "jess1",
  name: "First Ad Creative",
  type: "image",
  content: "/images/first_ad_creative.png",
  additional_data: [{ client: "TBD" }],
};

const newAC = createAdCreative(data);
```

## Responses

### Success (`200` )

#### Response body

Successful requests will respond with a `200` status code, as well as the [ad creative object](/docs/intro#ad-creative-object) object for the newly created ad creative.

| Field               | Type                |
| ------------------- | ------------------- |
| `id`                | `string`            |
| `name`              | `string`            |
| `type`              | `string`            |
| `content`           | `string`            |
| `additional_data`   | `array`             |
| `created_at`        | `string` (ISO date) |
| `last_updated_time` | `string` (ISO date) |

#### Response example

```json
{
  "id": "jess1",
  "name": "First Ad Creative",
  "type": "image",
  "content": "/images/first_ad_creative.png",
  "additional_data": [{ "client": "TBD" }],
  "created_time": "2024-01-31 23:59:59",
  "last_updated_time": "2024-01-31 23:59:59"
}
```

### Error (`400`)

Unsuccessful requests will respond with a status code of `400`.

Errors can occur for various reasons, such as a missing or invalid token or required parameter. To resolve request errors, refer to the `error_msg` in the response body for more information.

```json
{
  "error": {
    "error_msg": "Missing required parameters in request. 'name' parameter should be included."
  }
}
```
