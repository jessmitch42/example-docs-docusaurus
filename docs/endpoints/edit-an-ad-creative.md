---
sidebar_position: 5
---

# Edit an ad creative

### PATCH `https://api.adcreative.com/v1/ad-creative/<id>`

Update an existing ad creative with a `PATCH` request to this endpoint.

## Requests

`PATCH` requests must include the [ad creative object](/docs/intro#ad-creative-object) `id` as a path param to indicate which ad creative is being updated, as well as the fields being updated in the body params. Only the fields being updated are required.

### Path params

| Param | Type     | Required | Example  |
| ----- | -------- | -------- | -------- |
| `id`  | `string` | yes ✅   | `"jyh7"` |

```text
https://api.adcreative.com/v1/ad-creative/jyh7
```

### Body parameters

Include only the body parameters that need to be updated for the ad creative. Fields that are not included will not be updated from the original. Required fields cannot be set to `null` or `undefined`.

| Param             | Type                                               | Required | Example                                                                       |
| ----------------- | -------------------------------------------------- | -------- | ----------------------------------------------------------------------------- |
| `id`              | `string`                                           | no ❌    | `"jyh7"`                                                                      |
| `name`            | `string`                                           | no ❌    | `"Ad Creative 1"`                                                             |
| `type`            | `string`                                           | no ❌    | `"text"`                                                                      |
| `content`         | `string`                                           | no ❌    | `"Here is some text for an ad"`                                               |
| `additional_data` | `array` of key (`string`) ⇒ value (`any`) elements | no ❌    | `[{ "example1": 15 },{ "example2": "another value" },{ "example3": false },]` |

### Request examples

#### cURL

```bash
curl -X PATCH 'https://api.adcreative.com/v1/ad-creative/jyh7' \
  -H 'Authorization: Bearer '"$X_TOKEN"'' \
  -H "Content-Type: application/json" \
  --data '{
  "content": "/images/different_source_image.png",
  }'
```

#### JavaScript

```jsx
async function updateAdCreative(data) {
  const { id, options } = data;
  if (!id) {
    console.error("An ID is required.");
    return;
  }
  const baseURL = `https://api.adcreative.com/v1/ad-creative/${id}`;
  const token = process.env.X_TOKEN;

  // Make PATCH request
  try {
    const response = await fetch(baseURL, {
      method: "PATCH",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${token}`,
      },
      body: JSON.stringify(options),
    });

    return await response.json();
  } catch (error) {
    console.error("Error:", error);
    return error;
  }
}

const data = {
  id: "jyh7",
  options: { content: "/images/different_source_image.png" },
};

const updatedAC = updateAdCreative(data);
```

## Responses

### Success (`200` )

#### Response body

Successful requests will respond with a `200` status code, as well as information related to the updated ad creative. The full ad creative object will be returned even if only certain fields were updated.

| Field              | Type     |
| ------------------ | -------- |
| `id`               | `string` |
| `name`             | `string` |
| `type`             | `string` |
| `content`          | `string` |
| `additional_data`  | `array`  |
| `created_at`       | `string` |
| `last_edited_time` | `string` |

#### Response example

```json
{
  "id": "jess1",
  "name": "First Ad Creative",
  "type": "image",
  "content": "/images/different_source_image.png",
  "additional_data": [{ "client": "TBD" }],
  "created_time": "2024-01-31 23:59:59",
  "last_edited_time": "2024-02-04 13:59:59"
}
```

### Error (`400` )

Errors can occur for different reasons, such as a missing or invalid token or required parameter. To resolve request errors, refer to the `error_msg` in the response body for more information.

```json
{
  "error": {
    "error_msg": "The ID included does not match the ID of an ad creative tied to this account."
  }
}
```
