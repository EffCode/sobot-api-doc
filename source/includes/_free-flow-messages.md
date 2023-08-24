# Free-flow Messages

## Text Message
```shell
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
          "message":"Hello",
          "type":"text",
          "customer_number":"919970XXXXXX",
          "customer_name": "John Doe"
}'
```

```python
import requests
import json
url = "https://api.sobot.in/message/"

payload = json.dumps(
  {
  "message": "Hello",
  "type": "text",
  "customer_number": "919970XXXXXX",
  "customer_name": "John Doe"
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
$request->setBody('{"message":"Hello",
"type":"text",
"customer_number":"919970XXXXXX",
"customer_name": "John Doe"}'
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
This API allows you to send text messages to customers using the Sobot platform, enabling seamless communication with your customer.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Body Parameters

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
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
    "type": "image",
    "url": "https://example.com/images/20230625_003239.jpg",
    "customer_number": "919970XXXXXX",
    "customer_name": "John Doe",
    "mime_type": "image/jpeg"
}'
```

```python
import requests
import json
url = "https://api.sobot.in/message/"

payload = json.dumps({
  "type": "image",
  "url": "https://example.com/images/20230625_003239.jpg",
  "customer_number": "919970XXXXXX",
  "customer_name": "John Doe",
  "mime_type": "image/jpeg"
})
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
  'x-api-secret' => 'yourapisecretkey'
));
$request->setBody('{\n    
"type": "image",\n    
"url": "https://example.com/images/20230625_003239.jpg",\n    
"customer_number": "919970XXXXXX",\n    
"customer_name": "John Doe",\n    
"mime_type": "image/jpeg"\n}'
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
This API allows you to send image messages to customers using the Sobot platform, enabling seamless communication with your customer.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Body Parameters

Parameter | Required | Description | Default
--------- | ------- | ----------- | ---------------
type | Yes | Type of message contents. Set to ```image``` in case of Image messages. | -
url | Yes | URL of an image you want to send to customer and this image should be publicly accessible. <br /><br /> Please check supported Media Types below.| - 
mime_type | Yes | Mime-type of image that you added in the URL <br /><br /> e.g. image/jpeg, image/png | -
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | -
customer_name | Yes | Name of a customer for future reference | -
caption | No | The text to send along with the image message.<br/> <br/> Maximum length: 1024 characters | -


### Supported Media Types

| Media     | Supported Types| Size Limit |
|-----------|----------------|-----------|
| image | image/jpeg, image/png Images must be 8-bit, RGB or RGBA | 5MB |

### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.


## Sticker Message
```shell
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
    "type": "image",
    "url": "https://example.com/stickers/20230625_003239.webp",
    "customer_number": "919970XXXXXX",
    "customer_name": "John Doe",
    "mime_type": "image/webp"
}'
```

```python
import requests
import json
url = "https://api.sobot.in/message/"

payload = json.dumps({
  "type": "image",
  "url": "https://example.com/stickers/20230625_003239.webp",
  "customer_number": "919970XXXXXX",
  "customer_name": "John Doe",
  "mime_type": "image/webp"
})
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
  'x-api-secret' => 'yourapisecretkey'
));
$request->setBody('{\n    
"type": "image",\n    
"url": "https://example.com/stickers/20230625_003239.webp",\n    
"customer_number": "919970XXXXXX",\n    
"customer_name": "John Doe",\n    
"mime_type": "image/webp"\n}'
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
This API allows you to send sticker messages to customers using the Sobot platform, enabling seamless communication with your customer.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Body Parameters

Parameter | Required | Description | Default
--------- | ------- | ----------- | ---------------
type | Yes | Type of message contents. Set to ```sticker``` in case of Sticker messages. | -
url | Yes | URL of an sticker you want to send to customer and this sticker file should be publicly accessible. <br /><br /> Please check supported Media Types below.| - 
mime_type | Yes | Mime-type of image that you added in the URL <br /><br /> e.g. image/webp | -
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | -
customer_name | Yes | Name of a customer for future reference | -


### Supported Media Types

| Media     | Supported Types| Size Limit                                       |
|-----------|----------------|-----------|
| sticker | image/webp | Static stickers: 100KB<br/><br/> Animated stickers: 500KB |


### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.

## Video Message
```shell
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
    "type": "video",
    "url": "https://example.com/videos/20230625_003239.mp4",
    "customer_number": "919970XXXXXX",
    "customer_name": "John Doe",
    "mime_type": "video/mp4"
}'
```

```python
import requests
import json
url = "https://api.sobot.in/message/"

payload = json.dumps(
  {
  "type": "video",
  "url": "https://example.com/videos/20230625_003239.mp4",
  "customer_number": "919970XXXXXX",
  "customer_name": "John Doe",
  "mime_type": "video/mp4"
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
  'x-api-secret' => 'yourapisecretkey'
));
$request->setBody('{\n    "type": "video",\n    
"url": "https://example.com/videos/20230625_003239.mp4",\n    
"customer_number": "919970XXXXXX",\n    
"customer_name": "John Doe",\n    
"mime_type": "video/mp4"\n}');
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
This API allows you to send video messages to customers using the Sobot platform, enabling seamless communication with your customer.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Body Parameters

Parameter | Required | Description | Default
--------- | ------- | ----------- | ---------------
type | Yes | Type of message contents. Set to ```video``` in case of Video messages. | -
url | Yes | URL of an video you want to send to customer and this video file should be publicly accessible. <br /><br /> Please check supported Media Types below.| - 
mime_type | Yes | Mime-type of image that you added in the URL <br /><br /> e.g. video/mp4, video/3gp | -
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | -
customer_name | Yes | Name of a customer for future reference | -
caption | No | The text to send along with the video message.<br/> <br/> Maximum length: 1024 characters | -


### Supported Media Types

| Media     | Supported Types| Size Limit                                       |
|-----------|----------------|-----------|
| video | video/mp4, video/3gp<br/><br/> Notes: <br/>Only H.264 video codec and AAC audio codec is supported. <br/>We support videos with a single audio stream or no audio stream. | 16MB |

### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.

## Document Message
```shell
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
    "type": "document",
    "url": "https://example.com/documents/20230625_003239.pdf",
    "customer_number": "919970XXXXXX",
    "customer_name": "John Doe",
    "mime_type": "application/pdf",
    "filename": "file.pdf"
}'
```

```python
import requests
import json
url = "https://api.sobot.in/message/"

payload = json.dumps(
  {
  "type": "document",
  "url": "https://example.com/documents/20230625_003239.pdf",
  "customer_number": "919970XXXXXX",
  "customer_name": "John Doe",
  "mime_type": "application/pdf",
  "filename": "file.pdf"
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
  'content-type': 'application/json'
  
));
$request->setBody('{\n    "type": "document",\n    
"url": "https://example.com/documents/20230625_003239.pdf",\n   
 "customer_number": "919970XXXXXX",\n    
 "customer_name": "John Doe",\n    
 "mime_type": "application/pdf",\n    
 "filename": "file.pdf"\n}');
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
This API allows you to send document messages to customers using the Sobot platform, enabling seamless communication with your customer.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Body Parameters

Parameter | Required | Description | Default
--------- | ------- | ----------- | ---------------
type | Yes | Type of message contents. Set to ```document``` in case of document messages. | -
url | Yes | URL of an document you want to send to customer and this document file should be publicly accessible. <br /><br /> Please check supported Media Types below.| - 
mime_type | Yes | Mime-type of image that you added in the URL <br /><br /> e.g. application/pdf, application/msword | -
filename | Yes | Name of a file that you've mentioned in a ```url``` parameter. | -
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | -
customer_name | Yes | Name of a customer for future reference | -
caption | No | The text to send along with the document message.<br/> <br/> Maximum length: 1024 characters | -


### Supported Media Types

| Media     | Supported Types| Size Limit                                       |
|-----------|----------------|-----------|
| document | text/plain, application/pdf, application/vnd.ms-powerpoint, application/msword, application/vnd.ms-excel, application/vnd.openxmlformats-officedocument.wordprocessingml.document, application/vnd.openxmlformats-officedocument.presentationml.presentation, application/vnd.openxmlformats-officedocument.spreadsheetml.sheet | 100MB |


### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.


## Location Message
```shell
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
    "type": "location",
    "customer_number": "919970XXXXXX",
    "customer_name": "John Doe",
    "longitude": "78.272125", 
    "latitude": "13.891411",
    "location_name": "New York, NYC",
    "address": "13, New York Street, NY, US."
}'
```

```python
import requests
import json
url = "https://api.sobot.in/message/"

payload = json.dumps(
  {
    "type": "location",
    "customer_number": "919970XXXXXX",
    "customer_name": "John Doe",
    "longitude": "78.272125", 
    "latitude": "13.891411",
    "location_name": "New York, NYC",
    "address": "13, New York Street, NY, US."
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
  'content-type': 'application/json'
  
));
$request->setBody('{\n    {
    "type": "location",\n
    "customer_number": "919970XXXXXX",\n
    "customer_name": "John Doe",\n
    "longitude": "78.272125",\n
    "latitude": "13.891411",\n
    "location_name": "New York, NYC",\n
    "address": "13, New York Street, NY, US."}\n}');
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
This API allows you to send location messages to customers using the Sobot platform, enabling seamless communication with your customer.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Body Parameters

Parameter | Required | Description | Default
--------- | ------- | ----------- | ---------------
type | Yes | Type of message contents. Set to ```location``` in case of Location messages. | -
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | -
customer_name | Yes | Name of a customer for future reference | -
longitude | Yes | Longitude of the location. | - 
latitude | Yes | Latitude of the location. | -
name | No | Name of the location. | -
Address | No | Only displayed if name is present. | -

### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.

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



## List Message
```shell
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
          "message":"Hello",
          "customer_number":"919970XXXXXX",
          "customer_name": "John Doe",
          "type": "list",
          "header": "This is a header",
          "caption": "This will go in footer",
          "list_obj": {
              "button": "Show List",
              "sections": [
                  {
                      "title": "one",
                      "rows": [
                          {
                              "title": "First title",
                              "id": "id_1",
                              "description": "test description"
                          },
                          {
                              "title": "second title",
                              "id": "id_2",
                              "description": "test description"
                          }
                      ]
                  }
              ]
          }
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
          "header": "This is a header",
          "caption": "This will go in footer",
          "list_obj": {
              "button": "Show List",
              "sections": [
                  {
                      "title": "one",
                      "rows": [
                          {
                              "title": "First title",
                              "id": "id_1",
                              "description": "test description"
                          },
                          {
                              "title": "second title",
                              "id": "id_2",
                              "description": "test description"
                          }
                      ]
                  }
              ]
          }
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
          "header": "This is a header",\n
          "caption": "This will go in footer"
          "list_obj": {\n
              "button": "Show List",\n
              "sections": [\n
                  {\n
                      "title": "one",\n
                      "rows": [\n
                          {\n
                              "title": "First title",\n
                              "id": "id_1",\n
                              "description": "test description"\n
                          },\n
                          {\n
                              "title": "second title",\n
                              "id": "id_2",\n
                              "description": "test description"\n
                          }\n
                      ]\n
                  }\n
              ]\n
          }\n}'
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
This API allows you to send List messages to customers using the Sobot platform, enabling seamless communication with your customer.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Body Parameters

Parameter | Required | Description | Default
--------- | ------- | ----------- | ---------------
message | Yes | The text of the text message which can contain URLs which begin with http:// or https://(All URLs are set to preview in message by default.) and formatting (See Below for formattting options) .<br/> <br/> Maximum length: 1024 characters | - 
type | Yes | Type of message contents. Set to ```list``` in case of List messages. | - 
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | - 
customer_name | Yes | Name of a customer for future reference | - 
list_obj | Yes | A object which consist of following parameters. <table><thead><tr><td>Parameter</td><td>Required</td><td>Description</td><tr><thead><tr><td>button</td><td>Yes</td><td>Text of the button to trigger the List. It cannot be an empty string and must be unique within the message. Emojis are supported, markdown is not. Maximum length: 20 characters.</td></tr><tr><td>sections</td><td>Yes</td><td>Array of section objects. Minimum of 1, maximum of 10. Each section object has two required parameters as follows: <table><tr><td>title</td><td>Title for section. Acts like a separator in the list. Maximum length: 24 characters.</td></tr><tr><td>rows</td><td>Contains a list of rows. You can have a total of 10 rows across your sections. Each row must have a title (Maximum length: 24 characters) and an ID (Maximum length: 200 characters). You can add a description (Maximum length: 72 characters), but it is optional.</td></tr></table></td></tr></table> | - 
header | No | Header content displayed on top of a message. No Emojis. markdown and Links are supported Maximum length: 60 characters.| - 
caption | No | The footer content. Emojis, markdown, and links are supported. Maximum length: 60 characters. | - 


### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.


## Single Product Message
```shell
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
          "message":"Hello",
          "customer_number":"919970XXXXXX",
          "customer_name": "John Doe",
          "type": "product",
          "caption": "This will go in footer",
          "product_list": {"product_retailer_id": "sbt_in_4_1"}       
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
          "type": "product",
          "caption": "This will go in footer",
          "product_list": {"product_retailer_id": "sbt_in_4_1"}       
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
          "type": "product",\n
          "caption": "This will go in footer",\n
          "product_list": {"product_retailer_id": "sbt_in_4_1"}\n}'
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
This API allows you to send Single Product messages to customers using the Sobot platform, enabling seamless communication with your customer.

This API needs Meta catalog to be connected to your WhatsApp business account. The catalog id should be updated in Sobot before using this API. This API uses that catalog id as a default for refering all your products with ```product_retailer_id```.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Body Parameters

Parameter | Required | Description | Default
--------- | ------- | ----------- | ---------------
message | Yes | The text of the text message which can contain URLs which begin with http:// or https://(All URLs are set to preview in message by default.) and formatting (See Below for formattting options) .<br/> <br/> Maximum length: 1024 characters | - 
type | Yes | Type of message contents. Set to ```product``` in case of Single Product messages. | - 
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | - 
customer_name | Yes | Name of a customer for future reference | - 
product_list | Yes | A object which consist of following parameters. <table><thead><tr><td>Parameter</td><td>Required</td><td>Description</td><tr><thead><tr><td>product_retailer_id</td><td>Yes</td><td>Unique identifier of the product in a catalog. To get this ID go to [Meta Commerce Manager](https://business.facebook.com/commerce/) and select your Meta Business account.</td></tr></table> | - 
caption | No | The footer content. Emojis, markdown, and links are supported. Maximum length: 60 characters. | - 


### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.




## Multi-product Message
```shell
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
          "message":"Hello",
          "customer_number":"919970XXXXXX",
          "customer_name": "John Doe",
          "type": "product",
          "header": "This is a header",
          "caption": "This will go in footer",
          "product_list": {
            "sections": [
            {
                    "title": "Cakes",
                    "product_items": [
                        {
                            "product_retailer_id": "sbt_in_4_1"
                        },
                        {
                            "product_retailer_id": "sbt_in_4_2"
                        }
                    ]
                }
            ]
          }       
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
          "type": "product",
          "header": "This is a header",
          "caption": "This will go in footer",
          "product_list": {
            "sections": [
            {
                    "title": "Cakes",
                    "product_items": [
                        {
                            "product_retailer_id": "sbt_in_4_1"
                        },
                        {
                            "product_retailer_id": "sbt_in_4_2"
                        }
                    ]
                }
            ]
          }       
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
          "type": "product",\n
          "header": "This is a header",\n
          "caption": "This will go in footer",\n
          "product_list": {\n
            "sections": [\n
            {\n
                    "title": "Cakes",\n
                    "product_items": [\n
                        {\n
                            "product_retailer_id": "sbt_in_4_1"\n
                        },\n
                        {\n
                            "product_retailer_id": "sbt_in_4_2"\n
                        }\n
                    ]\n
                }\n
            ]\n
          }\n}'
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
This API allows you to send Single Product messages to customers using the Sobot platform, enabling seamless communication with your customer.

This API needs Meta catalog to be connected to your WhatsApp business account. The catalog id should be updated in Sobot before using this API. This API uses that catalog id as a default for refering all your products with ```product_retailer_id```.

<aside class="warning">
You can only send a text message up until 24 hours after receiving a message from the user. If you have not received a message from the user within this time, you will need to start a new conversation by sending a Template message.
</aside>

### HTTP Request

`POST https://api.sobot.in/message/`

### Body Parameters

Parameter | Required | Description | Default
--------- | ------- | ----------- | ---------------
message | Yes | The text of the text message which can contain URLs which begin with http:// or https://(All URLs are set to preview in message by default.) and formatting (See Below for formattting options) .<br/> <br/> Maximum length: 1024 characters | - 
type | Yes | Type of message contents. Set to ```product``` in case of Single Product messages. | - 
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | - 
customer_name | Yes | Name of a customer for future reference | - 
product_list | Yes | A object which consist of following parameters. <table><thead><tr><td>Parameter</td><td>Required</td><td>Description</td></tr><thead><tr><td>sections</td><td>Yes</td><td>Array of section objects. Minimum of 1, maximum of 30. Each section object has two required parameters as follows: <table><tr><td>title</td><td>Title for section. Acts like a separator in the Product List. Maximum length: 24 characters.</td></tr><tr><td>Product Items</td><td>Array of product objects. There is a minimum of 1 product per section and a maximum of 30 products across all sections. Every object consist of single key ```product_retailer_id```. This is a unique identifier of the product in a catalog. To get this ID go to [Meta Commerce Manager](https://business.facebook.com/commerce/) and select your Meta Business account.</td></tr></table></td></tr></table> | - 
header | No | Header content displayed on top of a message. No Emojis. markdown and Links are supported Maximum length: 60 characters.| - 
caption | No | The footer content. Emojis, markdown, and links are supported. Maximum length: 60 characters. | - 


### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.


