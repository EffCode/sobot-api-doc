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
