---
sidebar_position: 2
---

# Create bulk ad creatives

### POST `https://api.adcreative.com/v1/ad-creative`

Bulk ad creatives can be created with a single `POST` request to this endpoint.

> 💡 To create a single ad creative, use the [Create ad creatives](./create-bulk-ad-creatives) endpoint.

## Requests

### Body parameters

The body parameters for this `POST` request must include an array of [ad creative objects](./create-bulk-ad-creatives#ad-creative-object) in the body of the request.

| Param             | Type                                                                            | Required | Example                                            |
| ----------------- | ------------------------------------------------------------------------------- | -------- | -------------------------------------------------- |
| Ad creative array | `array` of [ad creative objects](./create-bulk-ad-creatives#ad-creative-object) | yes ✅   | `[<ad-creative-object-1>, <ad-creative-object-2>]` |

#### Ad creative object

| Param             | Type                                                                                         | Required | Example                                                                       |
| ----------------- | -------------------------------------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------- |
| `id`              | `string`                                                                                     | yes ✅   | `"jyh7"`                                                                      |
| `name`            | `string`                                                                                     | yes ✅   | `"Ad Creative 1"  `                                                           |
| `type`            | `string`                                                                                     | yes ✅   | `"text"`                                                                      |
| `content`         | `string`                                                                                     | yes ✅   | `"Here is some text for an ad"`                                               |
| `additional_data` | `array` of `{ key: value }` objects where the key is a `string` and the value is `any` type. | no ❌    | `[{ "example1": 15 },{ "example2": "another value" },{ "example3": false },]` |

### Request examples

#### cURL

```bash
curl -X POST 'https://api.adcreative.com/v1/ad-creative' \
  -H 'Authorization: Bearer '"$X_TOKEN"'' \
  -H "Content-Type: application/json" \
  --data '[
  {
    "id": "jess1",
    "name": "First Ad Creative",
    "type": "image",
    "content": "/images/first_ad_creative.png",
    "additional_data": [
      {
        "client": "Sigma"
      },
    ]
  },
  {
    "id": "bob's example",
    "name": "Second Ad Creative",
    "type": "image",
    "content": "/images/second_ad_creative.png",
  }
  ]'
```

#### JavaScript

```jsx
async function createBulkAdCreatives(adArray) {
  const token = process.env.X_TOKEN;
  const baseURL = "https://api.adcreative.com/v1/ad-creative";
  // (Add client-side data validation for array as needed)

  // Make POST request
  try {
    const response = await fetch(baseURL, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${token}`,
      },
      body: JSON.stringify(adArray),
    });

    return await response.json();
  } catch (error) {
    console.error("Error:", error);
    return error;
  }
}

const data = [
  {
    id: "jess1",
    name: "First Ad Creative",
    type: "image",
    content: "/images/first_ad_creative.png",
    additional_data: [{ client: "TBD" }],
  },
  {
    id: "bob's example",
    name: "Another Ad Creative",
    type: "text",
    content: "Here is some text for an ad!",
  },
];

const newBulkACs = createBulkAdCreatives(data);
```

## Responses

### Success (`200` )

#### Response body

Successful requests will respond with a `200` status code, as well as the array of ad creative objects that were successfully created.

| Field       | Type                                                          |
| ----------- | ------------------------------------------------------------- |
| `"results"` | `array` of [ad creative objects](../intro#ad-creative-object) |

#### Response example

```json
{
  "results": [
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
}
```

### Error (`400`)

Unsuccessful requests will respond with a status code of `400`.

Errors while creating ad creatives can occur for various reasons, such as a missing or invalid field.

For this endpoint, an array of objects will be returned for each ad creative. Ad creatives causing an error include an error message. Refer to the `error_msg` in the response body for more information on the error(s) that occurred.

```json
{
  "error": [
    { "error_msg": null },
    { "error_msg": "Invalid type for id: 'jyH7'." }
  ]
}
```
