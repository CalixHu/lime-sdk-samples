# Helplightning SDK Server Samples

A python implementation to demonstrate how to make a call by using helplightning api.  

## Table of Contents
-  [Environment](#environment)
-  [Deploy](#deploy)
-  [Authentication](#authentication)
-  [Create-Session](#create-session)
- [Get-Session-By-PinCode](#Get-Session-By-PinCode)

# Environment

Make sure exports following environments before run the server:
```sh
export HLSERVER_URL=https://api.helplightning.com/
export HLSERVER_ENTERPRISE_ID=0000
export HLSERVER_API_KEY=1234
export HLSERVER_PARTNER_KEY=apikey
```
`HLSERVER_URL` - Helplightning api server url  
`HLSERVER_ENTERPRISE_ID` - Your enterprise id in helplightning  
`HLSERVER_API_KEY` - Your apikey from helplightning  
`HLSERVER_PARTNER_KEY` - Path to a partner key file(*.pem* formart)  

## Deploy
You may need to installs follow python3 libs: `requests, json, jwt`.
Run:
```sh
python3 ./HLServer.py
```
The server will listen on port *:8777*. 
> http://localhost:8777

## Authentication

Both users should authenticate first before making the call.  
Request: `https://localhost:8777/auth?email=your-email@example.com`  
Response:  `{"token": "your-authorized-token"}`  

## Create-Session

You can create a session once you get your user token.
Request: 
```sh
URL: http://localhost:8777/session
Headers: 
{
'Authorization': 'your-user-token', 
'Content-Type': 'application/json; charset=utf-8'
}
Body: {'contact_email: "contact-user-email@example.com'}
```
Response:
```sh
{
"sid": "3271",
"session_id": ["76125039-3a0c-4b3c-bc8c-248566357bd8"],
"session_token": "session-token",
"user_token": "your-user-token",
"url": "gss+ssl://gss.helplightning.net"
}
```
`sid` - A pin code to share with your contact user  
`session-id` - Session id for the call  
`session-token` - Session token for call  
`user-token` - Your user token you want call with

Once you get session data, you can share the pin code(`sid`) to your contact. 
 
## Get-Session-By-PinCode

> Note: This is API will get session data for a contact user only.

Once your contact gets the pin code, they can get the session.

Request: `192.168.2.110:8777/session?sid=3271`
Response:
```sh
{
"sid": "3271",
"session_id": ["76125039-3a0c-4b3c-bc8c-248566357bd8"],
"session_token": "session-token",
"user_token": "contact-user-token",
"url": "gss+ssl://gss.helplightning.net"
}
```