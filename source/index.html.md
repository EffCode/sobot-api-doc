---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell: cURL
  - python: Python
  - php: PHP

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

Sobot employs authentication keys to grant access to its API. To acquire a new Sobot API keys, please follow below instructons to obtain keys from our portal.

Sign In to [app.sobot.in](https://app.sobot.in) -> Settings -> Developers tools - > Generate Keys

<aside class="warning">
Every time you will generate the new keys, old keys will be deprecated. 
</aside>

For each API request directed to the server, Sobot requires the API keys to be included in the header. The header should follow this format:

`x-api-key: your-access-key`

`x-api-secret: your-secret-key`

These keys play a crucial role in ensuring the security and validity of API interactions. Please ensure that you incorporate your provided access and secret keys correctly in the headers of your API requests.

<aside class="notice">
You must replace <code>your-access-key</code> & <code>your-secret-key</code> with your personal API keys.
</aside>


# Free-flow Messages

## Text Message

```shell
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: {{api-access-key}}' \
--header 'x-api-secret: {{api-secret-key}}' \
--data '{"message":"Hello","type":"text","customer_number":"919970XXXXXX","customer_name": "John Doe"}'
```

```python
import requests

url = "https://api.sobot.in/message/"

payload = "{\"message\":\"Hello\",\"type\":\"text\",\"customer_number\":\"919970XXXXXX\",\"customer_name\": \"John Doe\"}"
headers = {
  'x-api-key': '{{api-access-key}}',
  'x-api-secret': '{{api-secret-key}}'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.sobot.in/message/');
$request->setMethod(HTTP_Request2::METHOD_POST);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => '{{api-access-key}}',
  'x-api-secret' => '{{api-secret-key}}'
));
$request->setBody('{"message":"Hello","type":"text","customer_number":"919970XXXXXX","customer_name": "John Doe"}');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}

```

> The above API call returns JSON response like this:

```json
{
    "data": {
        "id": "wamid.HBgMOTE5OTcwNTg1NTU2FQIAERgSQjhGRDQ2REFBQjAxMjJBM0Q1AA==",
        "status": "submitted"
    },
    "message": "Notification sent successfully.",
    "code": 200
}
```
This API allows you to send text messages to customers using the Sobot platform, enabling seamless communication with your customer.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Query Parameters

Parameter | Required | Description | Default
--------- | ------- | ----------- | ---------------
message | Yes | The text of the text message which can contain URLs which begin with http:// or https://(All URLs are set to preview in message by default.) and formatting (See Below for formattting options) .<br/> <br/> Maximum length: 4096 characters | -
type | Yes | Type of message contents. Set to ```Text``` in case of Text messages. | -
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | -
customer_name | Yes | Name of a customer for future reference | -


WhatsApp allows some formatting in messages. To format all or part of a message, use these formatting symbols:

Formatting     | Symbol                 | Example                     
----------------|------------------------|-----------------------------
Bold | Asterisk (*) | Your total is *$10.50*. 
Italics | Underscore (_) | Welcome to _WhatsApp_! 
Strike-through | Tilde (~) | This is ~better~ best! 

### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.



## Image Message
```shell
curl --location --globoff '{{base_url}}/message/' \
--header 'x-api-key: {{api-access-key}}' \
--header 'x-api-secret: {{api-secret-key}}' \
--data '{
    "type": "image",
    "url": "https://sobot-assets.s3.amazonaws.com/113367044717422/105445182186358/images/20230625_003239.jpg",
    "customer_number": "919970585556",
    "customer_name": "Sagar",
    "mime_type": "image/jpeg"
}'
```

```python
import requests

url = "{{base_url}}/message/"

payload = "{\n    \"type\": \"image\",\n    \"url\": \"https://sobot-assets.s3.amazonaws.com/113367044717422/105445182186358/images/20230625_003239.jpg\",\n    \"customer_number\": \"919970585556\",\n    \"customer_name\": \"Sagar\",\n    \"mime_type\": \"image/jpeg\"\n}"
headers = {
  'x-api-key': '{{api-access-key}}',
  'x-api-secret': '{{api-secret-key}}'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('{{base_url}}/message/');
$request->setMethod(HTTP_Request2::METHOD_POST);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => '{{api-access-key}}',
  'x-api-secret' => '{{api-secret-key}}'
));
$request->setBody('{\n    "type": "image",\n    "url": "https://sobot-assets.s3.amazonaws.com/113367044717422/105445182186358/images/20230625_003239.jpg",\n    "customer_number": "919970585556",\n    "customer_name": "Sagar",\n    "mime_type": "image/jpeg"\n}');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}

```

> The above API call returns JSON response like this:

```json
{
    "data": {
        "id": "wamid.HBgMOTE5OTcwNTg1NTU2FQIAERgSQjhGRDQ2REFBQjAxMjJBM0Q1AA==",
        "status": "submitted"
    },
    "message": "Notification sent successfully.",
    "code": 200
}
```
This API allows you to send text messages to customers using the Sobot platform, enabling seamless communication with your customer.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Query Parameters

Parameter | Required | Description | Default
--------- | ------- | ----------- | ---------------
message | Yes | The text of the text message which can contain URLs which begin with http:// or https://(All URLs are set to preview in message by default.) and formatting (See Below for formattting options) .<br/> <br/> Maximum length: 4096 characters | -
type | Yes | Type of message contents. Set to ```Text``` in case of Text messages. | -
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | -
customer_name | Yes | Name of a customer for future reference | -


WhatsApp allows some formatting in messages. To format all or part of a message, use these formatting symbols:

Formatting     | Symbol                 | Example                     
----------------|------------------------|-----------------------------
Bold | Asterisk (*) | Your total is *$10.50*. 
Italics | Underscore (_) | Welcome to _WhatsApp_! 
Strike-through | Tilde (~) | This is ~better~ best! 

### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.

## Button Message

# Template
Templates are used in template messages to open marketing, utility, and authentication conversations with customers. Unlike free-form messages, template messages are the only type of message that can be sent to customers who have yet to message you, or who have not sent you a message in the last 24 hours.

Templates must be approved before they can be sent in template messages. In addition, templates may be disabled automatically based on customer feedback. Once disabled, a template cannot be sent in a template message until its quality rating has improved or it no longer violates our business or commerce policies.

## Send Messages

# Template Messages

## Text Message

## Text Message with Buttons

## Text Message with CTA


