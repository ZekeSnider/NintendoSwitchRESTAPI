FORMAT: 1A
HOST: https://api-lp1.znc.srv.nintendo.net

# Nintendo Switch API Blueprint

## Account Login [/v1/Account/Login]

### <a name="LoginAccount"></a> Login to Account [POST]

`naIdToken` is `id_token` from the response of [GET /connect/1.0.0/api/token](#GetServiceToken). `naBirthday` should be the birthday on the account used to login in the specified format.

+ Request

	+ Body
		{
		  "parameter": {
		    "language": "en-US",
		    "naBirthday": "yyyy-mm-dd",
		    "naCountry": "US",
		    "naIdToken": "[tokengoeshere]"
		  }
		}

+ Response 200 (application/json)

	+ Body

		{
		  "result": {
		    "user": {
		      "imageUri": "[userimagehere]",
		      "supportId": "[supportidhere]",
		      "name": "[namehere]",
		      "id": [useridhere]
		    },
		    "firebaseCredential": {
		      "accessToken": "firebasetokenhere",
		      "expiresIn": 3600
		    },
		    "webApiServerCredential": {
		      "accessToken": "webapitokenhere",
		      "expiresIn": 7200
		    }
		  },
		  "status": 0,
		  "correlationId": "61becf03-0ae45082"
		}

## Game List [/v1/Game/ListWebServices]

### <a name="GetGameList"></a> Get game list [GET]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

+ Request
	
	+ Headers

		Host: api-lp1.znc.srv.nintendo.net
		Content-Type: application/json; charset=utf-8
		Content-Length: 0
		Connection: keep-alive
		X-ProductVersion: 1.0.4
		Accept: application/json
		User-Agent: com.nintendo.znca/1.0.4 (iOS/10.3.3)
		Accept-Language: en-us
		X-Platform: iOS
		Authorization: Bearer [Web API Access Token Goes here]

+ Response 200 (application/json)

	+ Body

		{
		  "status": 0,
		  "correlationId": "d02af7dc-bf169f85",
		  "result": [
		    {
		      "whiteList": [
		        "app.splatoon2.nintendo.net"
		      ],
		      "id": 5741031244955648,
		      "uri": "https://app.splatoon2.nintendo.net/",
		      "name": "Splatoon 2",
		      "imageUri": "https://cdn.znc.srv.nintendo.net/gameWebServices/splatoon2/images/usEn/banner.png"
		    }
		  ]
		}

## Game Web Service Token [/v1/Game/GetWebServiceToken]

### <a name="GetGameWebServiceToken"></a> Get Game Web Service Token [POST]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

+ Request (application/json)
	+ Headers
		Host: api-lp1.znc.srv.nintendo.net
		Content-Type: application/json; charset=utf-8
		X-ProductVersion: 1.0.4
		Authorization: Bearer [Web API Access Token Goes here]
		Accept-Language: en-us
		Accept-Encoding: gzip, deflate
		Accept: application/json; charset=utf-8
		User-Agent: com.nintendo.znca/1.0.4 (iOS/10.3.3)
		Connection: keep-alive
		X-Platform: iOS

	+ Body
		{
		  "parameter": {
		    "id": [gameIDgoeshere]
		  }
		}

+ Response 200 (application/json)

	+ Body

		{
		  "result": {
		    "accessToken": "accesstokenwillbehere",
		    "expiresIn": 7200
		  },
		  "status": 0,
		  "correlationId": "d91de63c-f186fb6f"
		}

## Active Event ID [/v1/Event/GetActiveEventId]

### Get Active Event ID [GET]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

I'm not yet sure what this is supposed to be used for, as there is not currently an active event. Maybe this is used for splatfests?

+ Response 200 (application/json)

	+ Body

		{
		  "status": 0,
		  "result": {
		    "eventId": 0
		  },
		  "correlationId": "6c63576e-3e41f536"
		}