FORMAT: 1A
HOST: https://api-lp1.znc.srv.nintendo.net

# Nintendo Switch API Blueprint

## Account Login [/v1/Account/Login]

This is currenly **[Broken.](https://twitter.com/mattisenhower/status/908460571191795713)**

If you wish to use this API, extract the needed response from your phone using something like [Telerik Fiddler.](http://www.telerik.com/fiddler)

Or, if you wish to use exclusively the [_Splatoon 2 API_](Splatoon2Blueprint.md), extract your iksm_session from a response while on the game specific integration.

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

### <a name="GetGameList"></a> Get game list [POST]

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
	    ```
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
        ```
	+ Body
	    ```json
		{
		  "parameter": {
		    "id": [gameIDgoeshere]
		  }
		}
		```

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

### <a name="GetActiveEventId"></a> Get Active Event ID [GET]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

I think this is used for the current lobby events.

+ Response 200 (application/json)

	+ Body

		{
		  "status": 0,
		  "result": {
		    "eventId": 0
		  },
		  "correlationId": "6c63576e-3e41f536"
		}
		
## Event List [/v1/Event/List]

### <a name="GetEventList"></a> Get all events [POST]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

Obtains all joinable lobbies.

+ Request

    + Headers
    
        ```
        X-ProductVersion: 1.1.0
        X-Platform: Android
        User-Agent: com.nintendo.znca/1.1.0 (Android/7.0)
        Accept: application/json
        Authorization: Bearer [Web API access token]
        Content-Type: application/json; charset=utf-8
        Content-Length: 0
        Host: api-lp1.znc.srv.nintendo.net
        Connection: Keep-Alive
        Accept-Encoding: gzip
        ```
        
+ Response 200 (application/json)

    + Body
        
        ```json
        {
          "correlationId": "499ab925-56d67923",
          "status": 0,
          "result": [
            {
              "allowJoinGameWithoutCoral": false,
              "members": [
                {
                  "isPlaying": false,
                  "isInvited": true,
                  "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/ae160604808ae5ad",
                  "id": 6403160302157824,
                  "name": "Virepri"
                },
                {
                  "isPlaying": true,
                  "isInvited": true,
                  "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/26f4a1e2a08ee69b",
                  "id": 5409588421591040,
                  "name": "TPoS-Shin"
                }
              ],
              "gameStatus": {
                "isClosed": false
              },
              "id": 5714341576835072,
              "passCode": "",
              "shareUri": "https://lounge.nintendo.com/room/DDx46PX1Ck",
              "ownerUserId": 5409588421591040,
              "game": {
                "instructionPageUri": "",
                "minMember": 1,
                "imageUri": "",
                "maxMember": 1,
                "selectedGameMode": {
                  "instructionPageUri": "https://web-lp1.znc.srv.nintendo.net/games/hac-aab6b/gameModes/SalmonRun/howtoJoin/index.html",
                  "minMember": 1,
                  "imageUri": "https://cdn.znc.srv.nintendo.net/games/hac-aab6b/gameModes/SalmonRun/images/usEn/banner.jpg",
                  "maxMember": 1,
                  "id": 5,
                  "name": "Salmon Run",
                  "ogpTitle": "Join {room_name} now!"
                },
                "id": 5741031244955648,
                "voiceChatBackgroundImageUri": "https://cdn.znc.srv.nintendo.net/games/hac-aab6b/voiceChat/background.webp",
                "name": "Splatoon 2",
                "officialSiteUri": "http://www.nintendo.com/games/detail/splatoon-2-switch"
              },
              "description": "",
              "name": "TPoS-Shin's Room"
            }
          ]
        }
        ```
        
## Show Event [/v1/Event/Show]

### <a name="EventShow"></a> [POST]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

+ Request (application/json)

    + Headers
    
        ```
        X-ProductVersion: 1.1.0
        X-Platform: Android
        User-Agent: com.nintendo.znca/1.1.0 (Android/7.0)
        Accept: application/json
        Authorization: Bearer [Web API Access Token]
        Content-Type: application/json; charset=utf-8
        Content-Length: 37
        Host: api-lp1.znc.srv.nintendo.net
        Connection: Keep-Alive
        Accept-Encoding: gzip
        ```
        
    + Body
    
        ```json
        {
          "parameter":{
            "id":5714341576835072
          }
        }
        ```
        
+ Response 200 (application/json)

    + Body
    
        ```json
        {
          "result": {
            "passCode": "",
            "id": 5714341576835072,
            "description": "",
            "ownerUserId": 5409588421591040,
            "shareUri": "https://lounge.nintendo.com/room/DDx46PX1Ck",
            "members": [
              {
                "id": 6403160302157824,
                "name": "Virepri",
                "isPlaying": false,
                "isInvited": true,
                "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/ae160604808ae5ad"
              },
              {
                "id": 5409588421591040,
                "name": "TPoS-Shin",
                "isPlaying": true,
                "isInvited": true,
                "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/26f4a1e2a08ee69b"
              }
            ],
            "allowJoinGameWithoutCoral": false,
            "name": "TPoS-Shin's Room",
            "game": {
              "officialSiteUri": "http://www.nintendo.com/games/detail/splatoon-2-switch",
              "id": 5741031244955648,
              "minMember": 1,
              "imageUri": "",
              "voiceChatBackgroundImageUri": "https://cdn.znc.srv.nintendo.net/games/hac-aab6b/voiceChat/background.webp",
              "instructionPageUri": "",
              "maxMember": 1,
              "selectedGameMode": {
                "id": 5,
                "minMember": 1,
                "imageUri": "https://cdn.znc.srv.nintendo.net/games/hac-aab6b/gameModes/SalmonRun/images/usEn/banner.jpg",
                "name": "Salmon Run",
                "ogpTitle": "Join {room_name} now!",
                "maxMember": 1,
                "instructionPageUri": "https://web-lp1.znc.srv.nintendo.net/games/hac-aab6b/gameModes/SalmonRun/howtoJoin/index.html"
              },
              "name": "Splatoon 2"
            },
            "gameStatus": {
              "isClosed": false
            }
          },
          "correlationId": "4b0d88f2-e642524a",
          "status": 0
        }
        ```
        
## Invite to Event [/v1/Event/Invite]

### <a name="EventInvite"></a> Invite to Event [POST]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

+ Request
    
    + Headers
        
        ```
        X-ProductVersion: 1.1.0
        X-Platform: Android
        User-Agent: com.nintendo.znca/1.1.0 (Android/7.0)
        Accept: application/json
        Authorization: Bearer [Web API Access Token]
        Content-Type: application/json; charset=utf-8
        Content-Length: 71
        Host: api-lp1.znc.srv.nintendo.net
        Connection: Keep-Alive
        Accept-Encoding: gzip
        ```
    
    + Body
    
        ```json
        {
          "parameter": {
            "id": 5123588421058560,
            "users": [
              {
                "id": 5409588421591040
              }
            ]
          }
        }
        ```

+ Response

    + Body
    
        ```json
        {
          "result": {},
          "status": 0,
          "correlationId": "ae0f0cf7-f03bfb4e"
        }
        ```
		
## Register Device [/v1/Notification/RegisterDevice]

### <a name="RegisterDevice"></a> Register device for notifications [POST]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

Device ID is generated in-app. Extract it from this call on your device.

I don't know why you'd use this, either, unless you're the phone.

+ Request (application/json)

    + Headers
    
        ```
        X-ProductVersion: 1.1.0
        X-Platform: Android
        User-Agent: com.nintendo.znca/1.1.0 (Android/7.0)
        Accept: application/json
        Authorization: Bearer [Web API access token]
        Content-Type: application/json
        Content-Length: 190
        Host: api-lp1.znc.srv.nintendo.net
        Connection: Keep-Alive
        Accept-Encoding: gzip
        ```
        
    + Body
    
        ```json
        {
          "parameter": {
            "registrationToken":"[Device ID]"
          }
        }
        ```
        
+ Response 200 (application/json)

    + Body
    
        ```json
        {
          "correlationId":"a7c8abce-e0427bfb",
          "result": {},
          "status":0
        }
        ```
        
## Join VOIP [/v1/Voip/Join]

### <a name="VoipJoin"></a> Join VoIP. [POST]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

Device ID is generated in-app. Extract it from [POST /v1/Notification/RegisterDevice](#RegisterDevice) on your device.

+ Request (application/json)

    + Headers
    
        ```
        X-ProductVersion: 1.1.0
        X-Platform: Android
        User-Agent: com.nintendo.znca/1.1.0 (Android/7.0)
        Accept: application/json
        Authorization: Bearer [Web API Access Token]
        Content-Type: application/json; charset=utf-8
        Content-Length: 230
        Host: api-lp1.znc.srv.nintendo.net
        Connection: Keep-Alive
        Accept-Encoding: gzip
        ```
    
    + Body
    
        ```json
        {
          "parameter": {
            "id": 6088424361558016,
            "deviceIdentifier": "[Device ID]",
            "muteUserIds": null
          }
        }
        ```
        
+ Response 200 (application/json)

    + Body
    
        ```json
        {
          "result": {
            "remoteKeyHex": "a61216832df4c22914c2a976730d399b75cd0f0f247f38f45781945c7cc8",
            "remoteSsrc": 1151231983,
            "localKeyHex": "922509928cb51eb163a4b4feff7339ef1f1b23f23556d4eae161128a6e61",
            "channelId": 0,
            "remotePort": 2001,
            "localSsrc": 685664239,
            "remoteHost": "104.154.86.184"
          },
          "status": 0,
          "correlationId": "bc3021dd-528df2ad"
        }
        ```
        
## Get VOIP configuration [/v1/Voip/GetConfig]

### <a name="VoipGetConfig"></a> Get VoIP configuration [POST]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

+ Request (application/json)

    + Headers
    
        ```
        X-ProductVersion: 1.1.0
        X-Platform: Android
        User-Agent: com.nintendo.znca/1.1.0 (Android/7.0)
        Accept: application/json
        Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJmNDE3ZTF0aWJqcWQ5MWNoOTl1NDlpd3o1c245Y2h5MyIsInN1YiI6NjQwMzE2MDMwMjE1NzgyNCwiaXNzIjoiYXBpLWxwMS56bmMuc3J2Lm5pbnRlbmRvLm5ldCIsImlhdCI6MTUwNzQyNDU4MywidHlwIjoiaWRfdG9rZW4iLCJleHAiOjE1MDc0MzE3ODN9.MHZxeCuV_cWm-9IyXXtmMDiLaS316tPjUg1v6B9aBtg
        Content-Type: application/json; charset=utf-8
        Content-Length: 230
        Host: api-lp1.znc.srv.nintendo.net
        Connection: Keep-Alive
        Accept-Encoding: gzip
        ```
    
    + Body
    
        ```json
        {
          "parameter": {
            "platform": "Android",
            "model": "SM-G935U",
            "product": "hero2qlteue",
            "device": "hero2qlteue",
            "manufacturer": "samsung",
            "versionRelease": "7.0",
            "versionSdkInt": 24
          }
        }
        ```
        
+ Response 200 (application/json)

    + Body
    
        ```json
        {
          "status": 0,
          "correlationId": "d806c612-3f51520f",
          "result": {
            "androidAudioMode": 3,
            "smaec": 1,
            "androidRecordingPreset": 4,
            "smaecEc": true,
            "androidStreamType": 0
          }
        }
        ```
        
## Leave VOIP [/v1/Voip/Leave]

### <a name="VoipLeave"></a> Leave VoIP [POST]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

Device ID is generated in-app. Extract it from [POST /v1/Notification/RegisterDevice](#RegisterDevice) on your device.

ID should be the group ID, obtained via [POST /v1/Event/List](#GetEventList)

+ Request (application/json)

    + Headers
    
        ```
        X-ProductVersion: 1.1.0
        X-Platform: Android
        User-Agent: com.nintendo.znca/1.1.0 (Android/7.0)
        Accept: application/json
        Authorization: Bearer [Web API Access Token]
        Content-Type: application/json; charset=utf-8
        Content-Length: 230
        Host: api-lp1.znc.srv.nintendo.net
        Connection: Keep-Alive
        Accept-Encoding: gzip
        ```
        
    + Body
    
        ```json
        {
          "parameter": {
            "id": 5123588421058560,
            "deviceIdentifier": "[Device ID]"
          }
        }
        ```
        
+ Response 200 (application/json)

    + Body
    
        ```json
        {
          "result": {},
          "status": 0,
          "correlationId": "85906060-9e307e23"
        }
        ```
        
## Obtain friends list [/v1/User/List]

### <a name="GetFriendsList"></a> Obtain Friends List [POST]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

+ Request

    + Headers
    
        ```
        X-ProductVersion: 1.1.0
        X-Platform: Android
        User-Agent: com.nintendo.znca/1.1.0 (Android/7.0)
        Accept: application/json
        Authorization: Bearer [Web API Access Token]
        Content-Type: application/json; charset=utf-8
        Content-Length: 230
        Host: api-lp1.znc.srv.nintendo.net
        Connection: Keep-Alive
        Accept-Encoding: gzip
        ```
        
+ Response 200 (application/json)

    + Body
    
        ```json
        {
          "status": 0,
          "correlationId": "fffa6813-70e8fde9",
          "result": [
            {
              "name": "Virepri",
              "isServiceUser": true,
              "supportId": "0664-9173-0838-4959-9123-9",
              "isFriend": false,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/ae160604808ae5ad",
              "id": 6403160302157824,
              "isFavoriteFriend": false
            },
            {
              "name": "Centzilius",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/3b0937a3e09e6517",
              "id": 6330250325655552,
              "isFavoriteFriend": false
            },
            {
              "name": "TPoS-Shin",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/26f4a1e2a08ee69b",
              "id": 5409588421591040,
              "isFavoriteFriend": false
            },
            {
              "name": "AJ",
              "isServiceUser": false,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/aa25d9cdc3f03350",
              "id": 0,
              "isFavoriteFriend": false
            },
            {
              "name": "Some1CP",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/4a4af58feed30a0e",
              "id": 6612396567166976,
              "isFavoriteFriend": false
            },
            {
              "name": "Atomic",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/b55b17be67346d04",
              "id": 4877687744102400,
              "isFavoriteFriend": true
            },
            {
              "name": "Shags",
              "isServiceUser": false,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/34924d955f2dbe21",
              "id": 0,
              "isFavoriteFriend": false
            },
            {
              "name": "acid treez",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/c8e8ed04dfb82b52",
              "id": 5830558567366656,
              "isFavoriteFriend": false
            },
            {
              "name": "Arsanus",
              "isServiceUser": false,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/1b98b0d3e78dffb0",
              "id": 0,
              "isFavoriteFriend": true
            },
            {
              "name": "Vertsix",
              "isServiceUser": false,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/c1765003c338efc8",
              "id": 0,
              "isFavoriteFriend": false
            },
            {
              "name": "гεd☆sкγε",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/d5152ad313c572d4",
              "id": 5164065190051840,
              "isFavoriteFriend": false
            },
            {
              "name": "King Udyr",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/495508ab65149923",
              "id": 6223255610327040,
              "isFavoriteFriend": false
            },
            {
              "name": "UncleBones",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/8609da5bf75c1ae8",
              "id": 5333171474268160,
              "isFavoriteFriend": true
            },
            {
              "name": "FishPhd",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/fa7ee5bbdd1730be",
              "id": 6208096925908992,
              "isFavoriteFriend": false
            },
            {
              "name": "SillyChip",
              "isServiceUser": false,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/2d62166c88c180a7",
              "id": 0,
              "isFavoriteFriend": true
            },
            {
              "name": "ramtower",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/839f84e45d6c503c",
              "id": 5876604337127424,
              "isFavoriteFriend": true
            },
            {
              "name": "Kev | HDK",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/ec9c900c5bd98a18",
              "id": 5928458282598400,
              "isFavoriteFriend": false
            },
            {
              "name": "Weeee",
              "isServiceUser": false,
              "isFriend": true,
              "lastSeenAt": 0,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/fc40cf8eab622bf4",
              "id": 0,
              "isFavoriteFriend": false
            },
            {
              "name": "Sora",
              "isServiceUser": true,
              "isFriend": true,
              "lastSeenAt": 1506986817,
              "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/ec0cd600097a8dec",
              "id": 6525512310587392,
              "isFavoriteFriend": true
            }
          ]
        }
        ```
        
## Show User Fast [/v1/User/ShowFast]

### <a name="ShowFast"></a> Show User Fast (for VoIP) [POST]

Web API Access Token should be webApiServerCredential["accesstoken"] from [POST /v1/Account/Login](#LoginAccount).

ID should be a user ID

+ Request

    + Headers
    
        ```
        X-ProductVersion: 1.1.0
        X-Platform: Android
        User-Agent: com.nintendo.znca/1.1.0 (Android/7.0)
        Accept: application/json
        Authorization: Bearer [Web API Access Token]
        Content-Type: application/json; charset=utf-8
        Content-Length: 230
        Host: api-lp1.znc.srv.nintendo.net
        Connection: Keep-Alive
        Accept-Encoding: gzip
        ```
        
    + Body
    
        ```json
        {
          "parameter":{
            "id":5409588421591040
          }
        }
        ```
        
+ Response 200 (application/json)

    + Body
    
        ```json
        {
          "result": {
            "id": 5409588421591040,
            "name": "TPoS-Shin",
            "imageUri": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/26f4a1e2a08ee69b"
          },
          "correlationId": "b9917772-b68d5bff",
          "status": 0
        }
        ```