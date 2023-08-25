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

