## Adding a Webhook
Before you can start receiving notifications you will need to create an endpoint on your server to receive notifications.

Your endpoint must be able to process HTTPS requests: Event Notifications. Since requests use HTTPs, your server must have a valid TLS or SSL certificate correctly configured and installed. 

Webhooks payloads can be up to 3MB.

### Webhook Delivery Failure
<aside class="warning">
We will send all the webhook notifications only once, irresepctive of your server status or response code. 
</aside>