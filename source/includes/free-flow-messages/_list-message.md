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
