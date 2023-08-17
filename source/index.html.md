---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - python
  - javascript

toc_footers:
  - <a href='#'>Copyright &copy; Sobot 2023</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Sobot API Documentation
Welcome to the Sobot API documentation! Our API allows you to seamlessly integrate the power of the Sobot platform into your applications, enabling you to manage WhatsApp interactions effectively. Sobot is a SaaS platform designed to provide a comprehensive WhatsApp team inbox that facilitates seamless communication with customers, resolution of queries, execution of marketing campaigns, and more.

Whether you're building a customer support tool, enhancing your marketing capabilities, or creating innovative communication solutions, the Sobot API empowers you with a range of operations to interact with the WhatsApp team inbox and harness its features.

## Getting Started
To get started with the Sobot API, you'll need an [Access & Secret Keys](#authentication) that you can [obtain by signing up](https://app.sobot.in/signup) for an account on our platform. Once you have your Access & Secret keys, you can authenticate your requests and start accessing the Sobot API endpoints.

We provide language bindings in several programming languages, including Shell, Python, and JavaScript. In this documentation, you'll find code examples demonstrating API usage in these languages. The code examples are displayed in the dark area to the right, and you can easily switch between programming languages using the tabs in the top right corner of the code examples.

## API Endpoints and Operations
The Sobot API supports a variety of operations that allow you to interact with the WhatsApp team inbox seamlessly. Some of the key operations supported by the API include:

**Add Customer**: You can use this endpoint to add new customers to the WhatsApp team inbox, ensuring that you maintain a comprehensive contact list.

**Initiate Campaigns**: Launch and manage marketing campaigns directly from your application using the API, enabling you to engage with your audience effectively.

**Send Messages**: Send various types of messages, including text, videos, images, and templates, to customers through the WhatsApp team inbox, facilitating efficient communication.

**Create/Sync Templates**: Simplify message creation by utilizing templates. This endpoint allows you to create and synchronize message templates effortlessly.

## Explore and Integrate
This documentation serves as your comprehensive guide to integrating the Sobot API into your applications. You'll find detailed explanations, code examples, and best practices to ensure a smooth integration process.

So, whether you're aiming to enhance customer support, execute marketing strategies, or innovate with WhatsApp communication, the Sobot API equips you with the tools you need. Let's explore the possibilities together!

Feel free to refer to the code examples on this page and select the programming language that suits your development environment. If you have any questions or need assistance, don't hesitate to reach out to our support team.

Let's dive into the world of seamless WhatsApp communication with Sobot API!

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

