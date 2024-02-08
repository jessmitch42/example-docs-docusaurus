---
sidebar_position: 4
---

# Update an ad creative

### PATCH `https://api.adcreative.com/v1/ad-creative/<id>`

Update an existing ad creative with a `PATCH` request to this endpoint.

## Requests

### Path params

`PATCH` requests must include the [ad creative object](/docs/intro#ad-creative-object) `id` as a path param to indicate which ad creative is being updated.

| Param | Type     | Required | Example  |
| ----- | -------- | -------- | -------- |
| `id`  | `string` | yes ✅   | `"jyh7"` |

#### Example

```text
https://api.adcreative.com/v1/ad-creative/jyh7
```

### Body parameters

Include only the body parameters that need to be updated for the ad creative. Fields that are not included will not be updated from the original. Required fields for ad creatives cannot be set to `null` or `undefined`.

| Param             | Type                                                                                         | Required | Example                                                                       |
| ----------------- | -------------------------------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------- |
| `name`            | `string`                                                                                     | no ❌    | `"Ad Creative 1"`                                                             |
| `type`            | `string`                                                                                     | no ❌    | `"text"`                                                                      |
| `content`         | `string`                                                                                     | no ❌    | `"Here is some text for an ad"`                                               |
| `additional_data` | `array` of `{ key: value }` objects where the key is a `string` and the value is `any` type. | no ❌    | `[{ "example1": 15 },{ "example2": "another value" },{ "example3": false },]` |

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
{
  "id": "jess1",
  "name": "First Ad Creative",
  "type": "image",
  "content": "/images/different_source_image.png",
  "additional_data": [{ "client": "TBD" }],
  "created_time": "2024-01-31 23:59:59",
  "last_updated_time": "2024-02-04 13:59:59"
}
```

### Error (`400`, `404`)

Unsuccessful requests will respond with a status code of `400`.

Errors can occur for different reasons, such as a missing or invalid token.

If the ID of the ad creative being updated does not exist, the status code will be `404`.

To resolve request errors, refer to the `error_msg` in the response body for more information.

```json
{
  "error": {
    "error_msg": "Invalid value passed for 'type'."
  }
}
```
