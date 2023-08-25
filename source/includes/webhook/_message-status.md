## Message Status Updates
The Sobot Platform sends notifications to inform you of the status of the messages between you and your users. When a message is sent successfully, you receive a notification when the message is sent, delivered, and read. The order of these notifications in your app may not reflect the actual timing of the message status. View the timestamp to determine the timing, if necessary.

### Message Sent Status Payload

```json
{
    "id": "wamid.HBgMOTE5NTYxODc4MDgwFQIAERgSRTUzMjRGMDc2OTIzNjBDRkZGAA==", 
    "status": "sent", 
    "timestamp": "1692947519"
}
```
The following notification is received when a business sends a message as part of a user-initiated conversation: <br/>
```
{
    "id": "wamid.HBgMOTE5NTYxODc4MDgwFQIAERgSRTUzMjRGMDc2OTIzNjBDRkZGAA==", 
    "status": "sent", 
    "timestamp": "1692947519"
}
```


### Message Delivered Status Payload
```json
{
    "id": "wamid.HBgMOTE5NTYxODc4MDgwFQIAERgSRTUzMjRGMDc2OTIzNjBDRkZGAA==", 
    "status": "delivered",
     "timestamp": "1692947519"
}
```
The following notification is received when a business’ message is delivered and that message is part of a user-initiated conversation:<br/>
```
{
    "id": "wamid.HBgMOTE5NTYxODc4MDgwFQIAERgSRTUzMjRGMDc2OTIzNjBDRkZGAA==",
    "status": "delivered",
     "timestamp": "1692947519"
}
```


### Message Read Status Payload

```json
{
    "id": "wamid.HBgMOTE5NTYxODc4MDgwFQIAERgSRTUzMjRGMDc2OTIzNjBDRkZGAA==", 
    "status": "read", 
    "timestamp": "1692947519"
}
```

The following notification is received when a business’ message is read and that message is part of a user-initiated conversation:<br/>
```
{
    "id": "wamid.HBgMOTE5NTYxODc4MDgwFQIAERgSRTUzMjRGMDc2OTIzNjBDRkZGAA==", 
    "status": "read", 
    "timestamp": "1692947519"
}
```