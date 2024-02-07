---
sidebar_position: 4
---

# Assignment assumptions

The following assumptions have been made to create these example API docs:

1. I’m using a fake base URL (`https://api.adcreative.com/v1/`) as a placeholder, so these endpoints won't actually work.
2. Since this description didn’t specifically include an endpoint for creating tokens, we’ll assume the user already has a token. The goal of the security section is to explain why the token is necessary and how to use it, rather than how to create it. (Typically, you'd have a `Create a token` endpoint, as well.)
3. `Create an ad creative` accepts an `id` parameter in the request. I’m assuming this is to allow the user to set a custom ID, although it seems unusual to pass the `id` in the request body. (Usually it's just in the response body after the new item is created in your database.)
4. For the `additional_data` array, I’m assuming the values can be any type. This would typically be more defined in the schema though, so in a real-life situation I would ask the engineering team for their specifications.
5. I’ve included cURL and JavaScript examples because cURL commands tend to be quicker to read, but not all developer are comfortable with it. The JavaScript examples are a more typical "real-life" application of the endpoint usage.

# Documenting of choice

I chose [Docusaurus](https://docusaurus.io/) for this assignment for two reasons:

1. I love Docusaurus and think it's a great tool for technical documentation. It's easy to use, provides version control and content staging via git branches (unlike Readme), and allows for code samples.
2. I noticed the client also uses Docusaurus, so it seemed like an obvious choice.
