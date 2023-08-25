## Send Video Message
```shell
curl --location --globoff 'https://api.sobot.in/message/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
          "template_name": "hello_world",
          "template_lang": "en",
          "customer_number":"919970XXXXXX",
          "customer_name": "John Doe",
           "params":[
            {
                "type": "header",
                "parameters":[
                  {
                    "type": "video",
                    "link": "https://example.com/videos/20230625_003239.mp4"
                  }
                ]
            }
          ]
}'
```

```python
import requests
import json
url = "https://api.sobot.in/message/"

payload = json.dumps(
  {
    "template_name": "hello_world",
    "template_lang": "en",
    "customer_number": "919970XXXXXX",
    "customer_name": "John Doe",
    "params":[
            {
                "type": "header",
                "parameters":[
                  {
                    "type": "video",
                    "link": "https://example.com/videos/20230625_003239.mp4"
                  }
                ]
            }
          ]
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
$request->setBody('{
            "template_name": "hello_world",
            "template_lang": "en",
            "customer_number":"919970XXXXXX",
            "customer_name": "John Doe",
            "params":[
            {
                "type": "header",
                "parameters":[
                  {
                    "type": "video",
                    "link": "https://example.com/videos/20230625_003239.mp4"
                  }
                ]
            }
          ]
            }'
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
This API allows you to send Template messages with Video to customers using the Sobot platform, enabling seamless communication with your customer.


### HTTP Request

`POST https://api.sobot.in/message/`

### Body Parameters

Parameter | Required | Description |
--------- | ------- | ----------- | 
template_name | Yes | Specify the name of the template. You can get the name of template from template ```GET``` API. | 
template_lang | Yes | Specify the lang_code of the template that you want to send. e.g. en, en_US, en_GB | 
customer_number | Yes| WhatsApp phone number of the customer you want to send a message to. <br /> <br />No Plus signs (+), hyphens (-), parenthesis ((,)), and spaces are supported in customer phone number. <br /><br /> We highly recommend that you **include country calling code** when sending a message to a customer. If the country calling code is omitted, your business phone number's country calling code is prepended to the customer's phone number. This can result in undelivered or misdelivered messages. | 
customer_name | Yes | Name of a customer for future reference | 
params | Yes | This is a JSON array accepts the single JSON object to specify video as a header for video template. JSON object has two keys: <ul><li>type: In this case ```header```</li> <li>parameters: A nested JSON array holds single object which has following keys: <ul><li>type: for Video header specify ```video``` as a type.</li><li>A public URL of video. Please see below table for supported Media types.</li></ul>

### Supported Media Types
| Media     | Supported Types| Size Limit                                       |
|-----------|----------------|-----------|
| video | video/mp4, video/3gp<br/><br/> Notes: <br/>Only H.264 video codec and AAC audio codec is supported. <br/>We support videos with a single audio stream or no audio stream. | 16MB |


### Response
In response of successfully sent messages, you will get ```id``` & ```status``` under ```data``` key. Messages are identified by a unique ID (```wamid```). You can track message status in the Webhooks through its ```wamid```  (Check Webhook Documentation for recieving Status events of sent messages on your webhook). This ```wamid``` can have a maximum length of up to 128 characters.



