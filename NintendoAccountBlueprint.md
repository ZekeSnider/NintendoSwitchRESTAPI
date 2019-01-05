FORMAT: 1A
HOST: https://accounts.nintendo.com

# Nintendo Account API Blueprint

## Session Token [/connect/1.0.0/api/session_token]

### <a name="GetSessionToken"></a> Get session token [POST]
The body of the request should be of type Form URL-Encoded.
The `session_token_code` should be `session_token_code` from the login page's redirect. `session_token_code_verifier` should be `state` from the login page's redirect. `client_id` should be the client id from the URL of your login/authentication page on Nintendo's site.

+ Request (application/json)

	+ Body

		client_id=[client id here]&session_token_code=[session token code here]&session_token_code_verifier=[verifier code here]

+ Response 200 (application/json)
	
	+ Body

		{
		  "code": "codehere",
		  "session_token": "sessiontokenhere"
		}

## Service Token [/connect/1.0.0/api/token]

### <a name="GetServiceToken"></a> Get service token [POST]

`session_token` in body of request should be the `session_token` from the response of [GET /connect/1.0.0/api/session_token](#GetSessionToken). `client_id` should be retrieved from the auth page URL.

+ Request (application/json)
	+ Headers
		Host: accounts.nintendo.com
		Content-Type: application/json; charset=utf-8
		Connection: keep-alive
		User-Agent: OnlineLounge/1.0.4 NASDKAPI iOS
		Accept: application/json
		Accept-Language: en-US
		Accept-Encoding: gzip, deflate
	
	+ Body

		{
			"client_id":"[clientidhere]",
			"grant_type":"urn:ietf:params:oauth:grant-type:jwt-bearer-session-token",
			"session_token":"Nintendo Account Session Token Here"
		}

+ Response 200 (application/json)

	+ Body

		{
		  "token_type": "Bearer",
		  "expires_in": 900,
		  "access_token": "accesstokenhere",
		  "id_token": "idtokenhere",
		  "scope": [
		    "openid",
		    "user",
		    "user.birthday",
		    "user.mii",
		    "user.screenName"
		  ]
		}


## My user details [/2.0.0/users/me]

### Get my user details [GET]

Note: personal information has been redacted from the response body. 

Bearer token is `access_token` from the response of [GET /connect/1.0.0/api/token](#GetServiceToken)

+ Request
	+ Headers

		Host: api.accounts.nintendo.com
		Connection: keep-alive
		Accept: application/json
		User-Agent: OnlineLounge/1.0.4 NASDKAPI iOS
		Accept-Language: en-US
		Authorization: Bearer [Bearer token here]
		Accept-Encoding: gzip, deflate

+ Response 200 (application/json)
	
	+ Body
```json
{
  "region": null,
  "isChild": false,
  "timezone": {
    "name": "America/Los_Angeles",
    "utcOffsetSeconds": -25200,
    "id": "America/Los_Angeles",
    "utcOffset": "-07:00"
  },
  "mii": {
   "clientId": "clientidhere",
    "storeData": {
      "3": "storedatahere"
    },
    "id": "mii_idhere",
    "imageUriTemplate": "https://{imageOrigin}/1.0.0/miis{/id}/image{/etag}.{format}{?type,expression,width,bgColor,clothesColor,cameraXRotate,cameraYRotate,cameraZRotate,characterXRotate,characterYRotate,characterZRotate,lightXDirection,lightYDirection,lightZDirection,lightDirectionMode,splitDepthOffset,splitMode,instanceCount,instanceRotationMode}",
    "imageOrigin": "cdn-mii.accounts.nintendo.com",
    "etag": "etaghere",
    "updatedAt": 1455678671,
    "favoriteColor": "green",
    "type": "profile"
  },
  "clientFriendsOptedIn": true,
  "emailVerified": true,
  "updatedAt": 1488606410,
  "screenName": "censoredemailhere / censoredusernamehere",
  "emailOptedInUpdatedAt": 1455678552,
  "emailOptedIn": true,
  "clientFriendsOptedInUpdatedAt": 0,
  "nickname": "Zeke",
  "eachEmailOptedIn": {
    "survey": {
      "updatedAt": 1494449469,
      "optedIn": true
    },
    "deals": {
      "optedIn": true,
      "updatedAt": 1494449469
    }
  },
  "analyticsOptedInUpdatedAt": 1455678552,
  "country": "US",
  "gender": "male",
  "birthday": "yyyy-mm-dd",
  "id": "idhere",
  "candidateMiis": [
    {
      "updatedAt": 1455678671,
      "favoriteColor": "green",
      "type": "candidate",
      "clientId": "clientidhere",
      "storeData": {
	"3": "storedatahere"
      },
      "id": "idhere",
      "imageUriTemplate": "https://{imageOrigin}/1.0.0/miis{/id}/image{/etag}.{format}{?type,expression,width,bgColor,clothesColor,cameraXRotate,cameraYRotate,cameraZRotate,characterXRotate,characterYRotate,characterZRotate,lightXDirection,lightYDirection,lightZDirection,lightDirectionMode,splitDepthOffset,splitMode,instanceCount,instanceRotationMode}",
      "imageOrigin": "cdn-mii.accounts.nintendo.com",
      "etag": "etaghere"
    },
    {
      "type": "candidate",
      "favoriteColor": "yellowgreen",
      "updatedAt": 1492719363,
      "etag": "etaghere",
      "imageOrigin": "cdn-mii.accounts.nintendo.com",
      "imageUriTemplate": "https://{imageOrigin}/1.0.0/miis{/id}/image{/etag}.{format}{?type,expression,width,bgColor,clothesColor,cameraXRotate,cameraYRotate,cameraZRotate,characterXRotate,characterYRotate,characterZRotate,lightXDirection,lightYDirection,lightZDirection,lightDirectionMode,splitDepthOffset,splitMode,instanceCount,instanceRotationMode}",
      "id": "idhere",
      "storeData": {
	"3": "storedatahere"
      },
      "clientId": "clientidhere"
    }
  ],
  "createdAt": 1455678552,
  "analyticsOptedIn": true,
  "language": "en-US"
}
```
