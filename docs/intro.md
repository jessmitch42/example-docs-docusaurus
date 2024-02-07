---
sidebar_position: 1
---

# REST API Introduction

## Overview

Use this REST API to create, update, list, and query ad creatives. These are example docs for a technical assignment and do not represent a usable REST API.

### What is an ad creative?

"Ad creative" refers to the the visual, audio, or text-based elements of an advertisement.

These can include (but are not limited to):

- images
- animations
- text
- videos

_Note: For the purpose of these example docs, we'll limit ad creatives to these four types._

## Usage

To use this REST API, developers can make requests to the `https://api.adcreative.com/v1/` base URL. HTTPS is required for all API requests.

To learn more about how to use each endpoint that is currently available, see the [Endpoints](/docs/category/endpoints) section.

### Supported endpoints

The following endpoints are publicly available to developers.

| HTTP method | Endpoint                                                             |
| ----------- | -------------------------------------------------------------------- |
| `POST`      | [Create an ad creative](/docs/endpoints/create-an-ad-creative)       |
| `POST`      | [Create bulk ad creatives](/docs/endpoints/create-bulk-ad-creatives) |
| `GET`       | [Retrieve ad creatives](/docs/endpoints/retrieve-ad-creative)        |
| `PATCH`     | [Update an ad creative](/docs/endpoints/edit-an-ad-creative)         |
| `POST`      | [Query ad creatives](/docs/endpoints/query-ad-creatives)             |

## Ad creative object

Ad creatives are represented in this API by the "Ad creative object". Retrieved ad creatives will also be returned using this structure.

| Key                 | Type                                                         | Description                                                   | Example                                                                       |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| `id`                | `string`                                                     | A unique ID for the ad creative.                              | `"jyh7"`                                                                      |
| `name`              | `string`                                                     | The ad creative's name.                                       | `"Ad Creative 1"`                                                             |
| `type`              | `string` (`"image"` / `"animation"` / `"text"` / `"video"` ) | The ad creative's type (i.e., it's format).                   | `"text"`                                                                      |
| `content`           | `string`                                                     | Content for the ad creative; either the media source or text. | `"This is some text for an ad"`                                               |
| `additional_data`   | `array` of key (`string`) ⇒ value (any) elements             | Any additional information to note for the ad creative.       | `[{ "example1": 15 },{ "example2": "another value" },{ "example3": false },]` |
| `created_time`      | `string` (ISO date)                                          | A date assigned to the ad creative at the time of creation.   | `'2024-01-31 23:59:59'`                                                       |
| `last_updated_time` | `string` (ISO date)                                          | A date that is set when an ad creative is updated.            | `'2024-01-31 23:59:59'`                                                       |
