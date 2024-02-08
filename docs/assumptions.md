---
sidebar_position: 4
---

# Assignment assumptions

The following assumptions have been made to create these example API docs:

1. I’m using a fake base URL (`https://api.adcreative.com/v1/`) as a placeholder, so these endpoints obviously won't actually work.
2. Since this description didn’t specifically include an endpoint for creating tokens, we’ll assume the user already has a token. The goal of the security section is to explain why the token is necessary and how to use it, rather than how to create it. (Typically, you'd have a `Create a token` endpoint, as well.)
3. The `Create an ad creative` endpoint accepts an `id` parameter in the request body. I’m assuming this is to allow the user to set a custom ID, although it seems unusual to pass the `id` in the request body. It could also be something like a customer ID, but I'll treat it as a unique ID to avoid complicating things. (In my experience, you wouldn't usually pass an ID but would instead receive one in the response body.)
4. Ad creative field types: I'm assuming the types for each field because they aren't included in the assignment.
   - For the `additional_data` array, I’m assuming the values can be any type. This would typically be more defined in the schema, so in a real-life situation I would ask the engineering team for their specifications. I'm also assuming it's the only optional field since the user may not have additional information to add.
   - I'm limiting the `type` field to the following strings: `"image"`, `"animation"`, `"text"`, `"video"`. This would also be predefined in a real-life situation.
5. I’ve included cURL and JavaScript examples because cURL commands tend to be quicker to read, but not all developer are comfortable with them. The JavaScript examples represent a more common "real-world" application of the endpoint usage.
6. I added a `401` error for unauthorized requests.

# Documentating tool of choice

I chose [Docusaurus](https://docusaurus.io/) for this assignment for two reasons:

1. I love Docusaurus and think it's a great tool for technical documentation. It's easy to use, provides version control and content staging via git branches, and allows for code samples.
2. I noticed the client for this role also uses Docusaurus, so it seemed like an obvious choice.

Other possible options were Notion or Readme, but both have trade-offs.
