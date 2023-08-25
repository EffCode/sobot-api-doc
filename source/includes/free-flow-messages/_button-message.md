## Button Message
```shell
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
          "message":"Hello",
          "customer_number":"919970XXXXXX",
          "customer_name": "John Doe",
          "type": "quick_reply",
          "buttons": ["one", "two", "three"],
          "header": "This is a header",
          "caption": "This will go in footer"
}'
```
```python
import requests
import json
url = "https://api.sobot.in/message/"

payload = json.dumps(
  {
          "message":"Hello",
          "customer_number":"919970XXXXXX",
          "customer_name": "John Doe",
          "type": "quick_reply",
          "buttons": ["one", "two", "three"],
          "header": "This is a header",
          "caption": "This will go in footer"
}
)
headers = {
  'x-api-key': 'yourapiaccesskey',
  'x-api-secret': 'yourapisecretkey',
  'content-type': 'application/json'
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
  'x-api-key' => 'yourapiaccesskey',
  'x-api-secret' => 'yourapisecretkey',
  'content-type' => 'application/json'
));
$request->setBody('{\n
          "message":"Hello",\n
          "customer_number":"919970XXXXXX",\n
          "customer_name": "John Doe",\n
          "type": "quick_reply",\n
          "buttons": ["one", "two", "three"], \n
          "header": "This is a header",\n
          "caption": "This will go in footer"
          \n}'
);
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
    "message": "Message sent successfully.",
    "code": 200
}
```
This API allows you to send messages with Buttons (Quick reply) to customers using the Sobot platform, enabling seamless communication with your customer.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Body Parameters

Parameter | Required | Description | Default
--------- | ------- | ----------- | ---------------
message | Yes | The text of the text message which can contain URLs which begin with http:// or https://(All URLs are set to preview in message by default.) and formatting (See Below for formattting options) .<br/> <br/> Maximum length: 1024 characters | -
type | Yes | Type of message contents. Set to ```quick_reply``` in case of Button messages. | -
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | -
customer_name | Yes | Name of a customer for future reference | -
buttons | Yes | Array of strings consist of Title of buttons. You can have up to 3 buttons. It cannot be an empty string and must be unique within the message. Emojis are supported, markdown is not. <br/> <br/>Maximum length: 20 characters for each botton title. | -
header | No | Header content displayed on top of a message. No Emojis. markdown and Links are supported Maximum length: 60 characters.| - 
caption | No | The footer content. Emojis, markdown, and links are supported. Maximum length: 60 characters. | -


WhatsApp allows some formatting in messages. To format all or part of a message, use these formatting symbols:

Formatting     | Symbol                 | Example                     
----------------|------------------------|-----------------------------
Bold | Asterisk (*) | Your total is *$10.50*. 
Italics | Underscore (_) | Welcome to _WhatsApp_! 
Strike-through | Tilde (~) | This is ~better~ best! 

### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.
