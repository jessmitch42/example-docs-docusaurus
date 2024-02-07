---
sidebar_position: 2
---

# Create an ad creative

### POST `https://api.adcreative.com/v1/ad-creative`

A new ad creative can be created with `POST` request to this endpoint.

> To create multiple ad creatives with a single request, see the [Create bulk ad creatives](/docs/endpoints/create-bulk-ad-creatives) endpoint.

## Requests

`POST` requests must include an [ad creative object](/docs/intro#ad-creative-object) that specifies the details of the ad creative being created.

### Body parameters

The body parameters for this `POST` request match the ad creative object, as defined in the [introduction](/docs/intro#ad-creative-object) to these docs.

| Param             | Type                                               | Required | Example                                                                       |
| ----------------- | -------------------------------------------------- | -------- | ----------------------------------------------------------------------------- |
| `id`              | `string`                                           | yes ✅   | `"jyh7"`                                                                      |
| `name`            | `string`                                           | yes ✅   | `"Ad Creative 1"  `                                                           |
| `type`            | `string`                                           | yes ✅   | `"text"`                                                                      |
| `content`         | `string`                                           | yes ✅   | `"Here is some text for an ad"`                                               |
| `additional_data` | `array` of key (`string`) ⇒ value (`any`) elements | no ❌    | `[{ "example1": 15 },{ "example2": "another value" },{ "example3": false },]` |

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

  // return early if required data is not included
  if (!id || !name || !type || !content) {
    // add appropriate error handling
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

Successful requests will respond with a `200` status code, as well as information related to the created ad creative.

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
  "content": "/images/first_ad_creative.png",
  "additional_data": [{ "client": "TBD" }],
  "created_time": "2024-01-31 23:59:59",
  "last_edited_time": "2024-01-31 23:59:59"
}
```

### Error (`400` )

Errors can occur for different reasons, such as a missing or invalid token or required parameter. To resolve request errors, refer to the `error_msg` in the response body for more information.

```json
{
  "error": {
    "error_msg": "Missing required parameters in request. 'name' parameter should be included."
  }
}
```
