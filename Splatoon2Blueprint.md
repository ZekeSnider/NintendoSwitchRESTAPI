FORMAT: 1A
HOST: https://app.splatoon2.nintendo.net

# Splatoon 2 API

Note: I recommend setting the `User-Agent` on all requests to the Splatoon 2 API to the following string to blend in. There doesn't appear to be any checking for this but better safe than sorry. `Mozilla/5.0 (iPhone; CPU iPhone OS 10_3_3 like Mac OS X) AppleWebKit/603.3.8 (KHTML, like Gecko) Mobile/14G60`

# Table of Contents
* Home
	* [Homepage](#GetHomepage)
* Results
	* [Results [GET /api/results]](#GetResults)
	* [Individual Result [GET /api/results/{battle_number}]](#GetIndividualResult)
	* [Single Player [GET /api/records/hero]](#GetSinglePlayerData)
* Misc
	* [Schedules [GET /api/schedules]](#GetSchedule)
	* [Stages [GET /api/data/stages]](#GetStages)
	* [Timeline [GET /api/timeline]](#GetTimeline)
	* [Nickname and icon [GET /api/nickname_and_icon{?id}]](#GetNicknameIcon)
* Festivals
	* [Active Festivals [GET /api/festivals/active]](#GetActiveFestivals)
	* [Individual Festival [GET /api/festivals/{festival_id}/votes]](#GetFestivalVotes)
* Merchandise
	* [Merchandise List [GET /api/onlineshop/merchandises]](#GetMerchandiseList)
	* [Order merchandise [POST /api/onlineshop/order/{item_id}]](#OrderMerchandise)

# Group Home

## Homepage [/]

### <a name="GetHomepage"></a> Get homepage [GET]

This is the main page which loads in the HTML/JS of the web app. This page returns a cookie based on your web service token for Splatoon. You must load this page to retrieve a cookie before making any other requests to the Splatoon API. Your token must be sent in the `X-GameWebToken` header in the request, and the cookie is returned in the `Set-Cookie` header of the response. 

The token should be `accessToken` from [POST /v1/Game/GetWebServiceToken](SwitchBlueprint.md#GetGameWebServiceToken)

+ Request

	+ Headers
		X-GameWebToken: [Token here]

+ Response 200 (text/html)

	+ Headers
		Set-Cookie: [Cookie here]


# Group Result

## Results [/api/results]

### <a name="GetResults"></a> Get last 50 results [GET]

Note: The results array has been truncated from 50 elements to 2 here, for brevity.

+ Request

    + Headers

            Cookie: [Cookie variable here]

+ Response 200 (application/json)
	+ Body

		{
		  "results": [
		    {
		      "other_team_result": {
		        "name": "DEFEAT",
		        "key": "defeat"
		      },
		      "player_result": {
		        "player": {
		          "shoes": {
		            "id": "6003",
		            "thumbnail": "\/images\/shoes\/6564c18c77f9d0dc58a100f4b187bd7612187db5.png",
		            "image": "\/images\/shoes\/061da7c22c1d15acfc3c737383ced1d6f7ba48d8.png",
		            "name": "Blue Moto Boots",
		            "kind": "shoes",
		            "rarity": 2,
		            "brand": {
		              "name": "Rockenberg",
		              "frequent_skill": {
		                "name": "Run Speed Up",
		                "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		                "id": "3"
		              },
		              "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png",
		              "id": "3"
		            }
		          },
		          "head": {
		            "id": "1023",
		            "thumbnail": "\/images\/head\/d4fe25a57bdc9eae61ed20932b56ad89b2bdcdea.png",
		            "image": "\/images\/head\/b911d153004f390fafd4e998fc080a3773ca9167.png",
		            "name": "Jellyvader Cap",
		            "kind": "head",
		            "rarity": 2,
		            "brand": {
		              "id": "7",
		              "image": "\/images\/brand\/8175954b5a7e02b8097dbb484c808c8f39d31f41.png",
		              "name": "Skalop",
		              "frequent_skill": {
		                "name": "Quick Respawn",
		                "id": "8",
		                "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png"
		              }
		            }
		          },
		          "player_rank": 14,
		          "weapon": {
		            "thumbnail": "\/images\/weapon\/3abcd1e1152e6d819bee363311edcf4737d14a45.png",
		            "id": "5030",
		            "image": "\/images\/weapon\/aaead5ff0b63cdcb989b211d649b2552bb3e3a1b.png",
		            "name": "Dualie Squelchers",
		            "sub": {
		              "id": "8",
		              "image_a": "\/images\/sub\/14b4d4ef62e915e87bd7caa8b99fb4e986caea26.png",
		              "name": "Point Sensor",
		              "image_b": "\/images\/sub\/627ae0ea02ab649a7a482ee7ee7ace85ca307f44.png"
		            },
		            "special": {
		              "image_a": "\/images\/special\/e395a50d51459dcee4db62d8d1fbc4bb263bc326.png",
		              "image_b": "\/images\/special\/4819d9d318668bdd5dab248a23397ec351bc5c60.png",
		              "name": "Tenta Missiles",
		              "id": "0"
		            }
		          },
		          "star_rank": 0,
		          "clothes": {
		            "image": "\/images\/clothes\/60e601b160dd7d7a4aecc6ad2a5e51ae2d5b52b7.png",
		            "thumbnail": "\/images\/clothes\/158e48710cb726e94f2a5ac1fdb11c1c29f55ede.png",
		            "id": "10002",
		            "brand": {
		              "frequent_skill": {
		                "name": "Special Saver",
		                "id": "6",
		                "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png"
		              },
		              "name": "Zekko",
		              "id": "4",
		              "image": "\/images\/brand\/f3d01187fd633e7d48d9e4e16ef31da73279293c.png"
		            },
		            "rarity": 1,
		            "kind": "clothes",
		            "name": "Zekko Hoodie"
		          },
		          "principal_id": "3095008c85ee2a64",
		          "udemae": {
		            "s_plus_number": null,
		            "number": 4,
		            "name": "B"
		          },
		          "clothes_skills": {
		            "main": {
		              "name": "Ninja Squid",
		              "image": "\/images\/skill\/f0a99d1ab1a765b992b79610ebdc25b69d88fae9.png",
		              "id": "104"
		            },
		            "subs": [
		              {
		                "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		                "id": "13",
		                "name": "Cold-Blooded"
		              },
		              {
		                "id": "6",
		                "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png",
		                "name": "Special Saver"
		              },
		              null
		            ]
		          },
		          "shoes_skills": {
		            "subs": [
		              {
		                "name": "Bomb Defense Up",
		                "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png",
		                "id": "12"
		              },
		              {
		                "name": "Run Speed Up",
		                "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		                "id": "3"
		              },
		              null
		            ],
		            "main": {
		              "name": "Ink Resistance Up",
		              "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		              "id": "11"
		            }
		          },
		          "nickname": "Zeke",
		          "head_skills": {
		            "subs": [
		              {
		                "name": "Quick Super Jump",
		                "id": "9",
		                "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png"
		              },
		              {
		                "id": "8",
		                "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png",
		                "name": "Quick Respawn"
		              },
		              null
		            ],
		            "main": {
		              "id": "1",
		              "image": "\/images\/skill\/da8ff08954fd5d890fc8bc4dd4cb761e2a33b703.png",
		              "name": "Ink Saver (Sub)"
		            }
		          }
		        },
		        "game_paint_point": 493,
		        "special_count": 1,
		        "sort_score": 4,
		        "assist_count": 1,
		        "kill_count": 5,
		        "death_count": 5
		      },
		      "estimate_gachi_power": 1650,
		      "battle_number": "134",
		      "player_rank": 14,
		      "my_team_result": {
		        "name": "VICTORY",
		        "key": "victory"
		      },
		      "star_rank": 0,
		      "udemae": {
		        "name": "B",
		        "number": 4,
		        "s_plus_number": null
		      },
		      "other_team_count": 0,
		      "start_time": 1501351041,
		      "game_mode": {
		        "name": "Ranked Battle",
		        "key": "gachi"
		      },
		      "elapsed_time": 148,
		      "rule": {
		        "key": "splat_zones",
		        "name": "Splat Zones",
		        "multiline_name": "Splat\nZones"
		      },
		      "type": "gachi",
		      "stage": {
		        "name": "Starfish Mainstage",
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		        "id": "2"
		      },
		      "weapon_paint_point": 7473,
		      "my_team_count": 100
		    },
		    {
		      "other_team_result": {
		        "name": "DEFEAT",
		        "key": "defeat"
		      },
		      "player_result": {
		        "assist_count": 3,
		        "kill_count": 7,
		        "sort_score": 0,
		        "death_count": 3,
		        "game_paint_point": 1200,
		        "player": {
		          "principal_id": "3095008c85ee2a64",
		          "clothes": {
		            "thumbnail": "\/images\/clothes\/9ab52f8bf54a041e934853e40b90c897365e4a1d.png",
		            "id": "10005",
		            "image": "\/images\/clothes\/ac39a75be2c983ed9f815dc791e277df46a0aa27.png",
		            "kind": "clothes",
		            "name": "Grape Hoodie",
		            "brand": {
		              "frequent_skill": {
		                "id": "10",
		                "image": "\/images\/skill\/34e114a50a001778a574f7061039d43e632137b7.png",
		                "name": "Sub Power Up"
		              },
		              "name": "Enperry",
		              "id": "16",
		              "image": "\/images\/brand\/de96243d58e41e928d30290162a6f496033da868.png"
		            },
		            "rarity": 0
		          },
		          "nickname": "Zeke",
		          "head_skills": {
		            "main": {
		              "name": "Swim Speed Up",
		              "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png",
		              "id": "4"
		            },
		            "subs": [
		              {
		                "name": "Quick Super Jump",
		                "id": "9",
		                "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png"
		              },
		              {
		                "name": "Special Power Up",
		                "image": "\/images\/skill\/f20a3e85feeb6b4bb021d28059afd6265cee0b43.png",
		                "id": "7"
		              },
		              null
		            ]
		          },
		          "clothes_skills": {
		            "main": {
		              "id": "8",
		              "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png",
		              "name": "Quick Respawn"
		            },
		            "subs": [
		              {
		                "name": "Run Speed Up",
		                "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		                "id": "3"
		              },
		              null,
		              null
		            ]
		          },
		          "shoes_skills": {
		            "subs": [
		              {
		                "name": "Ink Saver (Sub)",
		                "id": "1",
		                "image": "\/images\/skill\/da8ff08954fd5d890fc8bc4dd4cb761e2a33b703.png"
		              },
		              null,
		              null
		            ],
		            "main": {
		              "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png",
		              "id": "9",
		              "name": "Quick Super Jump"
		            }
		          },
		          "head": {
		            "rarity": 1,
		            "brand": {
		              "image": "\/images\/brand\/154440ecbfb65a22cdb224fac843b02cccbcad03.png",
		              "id": "99",
		              "name": "amiibo"
		            },
		            "name": "Squid Hairclip",
		            "kind": "head",
		            "image": "\/images\/head\/7242a4b5e8b7c097e1676a2adb1b69dd89b3c292.png",
		            "id": "25000",
		            "thumbnail": "\/images\/head\/1a8ff55d9ecdd03674bf4bf38fe90a7cb8200fb1.png"
		          },
		          "player_rank": 11,
		          "shoes": {
		            "id": "3011",
		            "thumbnail": "\/images\/shoes\/c8feed975f89f99eeca267bf10f790e1df1de98e.png",
		            "image": "\/images\/shoes\/a1836036c077b41f3b30c5a2225b1cf4d4f6b77a.png",
		            "name": "Canary Trainers",
		            "kind": "shoes",
		            "rarity": 0,
		            "brand": {
		              "id": "10",
		              "image": "\/images\/brand\/02286fe17bb6bc3f5f13c6b251ddc0a55c44c756.png",
		              "name": "Tentatek",
		              "frequent_skill": {
		                "image": "\/images\/skill\/c14f4471b26e0f918c736b5c17e03212290f4541.png",
		                "id": "2",
		                "name": "Ink Recovery Up"
		              }
		            }
		          },
		          "weapon": {
		            "id": "60",
		            "thumbnail": "\/images\/weapon\/fdcd7cbe806eb84df374ea8f7e074ac9637d4762.png",
		            "image": "\/images\/weapon\/1f2b1db5917ef7a4e62f0e15b8805275e33f2179.png",
		            "name": "N-ZAP '85",
		            "sub": {
		              "image_b": "\/images\/sub\/9d6336b855940f6c8fc82979a972f9f3381c0e65.png",
		              "name": "Suction Bomb",
		              "image_a": "\/images\/sub\/79ec06c8afca6af0e14da4d9941706bb15f9927e.png",
		              "id": "1"
		            },
		            "special": {
		              "id": "1",
		              "image_a": "\/images\/special\/abe458a7d13d855f1b27135ccf3e96f46f1f3d10.png",
		              "image_b": "\/images\/special\/415bf85acb0b0dcc478316332fe86efb1fe4f203.png",
		              "name": "Ink Armor"
		            }
		          },
		          "star_rank": 0
		        },
		        "special_count": 2
		      },
		      "other_team_percentage": 34.1,
		      "start_time": 1500866759,
		      "my_team_percentage": 56.5,
		      "player_rank": 12,
		      "rule": {
		        "name": "Turf War",
		        "multiline_name": "Turf\nWar",
		        "key": "turf_war"
		      },
		      "battle_number": "85",
		      "game_mode": {
		        "key": "regular",
		        "name": "Regular Battle"
		      },
		      "type": "regular",
		      "my_team_result": {
		        "key": "victory",
		        "name": "VICTORY"
		      },
		      "stage": {
		        "name": "Port Mackerel",
		        "id": "7",
		        "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png"
		      },
		      "weapon_paint_point": 14188,
		      "win_meter": 10,
		      "star_rank": 0
		    }
		  ],
		  "unique_id": "16039570077175261768",
		  "summary": {
		    "count": 50,
		    "victory_rate": 0.56,
		    "special_count_average": 0.86,
		    "victory_count": 28,
		    "defeat_count": 22,
		    "kill_count_average": 6,
		    "assist_count_average": 0.8,
		    "death_count_average": 4.26
		  }
		}

## Individual Result [/api/results/{battle_number}]

+ Parameters
    + battle_number - The battle number for the battle which you wish to retrieve. This is returned as "battle_number" in a results array object element from the /api/results endpoint.

### <a name="GetIndividualResult"></a> Get an individual result [GET]

+ Request

    + Headers

            Cookie: [Cookie variable here]

+ Response 200 (application/json)
	
	+ Body

		{
		  "other_team_members": [
		    {
		      "player": {
		        "head": {
		          "name": "Noise Cancelers",
		          "kind": "head",
		          "image": "\/images\/head\/42d2266340450cec63223029ac186c2f85981831.png",
		          "id": "5002",
		          "rarity": 2,
		          "brand": {
		            "id": "5",
		            "image": "\/images\/brand\/b38b99b3358f587efd1613b72a72c9ca9f81f406.png",
		            "name": "Forge",
		            "frequent_skill": {
		              "id": "7",
		              "image": "\/images\/skill\/f20a3e85feeb6b4bb021d28059afd6265cee0b43.png",
		              "name": "Special Power Up"
		            }
		          },
		          "thumbnail": "\/images\/head\/e75fa0dc17abf45255ccb8dfef22f00ac874ad21.png"
		        },
		        "shoes_skills": {
		          "main": {
		            "name": "Quick Super Jump",
		            "id": "9",
		            "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png"
		          },
		          "subs": [
		            {
		              "name": "Ink Saver (Main)",
		              "id": "0",
		              "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png"
		            },
		            {
		              "name": "Bomb Defense Up",
		              "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png",
		              "id": "12"
		            },
		            {
		              "name": "Quick Super Jump",
		              "id": "9",
		              "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png"
		            }
		          ]
		        },
		        "player_rank": 23,
		        "weapon": {
		          "sub": {
		            "image_b": "\/images\/sub\/b13bf755b279af83904892fae01cd98c866dfec7.png",
		            "id": "0",
		            "name": "Splat Bomb",
		            "image_a": "\/images\/sub\/d2eaeec524d28ef315a13f8a9e11dd1039cb78aa.png"
		          },
		          "thumbnail": "\/images\/weapon\/5f519a8b3f436c854dc81ee14bfc3a26aef09ebc.png",
		          "id": "41",
		          "image": "\/images\/weapon\/331d889d8113b794131080c8943e05a3d2c4547d.png",
		          "special": {
		            "id": "8",
		            "image_b": "\/images\/special\/26e8117808ce17dadb0f23943359e5909fef4085.png",
		            "name": "Inkjet",
		            "image_a": "\/images\/special\/9871c82952ed0141be0310ace1942c9f5f66d655.png"
		          },
		          "name": "Tentatek Splattershot"
		        },
		        "clothes_skills": {
		          "main": {
		            "name": "Ink Recovery Up",
		            "id": "2",
		            "image": "\/images\/skill\/c14f4471b26e0f918c736b5c17e03212290f4541.png"
		          },
		          "subs": [
		            {
		              "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		              "id": "13",
		              "name": "Cold-Blooded"
		            },
		            {
		              "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		              "id": "11",
		              "name": "Ink Resistance Up"
		            },
		            {
		              "name": "Ink Saver (Main)",
		              "id": "0",
		              "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png"
		            }
		          ]
		        },
		        "shoes": {
		          "name": "Blue & Black Squidkid IV",
		          "kind": "shoes",
		          "id": "2018",
		          "image": "\/images\/shoes\/49e61b3411ef6709c9e698c43381a60fed91a77d.png",
		          "thumbnail": "\/images\/shoes\/38479bfc49f2b529342b43eec7c22c979f800847.png",
		          "brand": {
		            "name": "Enperry",
		            "frequent_skill": {
		              "name": "Sub Power Up",
		              "id": "10",
		              "image": "\/images\/skill\/34e114a50a001778a574f7061039d43e632137b7.png"
		            },
		            "id": "16",
		            "image": "\/images\/brand\/de96243d58e41e928d30290162a6f496033da868.png"
		          },
		          "rarity": 2
		        },
		        "nickname": "SSong_cw",
		        "star_rank": 0,
		        "clothes": {
		          "id": "5020",
		          "image": "\/images\/clothes\/b59185a2c7f57aaf15fef9d2fd46bbc2b6558ca7.png",
		          "thumbnail": "\/images\/clothes\/2145e986a017dc7954944f40137f8724aea0efc9.png",
		          "brand": {
		            "id": "5",
		            "image": "\/images\/brand\/b38b99b3358f587efd1613b72a72c9ca9f81f406.png",
		            "frequent_skill": {
		              "name": "Special Power Up",
		              "image": "\/images\/skill\/f20a3e85feeb6b4bb021d28059afd6265cee0b43.png",
		              "id": "7"
		            },
		            "name": "Forge"
		          },
		          "rarity": 2,
		          "name": "FA-01 Jacket",
		          "kind": "clothes"
		        },
		        "udemae": {
		          "name": "B+",
		          "s_plus_number": null
		        },
		        "head_skills": {
		          "subs": [
		            {
		              "name": "Ink Saver (Sub)",
		              "id": "1",
		              "image": "\/images\/skill\/da8ff08954fd5d890fc8bc4dd4cb761e2a33b703.png"
		            },
		            {
		              "name": "Ink Saver (Main)",
		              "id": "0",
		              "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png"
		            },
		            {
		              "name": "Ink Recovery Up",
		              "id": "2",
		              "image": "\/images\/skill\/c14f4471b26e0f918c736b5c17e03212290f4541.png"
		            }
		          ],
		          "main": {
		            "name": "Quick Super Jump",
		            "id": "9",
		            "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png"
		          }
		        },
		        "principal_id": "2359beeedf4c8dd6"
		      },
		      "game_paint_point": 481,
		      "kill_count": 5,
		      "special_count": 1,
		      "assist_count": 2,
		      "death_count": 6,
		      "sort_score": -4
		    },
		    {
		      "player": {
		        "weapon": {
		          "thumbnail": "\/images\/weapon\/98282e995fc07e2f2ba6157bcfdc997c5161f309.png",
		          "sub": {
		            "name": "Burst Bomb",
		            "image_a": "\/images\/sub\/5f978ddb4716f0d04fcc737755b0b3d212d5671c.png",
		            "id": "2",
		            "image_b": "\/images\/sub\/0c90dd7487c0c1179e0e6827b8928143cf04e336.png"
		          },
		          "id": "40",
		          "image": "\/images\/weapon\/e1d09fc9502a81c82137c8dcd5a872eb872af697.png",
		          "special": {
		            "image_b": "\/images\/special\/4eb81e00f5d707248879a7c7037d8475716a8045.png",
		            "id": "9",
		            "name": "Splashdown",
		            "image_a": "\/images\/special\/324d41e9582d84101152849bc8c96d6595c9b0ff.png"
		          },
		          "name": "Splattershot"
		        },
		        "shoes_skills": {
		          "subs": [
		            {
		              "id": "13",
		              "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		              "name": "Cold-Blooded"
		            },
		            {
		              "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png",
		              "id": "9",
		              "name": "Quick Super Jump"
		            },
		            {
		              "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png",
		              "id": "0",
		              "name": "Ink Saver (Main)"
		            }
		          ],
		          "main": {
		            "id": "2",
		            "image": "\/images\/skill\/c14f4471b26e0f918c736b5c17e03212290f4541.png",
		            "name": "Ink Recovery Up"
		          }
		        },
		        "head": {
		          "id": "5002",
		          "image": "\/images\/head\/42d2266340450cec63223029ac186c2f85981831.png",
		          "rarity": 2,
		          "brand": {
		            "frequent_skill": {
		              "image": "\/images\/skill\/f20a3e85feeb6b4bb021d28059afd6265cee0b43.png",
		              "id": "7",
		              "name": "Special Power Up"
		            },
		            "name": "Forge",
		            "image": "\/images\/brand\/b38b99b3358f587efd1613b72a72c9ca9f81f406.png",
		            "id": "5"
		          },
		          "thumbnail": "\/images\/head\/e75fa0dc17abf45255ccb8dfef22f00ac874ad21.png",
		          "name": "Noise Cancelers",
		          "kind": "head"
		        },
		        "player_rank": 19,
		        "shoes": {
		          "image": "\/images\/shoes\/640323cc9f8b9048087df6d13fdd5c5d47bafc49.png",
		          "id": "5000",
		          "rarity": 2,
		          "thumbnail": "\/images\/shoes\/269b53b0256617b041caa2e416421697a15f340a.png",
		          "brand": {
		            "id": "9",
		            "image": "\/images\/brand\/80648c6e427eae4d32677797fa1be7c0e253fda5.png",
		            "frequent_skill": {
		              "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png",
		              "id": "12",
		              "name": "Bomb Defense Up"
		            },
		            "name": "Inkline"
		          },
		          "kind": "shoes",
		          "name": "Trail Boots"
		        },
		        "nickname": "Darugis",
		        "clothes_skills": {
		          "main": {
		            "name": "Ability Doubler",
		            "image": "\/images\/skill\/67e4e8ec069dfaec1d732c7fe407a2c73e8e51b8.png",
		            "id": "108"
		          },
		          "subs": [
		            {
		              "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png",
		              "id": "12",
		              "name": "Bomb Defense Up"
		            },
		            {
		              "id": "6",
		              "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png",
		              "name": "Special Saver"
		            },
		            null
		          ]
		        },
		        "star_rank": 0,
		        "udemae": {
		          "name": "B",
		          "s_plus_number": null
		        },
		        "clothes": {
		          "rarity": 2,
		          "brand": {
		            "id": "0",
		            "image": "\/images\/brand\/5547e529d160b188d104e3b68ff4b7566eab9771.png",
		            "name": "SquidForce",
		            "frequent_skill": {
		              "id": "11",
		              "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		              "name": "Ink Resistance Up"
		            }
		          },
		          "thumbnail": "\/images\/clothes\/3690ef3f13e50f138eadcaa7043fd2351825f90a.png",
		          "id": "26000",
		          "image": "\/images\/clothes\/01356e2f6dfbaa2d5a36bd2a45a8b6c7ce0df87f.png",
		          "name": "Splatfest Tee",
		          "kind": "clothes"
		        },
		        "head_skills": {
		          "main": {
		            "name": "Quick Super Jump",
		            "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png",
		            "id": "9"
		          },
		          "subs": [
		            {
		              "id": "7",
		              "image": "\/images\/skill\/f20a3e85feeb6b4bb021d28059afd6265cee0b43.png",
		              "name": "Special Power Up"
		            },
		            {
		              "image": "\/images\/skill\/34e114a50a001778a574f7061039d43e632137b7.png",
		              "id": "10",
		              "name": "Sub Power Up"
		            },
		            {
		              "name": "Special Power Up",
		              "id": "7",
		              "image": "\/images\/skill\/f20a3e85feeb6b4bb021d28059afd6265cee0b43.png"
		            }
		          ]
		        },
		        "principal_id": "4aa6a44bc8598520"
		      },
		      "game_paint_point": 454,
		      "kill_count": 2,
		      "special_count": 2,
		      "assist_count": 1,
		      "death_count": 4,
		      "sort_score": -2
		    },
		    {
		      "special_count": 1,
		      "kill_count": 3,
		      "player": {
		        "weapon": {
		          "thumbnail": "\/images\/weapon\/c1befd17d09a527b66f9d2c8a70849a4969642e4.png",
		          "sub": {
		            "name": "Burst Bomb",
		            "image_a": "\/images\/sub\/5f978ddb4716f0d04fcc737755b0b3d212d5671c.png",
		            "image_b": "\/images\/sub\/0c90dd7487c0c1179e0e6827b8928143cf04e336.png",
		            "id": "2"
		          },
		          "image": "\/images\/weapon\/ad921a57ab1b7721c50873c082bb34591b61021c.png",
		          "id": "3010",
		          "special": {
		            "id": "1",
		            "image_b": "\/images\/special\/415bf85acb0b0dcc478316332fe86efb1fe4f203.png",
		            "image_a": "\/images\/special\/abe458a7d13d855f1b27135ccf3e96f46f1f3d10.png",
		            "name": "Ink Armor"
		          },
		          "name": "Tri-Slosher"
		        },
		        "shoes_skills": {
		          "subs": [
		            {
		              "name": "Run Speed Up",
		              "id": "3",
		              "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png"
		            },
		            {
		              "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		              "id": "3",
		              "name": "Run Speed Up"
		            },
		            null
		          ],
		          "main": {
		            "image": "\/images\/skill\/47a74cd575b25a9de3e3592084ff3870db0cf4e0.png",
		            "id": "110",
		            "name": "Object Shredder"
		          }
		        },
		        "player_rank": 18,
		        "head": {
		          "thumbnail": "\/images\/head\/49ed2086bbc82c6d8b33f20bfbd097e96310d74d.png",
		          "brand": {
		            "id": "5",
		            "image": "\/images\/brand\/b38b99b3358f587efd1613b72a72c9ca9f81f406.png",
		            "frequent_skill": {
		              "name": "Special Power Up",
		              "image": "\/images\/skill\/f20a3e85feeb6b4bb021d28059afd6265cee0b43.png",
		              "id": "7"
		            },
		            "name": "Forge"
		          },
		          "rarity": 2,
		          "image": "\/images\/head\/97589ba283a3fd7c4338bc0aedbda5864c20e991.png",
		          "id": "7007",
		          "name": "Hockey Helmet",
		          "kind": "head"
		        },
		        "shoes": {
		          "name": "Smoky Wingtips",
		          "kind": "shoes",
		          "id": "8006",
		          "image": "\/images\/shoes\/a610208c11cf34fc27fc99bf7adc493e87eb026c.png",
		          "rarity": 2,
		          "thumbnail": "\/images\/shoes\/50b887e3a2c82ccfd841b096014b7d6d2a4ad64e.png",
		          "brand": {
		            "frequent_skill": {
		              "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		              "id": "3",
		              "name": "Run Speed Up"
		            },
		            "name": "Rockenberg",
		            "id": "3",
		            "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png"
		          }
		        },
		        "clothes_skills": {
		          "subs": [
		            {
		              "name": "Bomb Defense Up",
		              "id": "12",
		              "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png"
		            },
		            {
		              "id": "4",
		              "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png",
		              "name": "Swim Speed Up"
		            },
		            null
		          ],
		          "main": {
		            "image": "\/images\/skill\/1378f3963526d7216ec44da35b924b81a8ff6a37.png",
		            "id": "5",
		            "name": "Special Charge Up"
		          }
		        },
		        "nickname": "Tony",
		        "star_rank": 0,
		        "udemae": {
		          "name": "B-",
		          "s_plus_number": null
		        },
		        "clothes": {
		          "kind": "clothes",
		          "name": "Crimson Parashooter",
		          "rarity": 2,
		          "brand": {
		            "name": "Annaki",
		            "frequent_skill": {
		              "name": "Cold-Blooded",
		              "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		              "id": "13"
		            },
		            "id": "15",
		            "image": "\/images\/brand\/0b09659e2770389dcb23d911359175e8686f85f5.png"
		          },
		          "thumbnail": "\/images\/clothes\/02751a777792f60584f11f4593cd2f2dc1b6c223.png",
		          "image": "\/images\/clothes\/22d760a39153dd7dea175e4e67fe70211513a943.png",
		          "id": "8020"
		        },
		        "head_skills": {
		          "subs": [
		            {
		              "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png",
		              "id": "9",
		              "name": "Quick Super Jump"
		            },
		            {
		              "name": "Cold-Blooded",
		              "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		              "id": "13"
		            },
		            {
		              "name": "Ink Saver (Sub)",
		              "id": "1",
		              "image": "\/images\/skill\/da8ff08954fd5d890fc8bc4dd4cb761e2a33b703.png"
		            }
		          ],
		          "main": {
		            "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		            "id": "13",
		            "name": "Cold-Blooded"
		          }
		        },
		        "principal_id": "5cb725eb4039c8eb"
		      },
		      "game_paint_point": 383,
		      "sort_score": -6,
		      "death_count": 4,
		      "assist_count": 1
		    },
		    {
		      "assist_count": 1,
		      "sort_score": 0,
		      "death_count": 3,
		      "game_paint_point": 508,
		      "player": {
		        "shoes_skills": {
		          "subs": [
		            {
		              "name": "Bomb Defense Up",
		              "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png",
		              "id": "12"
		            },
		            {
		              "name": "Ink Recovery Up",
		              "id": "2",
		              "image": "\/images\/skill\/c14f4471b26e0f918c736b5c17e03212290f4541.png"
		            },
		            {
		              "image": "\/images\/skill\/c14f4471b26e0f918c736b5c17e03212290f4541.png",
		              "id": "2",
		              "name": "Ink Recovery Up"
		            }
		          ],
		          "main": {
		            "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png",
		            "id": "12",
		            "name": "Bomb Defense Up"
		          }
		        },
		        "head": {
		          "rarity": 2,
		          "brand": {
		            "name": "Krak-On",
		            "frequent_skill": {
		              "name": "Swim Speed Up",
		              "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png",
		              "id": "4"
		            },
		            "image": "\/images\/brand\/9ac5752790dd6dbdc7a427df95e1bfe89fe318e0.png",
		            "id": "2"
		          },
		          "thumbnail": "\/images\/head\/db22e3da0309ac33028ef78385a9f1f0047e26ae.png",
		          "image": "\/images\/head\/13b7b48cd304d3f56c09006b6e6e6511244673f2.png",
		          "id": "1020",
		          "kind": "head",
		          "name": "Hickory Work Cap"
		        },
		        "player_rank": 24,
		        "weapon": {
		          "thumbnail": "\/images\/weapon\/3abcd1e1152e6d819bee363311edcf4737d14a45.png",
		          "sub": {
		            "id": "8",
		            "image_b": "\/images\/sub\/627ae0ea02ab649a7a482ee7ee7ace85ca307f44.png",
		            "image_a": "\/images\/sub\/14b4d4ef62e915e87bd7caa8b99fb4e986caea26.png",
		            "name": "Point Sensor"
		          },
		          "id": "5030",
		          "image": "\/images\/weapon\/aaead5ff0b63cdcb989b211d649b2552bb3e3a1b.png",
		          "special": {
		            "image_b": "\/images\/special\/4819d9d318668bdd5dab248a23397ec351bc5c60.png",
		            "id": "0",
		            "name": "Tenta Missiles",
		            "image_a": "\/images\/special\/e395a50d51459dcee4db62d8d1fbc4bb263bc326.png"
		          },
		          "name": "Dualie Squelchers"
		        },
		        "star_rank": 0,
		        "shoes": {
		          "brand": {
		            "name": "Tentatek",
		            "frequent_skill": {
		              "name": "Ink Recovery Up",
		              "id": "2",
		              "image": "\/images\/skill\/c14f4471b26e0f918c736b5c17e03212290f4541.png"
		            },
		            "id": "10",
		            "image": "\/images\/brand\/02286fe17bb6bc3f5f13c6b251ddc0a55c44c756.png"
		          },
		          "thumbnail": "\/images\/shoes\/8a851babcb842c5f6ccc445538b148b27e6a9ed3.png",
		          "rarity": 2,
		          "id": "2019",
		          "image": "\/images\/shoes\/b904cbc55f2c3618d5ea48ec8fdedc8d5de12bae.png",
		          "kind": "shoes",
		          "name": "Gray Sea-Slug Hi-Tops"
		        },
		        "nickname": "Alfador",
		        "clothes_skills": {
		          "subs": [
		            null,
		            null,
		            null
		          ],
		          "main": {
		            "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png",
		            "id": "6",
		            "name": "Special Saver"
		          }
		        },
		        "head_skills": {
		          "main": {
		            "name": "Special Power Up",
		            "image": "\/images\/skill\/f20a3e85feeb6b4bb021d28059afd6265cee0b43.png",
		            "id": "7"
		          },
		          "subs": [
		            null,
		            null,
		            null
		          ]
		        },
		        "clothes": {
		          "kind": "clothes",
		          "name": "Shirt & Tie",
		          "id": "8015",
		          "image": "\/images\/clothes\/e394fa214515cde618e3d31204694044e01f9edc.png",
		          "rarity": 2,
		          "thumbnail": "\/images\/clothes\/2cd7613563ede73573b246c03fd315072481036e.png",
		          "brand": {
		            "image": "\/images\/brand\/36bc10db0aa2640c87ad712fc0281515beedcca1.png",
		            "id": "8",
		            "frequent_skill": {
		              "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png",
		              "id": "0",
		              "name": "Ink Saver (Main)"
		            },
		            "name": "Splash Mob"
		          }
		        },
		        "udemae": {
		          "s_plus_number": null,
		          "name": "B+"
		        },
		        "principal_id": "b4c7fc1d13aa1ef6"
		      },
		      "special_count": 2,
		      "kill_count": 4
		    }
		  ],
		  "my_team_result": {
		    "key": "victory",
		    "name": "VICTORY"
		  },
		  "game_mode": {
		    "key": "gachi",
		    "name": "Ranked Battle"
		  },
		  "udemae": {
		    "name": "B",
		    "s_plus_number": null,
		    "number": 4
		  },
		  "type": "gachi",
		  "start_time": 1501351041,
		  "star_rank": 0,
		  "other_team_result": {
		    "name": "DEFEAT",
		    "key": "defeat"
		  },
		  "rule": {
		    "name": "Splat Zones",
		    "key": "splat_zones",
		    "multiline_name": "Splat\nZones"
		  },
		  "battle_number": "134",
		  "other_team_count": 0,
		  "stage": {
		    "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		    "id": "2",
		    "name": "Starfish Mainstage"
		  },
		  "elapsed_time": 148,
		  "estimate_gachi_power": 1650,
		  "my_team_members": [
		    {
		      "death_count": 3,
		      "sort_score": 0,
		      "assist_count": 0,
		      "kill_count": 7,
		      "special_count": 1,
		      "player": {
		        "principal_id": "dbce1468972ed657",
		        "clothes": {
		          "thumbnail": "\/images\/clothes\/068dce2c45cc7f0fd2ff0ed1ccdad3236cf72df4.png",
		          "brand": {
		            "frequent_skill": {
		              "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		              "id": "13",
		              "name": "Cold-Blooded"
		            },
		            "name": "Toni Kensa",
		            "image": "\/images\/brand\/4b05e494bf9a547b4d625fd52dcdd930a6c4defc.png",
		            "id": "17"
		          },
		          "rarity": 1,
		          "id": "8019",
		          "image": "\/images\/clothes\/0329e61e9aed350a26fe07159af9886d5f4f77e8.png",
		          "name": "Inkfall Shirt",
		          "kind": "clothes"
		        },
		        "udemae": {
		          "s_plus_number": null,
		          "name": "B-"
		        },
		        "head_skills": {
		          "subs": [
		            {
		              "id": "6",
		              "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png",
		              "name": "Special Saver"
		            },
		            null,
		            null
		          ],
		          "main": {
		            "name": "Last-Ditch Effort",
		            "id": "101",
		            "image": "\/images\/skill\/03d1b1e0221fc82d0ab26cb8cd3f5f40107b6190.png"
		          }
		        },
		        "clothes_skills": {
		          "subs": [
		            {
		              "name": "Ink Resistance Up",
		              "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		              "id": "11"
		            },
		            {
		              "name": "Quick Respawn",
		              "id": "8",
		              "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png"
		            },
		            null
		          ],
		          "main": {
		            "name": "Special Charge Up",
		            "id": "5",
		            "image": "\/images\/skill\/1378f3963526d7216ec44da35b924b81a8ff6a37.png"
		          }
		        },
		        "shoes": {
		          "kind": "shoes",
		          "name": "Hunter Hi-Tops",
		          "rarity": 0,
		          "thumbnail": "\/images\/shoes\/f3017c34185d47fb4eac8ff4fcb5ec321e2d284f.png",
		          "brand": {
		            "frequent_skill": {
		              "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png",
		              "id": "4",
		              "name": "Swim Speed Up"
		            },
		            "name": "Krak-On",
		            "image": "\/images\/brand\/9ac5752790dd6dbdc7a427df95e1bfe89fe318e0.png",
		            "id": "2"
		          },
		          "image": "\/images\/shoes\/5f04689e57f34d59d84ff3afd889c1bd67d7132d.png",
		          "id": "2004"
		        },
		        "nickname": "Kreid",
		        "star_rank": 0,
		        "shoes_skills": {
		          "main": {
		            "id": "2",
		            "image": "\/images\/skill\/c14f4471b26e0f918c736b5c17e03212290f4541.png",
		            "name": "Ink Recovery Up"
		          },
		          "subs": [
		            {
		              "id": "4",
		              "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png",
		              "name": "Swim Speed Up"
		            },
		            null,
		            null
		          ]
		        },
		        "player_rank": 20,
		        "head": {
		          "thumbnail": "\/images\/head\/52167beabbd015ced7d85ffc8cae786c03930f90.png",
		          "brand": {
		            "image": "\/images\/brand\/f3d01187fd633e7d48d9e4e16ef31da73279293c.png",
		            "id": "4",
		            "name": "Zekko",
		            "frequent_skill": {
		              "name": "Special Saver",
		              "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png",
		              "id": "6"
		            }
		          },
		          "rarity": 0,
		          "id": "3003",
		          "image": "\/images\/head\/b7d978444e664a6e42858dfb2b7980b107a7eb98.png",
		          "kind": "head",
		          "name": "Tinted Shades"
		        },
		        "weapon": {
		          "name": "Tentatek Splattershot",
		          "special": {
		            "name": "Inkjet",
		            "image_a": "\/images\/special\/9871c82952ed0141be0310ace1942c9f5f66d655.png",
		            "id": "8",
		            "image_b": "\/images\/special\/26e8117808ce17dadb0f23943359e5909fef4085.png"
		          },
		          "image": "\/images\/weapon\/331d889d8113b794131080c8943e05a3d2c4547d.png",
		          "id": "41",
		          "thumbnail": "\/images\/weapon\/5f519a8b3f436c854dc81ee14bfc3a26aef09ebc.png",
		          "sub": {
		            "name": "Splat Bomb",
		            "image_a": "\/images\/sub\/d2eaeec524d28ef315a13f8a9e11dd1039cb78aa.png",
		            "image_b": "\/images\/sub\/b13bf755b279af83904892fae01cd98c866dfec7.png",
		            "id": "0"
		          }
		        }
		      },
		      "game_paint_point": 609
		    },
		    {
		      "game_paint_point": 559,
		      "player": {
		        "shoes": {
		          "name": "LE Soccer Shoes",
		          "kind": "shoes",
		          "thumbnail": "\/images\/shoes\/d5cb1a718b4cec352682fe6de2eb0b1fea6147cc.png",
		          "brand": {
		            "name": "Takoroka",
		            "frequent_skill": {
		              "name": "Special Charge Up",
		              "id": "5",
		              "image": "\/images\/skill\/1378f3963526d7216ec44da35b924b81a8ff6a37.png"
		            },
		            "image": "\/images\/brand\/eab05d2d502cf953b4ae034c87e52e8c999339d6.png",
		            "id": "11"
		          },
		          "rarity": 2,
		          "image": "\/images\/shoes\/fb557c06c8c3218fc0ed258b0097a9acdf78e383.png",
		          "id": "1011"
		        },
		        "clothes_skills": {
		          "main": {
		            "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		            "id": "13",
		            "name": "Cold-Blooded"
		          },
		          "subs": [
		            {
		              "name": "Sub Power Up",
		              "id": "10",
		              "image": "\/images\/skill\/34e114a50a001778a574f7061039d43e632137b7.png"
		            },
		            {
		              "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png",
		              "id": "0",
		              "name": "Ink Saver (Main)"
		            },
		            {
		              "name": "Special Charge Up",
		              "image": "\/images\/skill\/1378f3963526d7216ec44da35b924b81a8ff6a37.png",
		              "id": "5"
		            }
		          ]
		        },
		        "nickname": "Aiden",
		        "star_rank": 0,
		        "weapon": {
		          "image": "\/images\/weapon\/df04ddaf086cea94491df553a6d2550230a4da3c.png",
		          "id": "50",
		          "sub": {
		            "id": "8",
		            "image_b": "\/images\/sub\/627ae0ea02ab649a7a482ee7ee7ace85ca307f44.png",
		            "image_a": "\/images\/sub\/14b4d4ef62e915e87bd7caa8b99fb4e986caea26.png",
		            "name": "Point Sensor"
		          },
		          "thumbnail": "\/images\/weapon\/3e69eaa1b1463689ddbe4fe23661f007dc216b08.png",
		          "name": ".52 Gal",
		          "special": {
		            "image_b": "\/images\/special\/caf32476e5010e27a4ef9923dbe323978b1d7510.png",
		            "id": "11",
		            "image_a": "\/images\/special\/3e9cd3e60367fbe82d6237a10fdc826d695b9fa0.png",
		            "name": "Baller"
		          }
		        },
		        "shoes_skills": {
		          "main": {
		            "name": "Ink Resistance Up",
		            "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		            "id": "11"
		          },
		          "subs": [
		            {
		              "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png",
		              "id": "9",
		              "name": "Quick Super Jump"
		            },
		            {
		              "id": "5",
		              "image": "\/images\/skill\/1378f3963526d7216ec44da35b924b81a8ff6a37.png",
		              "name": "Special Charge Up"
		            },
		            {
		              "image": "\/images\/skill\/34e114a50a001778a574f7061039d43e632137b7.png",
		              "id": "10",
		              "name": "Sub Power Up"
		            }
		          ]
		        },
		        "player_rank": 17,
		        "head": {
		          "id": "8001",
		          "image": "\/images\/head\/55203e23af837493032f29408acae2d8c5536da9.png",
		          "brand": {
		            "id": "5",
		            "image": "\/images\/brand\/b38b99b3358f587efd1613b72a72c9ca9f81f406.png",
		            "frequent_skill": {
		              "name": "Special Power Up",
		              "image": "\/images\/skill\/f20a3e85feeb6b4bb021d28059afd6265cee0b43.png",
		              "id": "7"
		            },
		            "name": "Forge"
		          },
		          "thumbnail": "\/images\/head\/41fa2be96416df12953fe57726a1161ed7979d94.png",
		          "rarity": 2,
		          "kind": "head",
		          "name": "Paintball Mask"
		        },
		        "principal_id": "86b5bfa0941c6236",
		        "udemae": {
		          "s_plus_number": null,
		          "name": "B+"
		        },
		        "clothes": {
		          "name": "Takoroka Windcrusher",
		          "kind": "clothes",
		          "id": "5018",
		          "image": "\/images\/clothes\/c9a4515bb6cbd433d1996b585826876ebb0ed500.png",
		          "thumbnail": "\/images\/clothes\/43932e8f460247ea0ef7b59654753062fd1dcf59.png",
		          "brand": {
		            "image": "\/images\/brand\/eab05d2d502cf953b4ae034c87e52e8c999339d6.png",
		            "id": "11",
		            "frequent_skill": {
		              "id": "5",
		              "image": "\/images\/skill\/1378f3963526d7216ec44da35b924b81a8ff6a37.png",
		              "name": "Special Charge Up"
		            },
		            "name": "Takoroka"
		          },
		          "rarity": 2
		        },
		        "head_skills": {
		          "subs": [
		            {
		              "name": "Ink Saver (Main)",
		              "id": "0",
		              "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png"
		            },
		            {
		              "image": "\/images\/skill\/f20a3e85feeb6b4bb021d28059afd6265cee0b43.png",
		              "id": "7",
		              "name": "Special Power Up"
		            },
		            {
		              "image": "\/images\/skill\/f20a3e85feeb6b4bb021d28059afd6265cee0b43.png",
		              "id": "7",
		              "name": "Special Power Up"
		            }
		          ],
		          "main": {
		            "name": "Comeback",
		            "image": "\/images\/skill\/bdc5135874439cf3169d9a54b3f1fbdba3731b34.png",
		            "id": "103"
		          }
		        }
		      },
		      "kill_count": 2,
		      "special_count": 2,
		      "assist_count": 3,
		      "death_count": 4,
		      "sort_score": 0
		    },
		    {
		      "special_count": 2,
		      "kill_count": 2,
		      "player": {
		        "shoes": {
		          "kind": "shoes",
		          "name": "Hunting Boots",
		          "thumbnail": "\/images\/shoes\/01ec0d91527fd71fd81b4c9146972af8fc5212fb.png",
		          "brand": {
		            "frequent_skill": {
		              "id": "0",
		              "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png",
		              "name": "Ink Saver (Main)"
		            },
		            "name": "Splash Mob",
		            "id": "8",
		            "image": "\/images\/brand\/36bc10db0aa2640c87ad712fc0281515beedcca1.png"
		          },
		          "rarity": 2,
		          "image": "\/images\/shoes\/8dc67befb3158733c963c78e0d3205adb2245987.png",
		          "id": "6012"
		        },
		        "clothes_skills": {
		          "main": {
		            "id": "108",
		            "image": "\/images\/skill\/67e4e8ec069dfaec1d732c7fe407a2c73e8e51b8.png",
		            "name": "Ability Doubler"
		          },
		          "subs": [
		            {
		              "name": "Ink Resistance Up",
		              "id": "11",
		              "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png"
		            },
		            {
		              "name": "Ink Resistance Up",
		              "id": "11",
		              "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png"
		            },
		            null
		          ]
		        },
		        "nickname": "Jersca",
		        "star_rank": 0,
		        "shoes_skills": {
		          "subs": [
		            {
		              "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		              "id": "13",
		              "name": "Cold-Blooded"
		            },
		            {
		              "name": "Sub Power Up",
		              "id": "10",
		              "image": "\/images\/skill\/34e114a50a001778a574f7061039d43e632137b7.png"
		            },
		            {
		              "name": "Swim Speed Up",
		              "id": "4",
		              "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png"
		            }
		          ],
		          "main": {
		            "image": "\/images\/skill\/8a3f06a972689b094f762626ff36b3db8ee545b5.png",
		            "id": "109",
		            "name": "Stealth Jump"
		          }
		        },
		        "head": {
		          "rarity": 2,
		          "thumbnail": "\/images\/head\/4c6b2cd5775b542fc95cbfda5989e01b571403c4.png",
		          "brand": {
		            "image": "\/images\/brand\/0b09659e2770389dcb23d911359175e8686f85f5.png",
		            "id": "15",
		            "name": "Annaki",
		            "frequent_skill": {
		              "id": "13",
		              "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		              "name": "Cold-Blooded"
		            }
		          },
		          "id": "2009",
		          "image": "\/images\/head\/5cc610a4ba00ed1a43a280e64dffc09bf6fe2889.png",
		          "kind": "head",
		          "name": "Annaki Beret"
		        },
		        "player_rank": 19,
		        "weapon": {
		          "sub": {
		            "image_a": "\/images\/sub\/7d58593453b479138bca576ea13c19b870059ce9.png",
		            "name": "Toxic Mist",
		            "image_b": "\/images\/sub\/9ab41340bfcef91125430d18015ccf98985efdb6.png",
		            "id": "7"
		          },
		          "thumbnail": "\/images\/weapon\/2ec8112dc3b29c82869810743473655f4427e65a.png",
		          "id": "90",
		          "image": "\/images\/weapon\/007fb7ed50e76dde495ffb0747421b50dfce8aa3.png",
		          "name": "Jet Squelcher",
		          "special": {
		            "id": "0",
		            "image_b": "\/images\/special\/4819d9d318668bdd5dab248a23397ec351bc5c60.png",
		            "name": "Tenta Missiles",
		            "image_a": "\/images\/special\/e395a50d51459dcee4db62d8d1fbc4bb263bc326.png"
		          }
		        },
		        "principal_id": "1db880f3c63d9318",
		        "clothes": {
		          "id": "26000",
		          "image": "\/images\/clothes\/01356e2f6dfbaa2d5a36bd2a45a8b6c7ce0df87f.png",
		          "thumbnail": "\/images\/clothes\/3690ef3f13e50f138eadcaa7043fd2351825f90a.png",
		          "brand": {
		            "id": "0",
		            "image": "\/images\/brand\/5547e529d160b188d104e3b68ff4b7566eab9771.png",
		            "frequent_skill": {
		              "name": "Ink Resistance Up",
		              "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		              "id": "11"
		            },
		            "name": "SquidForce"
		          },
		          "rarity": 2,
		          "name": "Splatfest Tee",
		          "kind": "clothes"
		        },
		        "udemae": {
		          "s_plus_number": null,
		          "name": "B"
		        },
		        "head_skills": {
		          "subs": [
		            {
		              "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		              "id": "13",
		              "name": "Cold-Blooded"
		            },
		            {
		              "name": "Cold-Blooded",
		              "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		              "id": "13"
		            },
		            null
		          ],
		          "main": {
		            "id": "5",
		            "image": "\/images\/skill\/1378f3963526d7216ec44da35b924b81a8ff6a37.png",
		            "name": "Special Charge Up"
		          }
		        }
		      },
		      "game_paint_point": 383,
		      "sort_score": 0,
		      "death_count": 2,
		      "assist_count": 3
		    }
		  ],
		  "player_rank": 14,
		  "player_result": {
		    "kill_count": 5,
		    "special_count": 1,
		    "game_paint_point": 493,
		    "player": {
		      "star_rank": 0,
		      "clothes_skills": {
		        "main": {
		          "id": "104",
		          "image": "\/images\/skill\/f0a99d1ab1a765b992b79610ebdc25b69d88fae9.png",
		          "name": "Ninja Squid"
		        },
		        "subs": [
		          {
		            "id": "13",
		            "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		            "name": "Cold-Blooded"
		          },
		          {
		            "name": "Special Saver",
		            "id": "6",
		            "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png"
		          },
		          null
		        ]
		      },
		      "shoes": {
		        "rarity": 2,
		        "thumbnail": "\/images\/shoes\/6564c18c77f9d0dc58a100f4b187bd7612187db5.png",
		        "brand": {
		          "id": "3",
		          "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png",
		          "name": "Rockenberg",
		          "frequent_skill": {
		            "id": "3",
		            "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		            "name": "Run Speed Up"
		          }
		        },
		        "image": "\/images\/shoes\/061da7c22c1d15acfc3c737383ced1d6f7ba48d8.png",
		        "id": "6003",
		        "kind": "shoes",
		        "name": "Blue Moto Boots"
		      },
		      "nickname": "Zeke",
		      "weapon": {
		        "sub": {
		          "image_a": "\/images\/sub\/14b4d4ef62e915e87bd7caa8b99fb4e986caea26.png",
		          "name": "Point Sensor",
		          "id": "8",
		          "image_b": "\/images\/sub\/627ae0ea02ab649a7a482ee7ee7ace85ca307f44.png"
		        },
		        "thumbnail": "\/images\/weapon\/3abcd1e1152e6d819bee363311edcf4737d14a45.png",
		        "image": "\/images\/weapon\/aaead5ff0b63cdcb989b211d649b2552bb3e3a1b.png",
		        "id": "5030",
		        "name": "Dualie Squelchers",
		        "special": {
		          "id": "0",
		          "image_b": "\/images\/special\/4819d9d318668bdd5dab248a23397ec351bc5c60.png",
		          "name": "Tenta Missiles",
		          "image_a": "\/images\/special\/e395a50d51459dcee4db62d8d1fbc4bb263bc326.png"
		        }
		      },
		      "player_rank": 14,
		      "shoes_skills": {
		        "main": {
		          "id": "11",
		          "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		          "name": "Ink Resistance Up"
		        },
		        "subs": [
		          {
		            "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png",
		            "id": "12",
		            "name": "Bomb Defense Up"
		          },
		          {
		            "name": "Run Speed Up",
		            "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		            "id": "3"
		          },
		          null
		        ]
		      },
		      "head": {
		        "brand": {
		          "name": "Skalop",
		          "frequent_skill": {
		            "id": "8",
		            "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png",
		            "name": "Quick Respawn"
		          },
		          "id": "7",
		          "image": "\/images\/brand\/8175954b5a7e02b8097dbb484c808c8f39d31f41.png"
		        },
		        "thumbnail": "\/images\/head\/d4fe25a57bdc9eae61ed20932b56ad89b2bdcdea.png",
		        "rarity": 2,
		        "image": "\/images\/head\/b911d153004f390fafd4e998fc080a3773ca9167.png",
		        "id": "1023",
		        "name": "Jellyvader Cap",
		        "kind": "head"
		      },
		      "principal_id": "3095008c85ee2a64",
		      "head_skills": {
		        "subs": [
		          {
		            "name": "Quick Super Jump",
		            "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png",
		            "id": "9"
		          },
		          {
		            "id": "8",
		            "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png",
		            "name": "Quick Respawn"
		          },
		          null
		        ],
		        "main": {
		          "name": "Ink Saver (Sub)",
		          "id": "1",
		          "image": "\/images\/skill\/da8ff08954fd5d890fc8bc4dd4cb761e2a33b703.png"
		        }
		      },
		      "udemae": {
		        "name": "B",
		        "number": 4,
		        "s_plus_number": null
		      },
		      "clothes": {
		        "id": "10002",
		        "image": "\/images\/clothes\/60e601b160dd7d7a4aecc6ad2a5e51ae2d5b52b7.png",
		        "brand": {
		          "image": "\/images\/brand\/f3d01187fd633e7d48d9e4e16ef31da73279293c.png",
		          "id": "4",
		          "frequent_skill": {
		            "name": "Special Saver",
		            "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png",
		            "id": "6"
		          },
		          "name": "Zekko"
		        },
		        "thumbnail": "\/images\/clothes\/158e48710cb726e94f2a5ac1fdb11c1c29f55ede.png",
		        "rarity": 1,
		        "name": "Zekko Hoodie",
		        "kind": "clothes"
		      }
		    },
		    "death_count": 5,
		    "sort_score": 4,
		    "assist_count": 1
		  },
		  "weapon_paint_point": 7473,
		  "my_team_count": 100
		}


## Hero [/api/records/hero]

### <a name="GetSinglePlayerData"></a> Get Single Player Data [GET]

+ Request

    + Headers

            Cookie: [Cookie variable here]

+ Response 200 (application/json)

	+ Body

		{
		  "stage_infos": [
		    
		  ],
		  "summary": {
		    "clear_rate": 0,
		    "weapon_cleared_info": {
		      
		    },
		    "honor": {
		      "name": "Squidbeak Recruit",
		      "code": "title0"
		    }
		  },
		  "weapon_map": {
		    
		  }
		}


# Group Misc

## Schedules [/api/schedules]

### <a name="GetSchedule"></a> Get map schedule [GET]

+ Request

    + Headers

            Cookie: [Cookie variable here]

+ Response 200 (application/json)

	+ Body

		{
		  "league": [
		    {
		      "id": 4.7809526839201e+18,
		      "end_time": 1501394400,
		      "start_time": 1501387200,
		      "game_mode": {
		        "key": "league",
		        "name": "League Battle"
		      },
		      "stage_a": {
		        "name": "Sturgeon Shipyard",
		        "id": "3",
		        "image": "\/images\/stage\/bc794e337900afd763f8a88359f83df5679ddf12.png"
		      },
		      "rule": {
		        "multiline_name": "Splat\nZones",
		        "name": "Splat Zones",
		        "key": "splat_zones"
		      },
		      "stage_b": {
		        "id": "7",
		        "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png",
		        "name": "Port Mackerel"
		      }
		    },
		    {
		      "game_mode": {
		        "key": "league",
		        "name": "League Battle"
		      },
		      "start_time": 1501394400,
		      "end_time": 1501401600,
		      "id": 4.7809526839201e+18,
		      "stage_b": {
		        "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png",
		        "id": "8",
		        "name": "Moray Towers"
		      },
		      "rule": {
		        "key": "tower_control",
		        "name": "Tower Control",
		        "multiline_name": "Tower\nControl"
		      },
		      "stage_a": {
		        "name": "Musselforge Fitness",
		        "id": "1",
		        "image": "\/images\/stage\/83acec875a5bb19418d7b87d5df4ba1e38ceac66.png"
		      }
		    },
		    {
		      "stage_a": {
		        "name": "Humpback Pump Track",
		        "id": "5",
		        "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png"
		      },
		      "rule": {
		        "multiline_name": "Rainmaker",
		        "name": "Rainmaker",
		        "key": "rainmaker"
		      },
		      "stage_b": {
		        "image": "\/images\/stage\/bc794e337900afd763f8a88359f83df5679ddf12.png",
		        "id": "3",
		        "name": "Sturgeon Shipyard"
		      },
		      "id": 4.7809526839201e+18,
		      "end_time": 1501408800,
		      "start_time": 1501401600,
		      "game_mode": {
		        "key": "league",
		        "name": "League Battle"
		      }
		    },
		    {
		      "game_mode": {
		        "key": "league",
		        "name": "League Battle"
		      },
		      "start_time": 1501408800,
		      "end_time": 1501416000,
		      "id": 4.7809526839201e+18,
		      "stage_b": {
		        "id": "8",
		        "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png",
		        "name": "Moray Towers"
		      },
		      "rule": {
		        "multiline_name": "Splat\nZones",
		        "name": "Splat Zones",
		        "key": "splat_zones"
		      },
		      "stage_a": {
		        "id": "4",
		        "image": "\/images\/stage\/5c030a505ee57c889d3e5268a4b10c1f1f37880a.png",
		        "name": "Inkblot Art Academy"
		      }
		    },
		    {
		      "id": 4.7809526839201e+18,
		      "start_time": 1501416000,
		      "game_mode": {
		        "key": "league",
		        "name": "League Battle"
		      },
		      "end_time": 1501423200,
		      "rule": {
		        "multiline_name": "Tower\nControl",
		        "name": "Tower Control",
		        "key": "tower_control"
		      },
		      "stage_a": {
		        "name": "Port Mackerel",
		        "id": "7",
		        "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png"
		      },
		      "stage_b": {
		        "name": "Starfish Mainstage",
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		        "id": "2"
		      }
		    },
		    {
		      "stage_a": {
		        "image": "\/images\/stage\/98baf21c0366ce6e03299e2326fe6d27a7582dce.png",
		        "id": "0",
		        "name": "The Reef"
		      },
		      "rule": {
		        "key": "rainmaker",
		        "name": "Rainmaker",
		        "multiline_name": "Rainmaker"
		      },
		      "stage_b": {
		        "name": "Inkblot Art Academy",
		        "image": "\/images\/stage\/5c030a505ee57c889d3e5268a4b10c1f1f37880a.png",
		        "id": "4"
		      },
		      "id": 4.7809526839201e+18,
		      "end_time": 1501430400,
		      "game_mode": {
		        "name": "League Battle",
		        "key": "league"
		      },
		      "start_time": 1501423200
		    },
		    {
		      "id": 4.7809526839201e+18,
		      "end_time": 1501437600,
		      "start_time": 1501430400,
		      "game_mode": {
		        "name": "League Battle",
		        "key": "league"
		      },
		      "stage_a": {
		        "image": "\/images\/stage\/bc794e337900afd763f8a88359f83df5679ddf12.png",
		        "id": "3",
		        "name": "Sturgeon Shipyard"
		      },
		      "rule": {
		        "name": "Tower Control",
		        "multiline_name": "Tower\nControl",
		        "key": "tower_control"
		      },
		      "stage_b": {
		        "name": "Starfish Mainstage",
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		        "id": "2"
		      }
		    },
		    {
		      "stage_b": {
		        "name": "Humpback Pump Track",
		        "id": "5",
		        "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png"
		      },
		      "rule": {
		        "multiline_name": "Splat\nZones",
		        "name": "Splat Zones",
		        "key": "splat_zones"
		      },
		      "stage_a": {
		        "name": "Musselforge Fitness",
		        "image": "\/images\/stage\/83acec875a5bb19418d7b87d5df4ba1e38ceac66.png",
		        "id": "1"
		      },
		      "game_mode": {
		        "key": "league",
		        "name": "League Battle"
		      },
		      "start_time": 1501437600,
		      "end_time": 1501444800,
		      "id": 4.7809526839201e+18
		    },
		    {
		      "rule": {
		        "multiline_name": "Rainmaker",
		        "name": "Rainmaker",
		        "key": "rainmaker"
		      },
		      "stage_a": {
		        "id": "2",
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		        "name": "Starfish Mainstage"
		      },
		      "stage_b": {
		        "id": "0",
		        "image": "\/images\/stage\/98baf21c0366ce6e03299e2326fe6d27a7582dce.png",
		        "name": "The Reef"
		      },
		      "id": 4.7809526839201e+18,
		      "start_time": 1501444800,
		      "game_mode": {
		        "key": "league",
		        "name": "League Battle"
		      },
		      "end_time": 1501452000
		    },
		    {
		      "id": 4.7809526839201e+18,
		      "game_mode": {
		        "name": "League Battle",
		        "key": "league"
		      },
		      "start_time": 1501452000,
		      "end_time": 1501459200,
		      "rule": {
		        "name": "Tower Control",
		        "multiline_name": "Tower\nControl",
		        "key": "tower_control"
		      },
		      "stage_a": {
		        "id": "4",
		        "image": "\/images\/stage\/5c030a505ee57c889d3e5268a4b10c1f1f37880a.png",
		        "name": "Inkblot Art Academy"
		      },
		      "stage_b": {
		        "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png",
		        "id": "5",
		        "name": "Humpback Pump Track"
		      }
		    },
		    {
		      "stage_a": {
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		        "id": "2",
		        "name": "Starfish Mainstage"
		      },
		      "rule": {
		        "key": "splat_zones",
		        "name": "Splat Zones",
		        "multiline_name": "Splat\nZones"
		      },
		      "stage_b": {
		        "id": "8",
		        "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png",
		        "name": "Moray Towers"
		      },
		      "id": 4.7809526839201e+18,
		      "end_time": 1501466400,
		      "game_mode": {
		        "name": "League Battle",
		        "key": "league"
		      },
		      "start_time": 1501459200
		    },
		    {
		      "rule": {
		        "key": "tower_control",
		        "multiline_name": "Tower\nControl",
		        "name": "Tower Control"
		      },
		      "stage_a": {
		        "name": "Port Mackerel",
		        "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png",
		        "id": "7"
		      },
		      "stage_b": {
		        "name": "Musselforge Fitness",
		        "image": "\/images\/stage\/83acec875a5bb19418d7b87d5df4ba1e38ceac66.png",
		        "id": "1"
		      },
		      "id": 4.7809526839201e+18,
		      "start_time": 1501466400,
		      "game_mode": {
		        "key": "league",
		        "name": "League Battle"
		      },
		      "end_time": 1501473600
		    }
		  ],
		  "regular": [
		    {
		      "id": 4.7809526839201e+18,
		      "game_mode": {
		        "key": "regular",
		        "name": "Regular Battle"
		      },
		      "start_time": 1501387200,
		      "end_time": 1501394400,
		      "rule": {
		        "multiline_name": "Turf\nWar",
		        "name": "Turf War",
		        "key": "turf_war"
		      },
		      "stage_a": {
		        "image": "\/images\/stage\/98baf21c0366ce6e03299e2326fe6d27a7582dce.png",
		        "id": "0",
		        "name": "The Reef"
		      },
		      "stage_b": {
		        "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png",
		        "id": "8",
		        "name": "Moray Towers"
		      }
		    },
		    {
		      "stage_a": {
		        "name": "Sturgeon Shipyard",
		        "image": "\/images\/stage\/bc794e337900afd763f8a88359f83df5679ddf12.png",
		        "id": "3"
		      },
		      "rule": {
		        "key": "turf_war",
		        "multiline_name": "Turf\nWar",
		        "name": "Turf War"
		      },
		      "stage_b": {
		        "id": "2",
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		        "name": "Starfish Mainstage"
		      },
		      "id": 4.7809526839201e+18,
		      "end_time": 1501401600,
		      "start_time": 1501394400,
		      "game_mode": {
		        "name": "Regular Battle",
		        "key": "regular"
		      }
		    },
		    {
		      "id": 4.7809526839201e+18,
		      "end_time": 1501408800,
		      "game_mode": {
		        "name": "Regular Battle",
		        "key": "regular"
		      },
		      "start_time": 1501401600,
		      "stage_a": {
		        "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png",
		        "id": "7",
		        "name": "Port Mackerel"
		      },
		      "rule": {
		        "name": "Turf War",
		        "multiline_name": "Turf\nWar",
		        "key": "turf_war"
		      },
		      "stage_b": {
		        "id": "1",
		        "image": "\/images\/stage\/83acec875a5bb19418d7b87d5df4ba1e38ceac66.png",
		        "name": "Musselforge Fitness"
		      }
		    },
		    {
		      "id": 4.7809526839201e+18,
		      "start_time": 1501408800,
		      "game_mode": {
		        "name": "Regular Battle",
		        "key": "regular"
		      },
		      "end_time": 1501416000,
		      "rule": {
		        "multiline_name": "Turf\nWar",
		        "name": "Turf War",
		        "key": "turf_war"
		      },
		      "stage_a": {
		        "name": "Humpback Pump Track",
		        "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png",
		        "id": "5"
		      },
		      "stage_b": {
		        "name": "Starfish Mainstage",
		        "id": "2",
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png"
		      }
		    },
		    {
		      "stage_b": {
		        "id": "3",
		        "image": "\/images\/stage\/bc794e337900afd763f8a88359f83df5679ddf12.png",
		        "name": "Sturgeon Shipyard"
		      },
		      "rule": {
		        "multiline_name": "Turf\nWar",
		        "name": "Turf War",
		        "key": "turf_war"
		      },
		      "stage_a": {
		        "id": "8",
		        "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png",
		        "name": "Moray Towers"
		      },
		      "game_mode": {
		        "name": "Regular Battle",
		        "key": "regular"
		      },
		      "start_time": 1501416000,
		      "end_time": 1501423200,
		      "id": 4.7809526839201e+18
		    },
		    {
		      "id": 4.7809526839201e+18,
		      "start_time": 1501423200,
		      "game_mode": {
		        "name": "Regular Battle",
		        "key": "regular"
		      },
		      "end_time": 1501430400,
		      "rule": {
		        "key": "turf_war",
		        "name": "Turf War",
		        "multiline_name": "Turf\nWar"
		      },
		      "stage_a": {
		        "name": "Musselforge Fitness",
		        "id": "1",
		        "image": "\/images\/stage\/83acec875a5bb19418d7b87d5df4ba1e38ceac66.png"
		      },
		      "stage_b": {
		        "id": "5",
		        "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png",
		        "name": "Humpback Pump Track"
		      }
		    },
		    {
		      "rule": {
		        "multiline_name": "Turf\nWar",
		        "name": "Turf War",
		        "key": "turf_war"
		      },
		      "stage_a": {
		        "name": "The Reef",
		        "image": "\/images\/stage\/98baf21c0366ce6e03299e2326fe6d27a7582dce.png",
		        "id": "0"
		      },
		      "stage_b": {
		        "id": "7",
		        "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png",
		        "name": "Port Mackerel"
		      },
		      "id": 4.7809526839201e+18,
		      "game_mode": {
		        "name": "Regular Battle",
		        "key": "regular"
		      },
		      "start_time": 1501430400,
		      "end_time": 1501437600
		    },
		    {
		      "game_mode": {
		        "key": "regular",
		        "name": "Regular Battle"
		      },
		      "start_time": 1501437600,
		      "end_time": 1501444800,
		      "id": 4.7809526839201e+18,
		      "stage_b": {
		        "name": "Moray Towers",
		        "id": "8",
		        "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png"
		      },
		      "rule": {
		        "name": "Turf War",
		        "multiline_name": "Turf\nWar",
		        "key": "turf_war"
		      },
		      "stage_a": {
		        "name": "Inkblot Art Academy",
		        "id": "4",
		        "image": "\/images\/stage\/5c030a505ee57c889d3e5268a4b10c1f1f37880a.png"
		      }
		    },
		    {
		      "stage_b": {
		        "id": "1",
		        "image": "\/images\/stage\/83acec875a5bb19418d7b87d5df4ba1e38ceac66.png",
		        "name": "Musselforge Fitness"
		      },
		      "rule": {
		        "key": "turf_war",
		        "multiline_name": "Turf\nWar",
		        "name": "Turf War"
		      },
		      "stage_a": {
		        "name": "Sturgeon Shipyard",
		        "id": "3",
		        "image": "\/images\/stage\/bc794e337900afd763f8a88359f83df5679ddf12.png"
		      },
		      "start_time": 1501444800,
		      "game_mode": {
		        "key": "regular",
		        "name": "Regular Battle"
		      },
		      "end_time": 1501452000,
		      "id": 4.7809526839201e+18
		    },
		    {
		      "id": 4.7809526839201e+18,
		      "game_mode": {
		        "key": "regular",
		        "name": "Regular Battle"
		      },
		      "start_time": 1501452000,
		      "end_time": 1501459200,
		      "rule": {
		        "name": "Turf War",
		        "multiline_name": "Turf\nWar",
		        "key": "turf_war"
		      },
		      "stage_a": {
		        "name": "Port Mackerel",
		        "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png",
		        "id": "7"
		      },
		      "stage_b": {
		        "name": "Moray Towers",
		        "id": "8",
		        "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png"
		      }
		    },
		    {
		      "game_mode": {
		        "name": "Regular Battle",
		        "key": "regular"
		      },
		      "start_time": 1501459200,
		      "end_time": 1501466400,
		      "id": 4.7809526839201e+18,
		      "stage_b": {
		        "name": "The Reef",
		        "image": "\/images\/stage\/98baf21c0366ce6e03299e2326fe6d27a7582dce.png",
		        "id": "0"
		      },
		      "rule": {
		        "key": "turf_war",
		        "name": "Turf War",
		        "multiline_name": "Turf\nWar"
		      },
		      "stage_a": {
		        "name": "Humpback Pump Track",
		        "id": "5",
		        "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png"
		      }
		    },
		    {
		      "stage_a": {
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		        "id": "2",
		        "name": "Starfish Mainstage"
		      },
		      "rule": {
		        "multiline_name": "Turf\nWar",
		        "name": "Turf War",
		        "key": "turf_war"
		      },
		      "stage_b": {
		        "image": "\/images\/stage\/5c030a505ee57c889d3e5268a4b10c1f1f37880a.png",
		        "id": "4",
		        "name": "Inkblot Art Academy"
		      },
		      "id": 4.7809526839201e+18,
		      "end_time": 1501473600,
		      "game_mode": {
		        "name": "Regular Battle",
		        "key": "regular"
		      },
		      "start_time": 1501466400
		    }
		  ],
		  "gachi": [
		    {
		      "stage_b": {
		        "id": "1",
		        "image": "\/images\/stage\/83acec875a5bb19418d7b87d5df4ba1e38ceac66.png",
		        "name": "Musselforge Fitness"
		      },
		      "stage_a": {
		        "name": "Starfish Mainstage",
		        "id": "2",
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png"
		      },
		      "rule": {
		        "multiline_name": "Tower\nControl",
		        "name": "Tower Control",
		        "key": "tower_control"
		      },
		      "end_time": 1501394400,
		      "game_mode": {
		        "key": "gachi",
		        "name": "Ranked Battle"
		      },
		      "start_time": 1501387200,
		      "id": 4.7809526839201e+18
		    },
		    {
		      "rule": {
		        "multiline_name": "Rainmaker",
		        "name": "Rainmaker",
		        "key": "rainmaker"
		      },
		      "stage_a": {
		        "id": "5",
		        "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png",
		        "name": "Humpback Pump Track"
		      },
		      "stage_b": {
		        "name": "Port Mackerel",
		        "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png",
		        "id": "7"
		      },
		      "id": 4.7809526839201e+18,
		      "start_time": 1501394400,
		      "game_mode": {
		        "key": "gachi",
		        "name": "Ranked Battle"
		      },
		      "end_time": 1501401600
		    },
		    {
		      "stage_b": {
		        "id": "4",
		        "image": "\/images\/stage\/5c030a505ee57c889d3e5268a4b10c1f1f37880a.png",
		        "name": "Inkblot Art Academy"
		      },
		      "rule": {
		        "name": "Splat Zones",
		        "multiline_name": "Splat\nZones",
		        "key": "splat_zones"
		      },
		      "stage_a": {
		        "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png",
		        "id": "8",
		        "name": "Moray Towers"
		      },
		      "game_mode": {
		        "key": "gachi",
		        "name": "Ranked Battle"
		      },
		      "start_time": 1501401600,
		      "end_time": 1501408800,
		      "id": 4.7809526839201e+18
		    },
		    {
		      "id": 4.7809526839201e+18,
		      "game_mode": {
		        "key": "gachi",
		        "name": "Ranked Battle"
		      },
		      "start_time": 1501408800,
		      "end_time": 1501416000,
		      "rule": {
		        "name": "Tower Control",
		        "multiline_name": "Tower\nControl",
		        "key": "tower_control"
		      },
		      "stage_a": {
		        "image": "\/images\/stage\/bc794e337900afd763f8a88359f83df5679ddf12.png",
		        "id": "3",
		        "name": "Sturgeon Shipyard"
		      },
		      "stage_b": {
		        "image": "\/images\/stage\/98baf21c0366ce6e03299e2326fe6d27a7582dce.png",
		        "id": "0",
		        "name": "The Reef"
		      }
		    },
		    {
		      "stage_b": {
		        "id": "4",
		        "image": "\/images\/stage\/5c030a505ee57c889d3e5268a4b10c1f1f37880a.png",
		        "name": "Inkblot Art Academy"
		      },
		      "rule": {
		        "key": "rainmaker",
		        "multiline_name": "Rainmaker",
		        "name": "Rainmaker"
		      },
		      "stage_a": {
		        "name": "Musselforge Fitness",
		        "id": "1",
		        "image": "\/images\/stage\/83acec875a5bb19418d7b87d5df4ba1e38ceac66.png"
		      },
		      "start_time": 1501416000,
		      "game_mode": {
		        "key": "gachi",
		        "name": "Ranked Battle"
		      },
		      "end_time": 1501423200,
		      "id": 4.7809526839201e+18
		    },
		    {
		      "id": 4.7809526839201e+18,
		      "game_mode": {
		        "key": "gachi",
		        "name": "Ranked Battle"
		      },
		      "start_time": 1501423200,
		      "end_time": 1501430400,
		      "rule": {
		        "multiline_name": "Tower\nControl",
		        "name": "Tower Control",
		        "key": "tower_control"
		      },
		      "stage_a": {
		        "name": "Port Mackerel",
		        "id": "7",
		        "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png"
		      },
		      "stage_b": {
		        "id": "2",
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		        "name": "Starfish Mainstage"
		      }
		    },
		    {
		      "stage_b": {
		        "name": "Moray Towers",
		        "id": "8",
		        "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png"
		      },
		      "rule": {
		        "key": "splat_zones",
		        "multiline_name": "Splat\nZones",
		        "name": "Splat Zones"
		      },
		      "stage_a": {
		        "name": "Humpback Pump Track",
		        "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png",
		        "id": "5"
		      },
		      "start_time": 1501430400,
		      "game_mode": {
		        "key": "gachi",
		        "name": "Ranked Battle"
		      },
		      "end_time": 1501437600,
		      "id": 4.7809526839201e+18
		    },
		    {
		      "id": 4.7809526839201e+18,
		      "game_mode": {
		        "name": "Ranked Battle",
		        "key": "gachi"
		      },
		      "start_time": 1501437600,
		      "end_time": 1501444800,
		      "rule": {
		        "multiline_name": "Rainmaker",
		        "name": "Rainmaker",
		        "key": "rainmaker"
		      },
		      "stage_a": {
		        "id": "3",
		        "image": "\/images\/stage\/bc794e337900afd763f8a88359f83df5679ddf12.png",
		        "name": "Sturgeon Shipyard"
		      },
		      "stage_b": {
		        "id": "2",
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		        "name": "Starfish Mainstage"
		      }
		    },
		    {
		      "stage_b": {
		        "name": "Moray Towers",
		        "id": "8",
		        "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png"
		      },
		      "rule": {
		        "key": "tower_control",
		        "name": "Tower Control",
		        "multiline_name": "Tower\nControl"
		      },
		      "stage_a": {
		        "name": "Inkblot Art Academy",
		        "image": "\/images\/stage\/5c030a505ee57c889d3e5268a4b10c1f1f37880a.png",
		        "id": "4"
		      },
		      "start_time": 1501444800,
		      "game_mode": {
		        "key": "gachi",
		        "name": "Ranked Battle"
		      },
		      "end_time": 1501452000,
		      "id": 4.7809526839201e+18
		    },
		    {
		      "game_mode": {
		        "key": "gachi",
		        "name": "Ranked Battle"
		      },
		      "start_time": 1501452000,
		      "end_time": 1501459200,
		      "id": 4.7809526839201e+18,
		      "stage_b": {
		        "name": "Starfish Mainstage",
		        "id": "2",
		        "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png"
		      },
		      "rule": {
		        "name": "Splat Zones",
		        "multiline_name": "Splat\nZones",
		        "key": "splat_zones"
		      },
		      "stage_a": {
		        "name": "The Reef",
		        "image": "\/images\/stage\/98baf21c0366ce6e03299e2326fe6d27a7582dce.png",
		        "id": "0"
		      }
		    },
		    {
		      "id": 4.7809526839201e+18,
		      "end_time": 1501466400,
		      "start_time": 1501459200,
		      "game_mode": {
		        "name": "Ranked Battle",
		        "key": "gachi"
		      },
		      "stage_a": {
		        "id": "7",
		        "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png",
		        "name": "Port Mackerel"
		      },
		      "rule": {
		        "multiline_name": "Rainmaker",
		        "name": "Rainmaker",
		        "key": "rainmaker"
		      },
		      "stage_b": {
		        "image": "\/images\/stage\/83acec875a5bb19418d7b87d5df4ba1e38ceac66.png",
		        "id": "1",
		        "name": "Musselforge Fitness"
		      }
		    },
		    {
		      "start_time": 1501466400,
		      "game_mode": {
		        "name": "Ranked Battle",
		        "key": "gachi"
		      },
		      "end_time": 1501473600,
		      "id": 4.7809526839201e+18,
		      "stage_b": {
		        "id": "0",
		        "image": "\/images\/stage\/98baf21c0366ce6e03299e2326fe6d27a7582dce.png",
		        "name": "The Reef"
		      },
		      "rule": {
		        "multiline_name": "Splat\nZones",
		        "name": "Splat Zones",
		        "key": "splat_zones"
		      },
		      "stage_a": {
		        "id": "5",
		        "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png",
		        "name": "Humpback Pump Track"
		      }
		    }
		  ]
		}

## Stages [/api/data/stages]

### <a name="GetStages"></a> Get stages [GET]

+ Request

    + Headers

            Cookie: [Cookie variable here]

+ Response 200 (application/json)

	+ Body

		{
		  "stages": [
		    {
		      "id": "0",
		      "image": "\/images\/stage\/98baf21c0366ce6e03299e2326fe6d27a7582dce.png",
		      "name": "The Reef"
		    },
		    {
		      "name": "Musselforge Fitness",
		      "image": "\/images\/stage\/83acec875a5bb19418d7b87d5df4ba1e38ceac66.png",
		      "id": "1"
		    },
		    {
		      "name": "Starfish Mainstage",
		      "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		      "id": "2"
		    },
		    {
		      "id": "3",
		      "image": "\/images\/stage\/bc794e337900afd763f8a88359f83df5679ddf12.png",
		      "name": "Sturgeon Shipyard"
		    },
		    {
		      "name": "Inkblot Art Academy",
		      "image": "\/images\/stage\/5c030a505ee57c889d3e5268a4b10c1f1f37880a.png",
		      "id": "4"
		    },
		    {
		      "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png",
		      "id": "5",
		      "name": "Humpback Pump Track"
		    },
		    {
		      "id": "7",
		      "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png",
		      "name": "Port Mackerel"
		    },
		    {
		      "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png",
		      "id": "8",
		      "name": "Moray Towers"
		    }
		  ]
		}


## Timeline [/api/timeline]

### <a name="GetTimeline"></a> Get timeline [GET]

+ Request

    + Headers

            Cookie: [Cookie variable here]

+ Response 200 (application/json)

	+ Body

		{
		  "challenge": {
		    "next_challenge": {
		      "paint_points": 121000,
		      "key": "tenfold_squid_research_lab",
		      "image": "\/images\/challenge\/bc823e738fddce2cfb96469da441a5e58099740e.png",
		      "name": "Squid Research HQ x10"
		    },
		    "importance": 0.1,
		    "total_paint_point": 106559,
		    "last_archived_challenge": {
		      "name": "Great Pyramid of Giza",
		      "key": "great_pyramid_at_giza",
		      "image": "\/images\/challenge\/2509440d7e6a290451640485abc91ec1b2c20bbc.png",
		      "paint_points": 16000
		    }
		  },
		  "weapon_availability": {
		    "importance": 0.64706944444444,
		    "availabilities": [
		      {
		        "weapon": {
		          "sub": {
		            "id": "8",
		            "image_b": "\/images\/sub\/627ae0ea02ab649a7a482ee7ee7ace85ca307f44.png",
		            "name": "Point Sensor",
		            "image_a": "\/images\/sub\/14b4d4ef62e915e87bd7caa8b99fb4e986caea26.png"
		          },
		          "special": {
		            "image_a": "\/images\/special\/e395a50d51459dcee4db62d8d1fbc4bb263bc326.png",
		            "id": "0",
		            "name": "Tenta Missiles",
		            "image_b": "\/images\/special\/4819d9d318668bdd5dab248a23397ec351bc5c60.png"
		          },
		          "image": "\/images\/weapon\/aaead5ff0b63cdcb989b211d649b2552bb3e3a1b.png",
		          "thumbnail": "\/images\/weapon\/3abcd1e1152e6d819bee363311edcf4737d14a45.png",
		          "name": "Dualie Squelchers",
		          "id": "5030"
		        },
		        "release_time": 1501293600
		      }
		    ]
		  },
		  "onlineshop": {
		    "importance": 0.10622222222222,
		    "merchandise": {
		      "price": 7600,
		      "skill": {
		        "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png",
		        "id": "0",
		        "name": "Ink Saver (Main)"
		      },
		      "gear": {
		        "id": "6006",
		        "rarity": 1,
		        "thumbnail": "\/images\/shoes\/0585889cd0579eab915d05b769827408e4a7694b.png",
		        "name": "Punk Whites",
		        "brand": {
		          "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png",
		          "name": "Rockenberg",
		          "frequent_skill": {
		            "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		            "id": "3",
		            "name": "Run Speed Up"
		          },
		          "id": "3"
		        },
		        "image": "\/images\/shoes\/7f725fb83d72e41297d15e70319bd7c51a5080c1.png",
		        "kind": "shoes"
		      },
		      "kind": "shoes",
		      "end_time": 1501401600,
		      "id": "4780952683920163047"
		    }
		  },
		  "udemae": {
		    "change": 1,
		    "importance": 0,
		    "stat": {
		      "rule": {
		        "key": "splat_zones",
		        "name": "Splat Zones",
		        "multiline_name": "Splat\nZones"
		      },
		      "battle_number": "112",
		      "my_team_result": {
		        "name": "VICTORY",
		        "key": "victory"
		      },
		      "estimate_gachi_power": 1770,
		      "other_team_result": {
		        "name": "DEFEAT",
		        "key": "defeat"
		      },
		      "my_team_count": 100,
		      "player_result": {
		        "assist_count": 0,
		        "game_paint_point": 535,
		        "sort_score": -2,
		        "death_count": 3,
		        "player": {
		          "head": {
		            "rarity": 1,
		            "id": "1019",
		            "name": "King Flip Mesh",
		            "thumbnail": "\/images\/head\/3de76b009f2caf493322b2c4082355184b04ffda.png",
		            "brand": {
		              "frequent_skill": {
		                "image": "\/images\/skill\/34e114a50a001778a574f7061039d43e632137b7.png",
		                "name": "Sub Power Up",
		                "id": "10"
		              },
		              "id": "16",
		              "name": "Enperry",
		              "image": "\/images\/brand\/de96243d58e41e928d30290162a6f496033da868.png"
		            },
		            "kind": "head",
		            "image": "\/images\/head\/30cd8ed7847aa114483571d82bea61ddf7cc5c59.png"
		          },
		          "player_rank": 13,
		          "shoes_skills": {
		            "subs": [
		              {
		                "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png",
		                "id": "12",
		                "name": "Bomb Defense Up"
		              },
		              {
		                "id": "10",
		                "name": "Sub Power Up",
		                "image": "\/images\/skill\/34e114a50a001778a574f7061039d43e632137b7.png"
		              },
		              null
		            ],
		            "main": {
		              "name": "Special Charge Up",
		              "id": "5",
		              "image": "\/images\/skill\/1378f3963526d7216ec44da35b924b81a8ff6a37.png"
		            }
		          },
		          "shoes": {
		            "rarity": 1,
		            "id": "6006",
		            "thumbnail": "\/images\/shoes\/0585889cd0579eab915d05b769827408e4a7694b.png",
		            "brand": {
		              "name": "Rockenberg",
		              "id": "3",
		              "frequent_skill": {
		                "name": "Run Speed Up",
		                "id": "3",
		                "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png"
		              },
		              "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png"
		            },
		            "name": "Punk Whites",
		            "kind": "shoes",
		            "image": "\/images\/shoes\/7f725fb83d72e41297d15e70319bd7c51a5080c1.png"
		          },
		          "clothes": {
		            "image": "\/images\/clothes\/fcf3d555c3deb78e183cdb6ea8187a89f5a01af1.png",
		            "kind": "clothes",
		            "rarity": 1,
		            "id": "8018",
		            "thumbnail": "\/images\/clothes\/4a12e6be82746741a91933cd46ffc07e64656942.png",
		            "brand": {
		              "image": "\/images\/brand\/9ac5752790dd6dbdc7a427df95e1bfe89fe318e0.png",
		              "name": "Krak-On",
		              "id": "2",
		              "frequent_skill": {
		                "id": "4",
		                "name": "Swim Speed Up",
		                "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png"
		              }
		            },
		            "name": "Octobowler Shirt"
		          },
		          "head_skills": {
		            "subs": [
		              {
		                "image": "\/images\/skill\/da8ff08954fd5d890fc8bc4dd4cb761e2a33b703.png",
		                "name": "Ink Saver (Sub)",
		                "id": "1"
		              },
		              {
		                "name": "Swim Speed Up",
		                "id": "4",
		                "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png"
		              },
		              null
		            ],
		            "main": {
		              "name": "Run Speed Up",
		              "id": "3",
		              "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png"
		            }
		          },
		          "weapon": {
		            "id": "41",
		            "name": "Tentatek Splattershot",
		            "thumbnail": "\/images\/weapon\/5f519a8b3f436c854dc81ee14bfc3a26aef09ebc.png",
		            "special": {
		              "id": "8",
		              "image_b": "\/images\/special\/26e8117808ce17dadb0f23943359e5909fef4085.png",
		              "name": "Inkjet",
		              "image_a": "\/images\/special\/9871c82952ed0141be0310ace1942c9f5f66d655.png"
		            },
		            "image": "\/images\/weapon\/331d889d8113b794131080c8943e05a3d2c4547d.png",
		            "sub": {
		              "image_a": "\/images\/sub\/d2eaeec524d28ef315a13f8a9e11dd1039cb78aa.png",
		              "id": "0",
		              "name": "Splat Bomb",
		              "image_b": "\/images\/sub\/b13bf755b279af83904892fae01cd98c866dfec7.png"
		            }
		          },
		          "star_rank": 0,
		          "principal_id": "3095008c85ee2a64",
		          "udemae": {
		            "number": 3,
		            "s_plus_number": null,
		            "name": "B-"
		          },
		          "nickname": "Zeke",
		          "clothes_skills": {
		            "subs": [
		              {
		                "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png",
		                "name": "Swim Speed Up",
		                "id": "4"
		              },
		              {
		                "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png",
		                "id": "4",
		                "name": "Swim Speed Up"
		              },
		              null
		            ],
		            "main": {
		              "id": "0",
		              "name": "Ink Saver (Main)",
		              "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png"
		            }
		          }
		        },
		        "kill_count": 4,
		        "special_count": 0
		      },
		      "type": "gachi",
		      "other_team_count": 0,
		      "udemae": {
		        "number": 4,
		        "name": "B",
		        "s_plus_number": null
		      },
		      "star_rank": 0,
		      "start_time": 1501289726,
		      "player_rank": 13,
		      "elapsed_time": 111,
		      "stage": {
		        "id": "5",
		        "name": "Humpback Pump Track",
		        "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png"
		      },
		      "game_mode": {
		        "key": "gachi",
		        "name": "Ranked Battle"
		      },
		      "weapon_paint_point": 45060
		    }
		  },
		  "schedule": {
		    "schedules": {
		      "gachi": [
		        {
		          "end_time": 1501401600,
		          "stage_b": {
		            "id": "7",
		            "name": "Port Mackerel",
		            "image": "\/images\/stage\/0907fc7dc325836a94d385919fe01dc13848612a.png"
		          },
		          "start_time": 1501394400,
		          "stage_a": {
		            "image": "\/images\/stage\/fc23fedca2dfbbd8707a14606d719a4004403d13.png",
		            "id": "5",
		            "name": "Humpback Pump Track"
		          },
		          "rule": {
		            "multiline_name": "Rainmaker",
		            "name": "Rainmaker",
		            "key": "rainmaker"
		          },
		          "id": 4.7809526839201e+18,
		          "game_mode": {
		            "key": "gachi",
		            "name": "Ranked Battle"
		          }
		        }
		      ],
		      "league": [
		        {
		          "game_mode": {
		            "name": "League Battle",
		            "key": "league"
		          },
		          "start_time": 1501394400,
		          "stage_a": {
		            "name": "Musselforge Fitness",
		            "id": "1",
		            "image": "\/images\/stage\/83acec875a5bb19418d7b87d5df4ba1e38ceac66.png"
		          },
		          "rule": {
		            "name": "Tower Control",
		            "multiline_name": "Tower\nControl",
		            "key": "tower_control"
		          },
		          "id": 4.7809526839201e+18,
		          "stage_b": {
		            "id": "8",
		            "name": "Moray Towers",
		            "image": "\/images\/stage\/96fd8c0492331a30e60a217c94fd1d4c73a966cc.png"
		          },
		          "end_time": 1501401600
		        }
		      ],
		      "regular": [
		        {
		          "game_mode": {
		            "name": "Regular Battle",
		            "key": "regular"
		          },
		          "start_time": 1501394400,
		          "rule": {
		            "key": "turf_war",
		            "multiline_name": "Turf\nWar",
		            "name": "Turf War"
		          },
		          "stage_a": {
		            "image": "\/images\/stage\/bc794e337900afd763f8a88359f83df5679ddf12.png",
		            "id": "3",
		            "name": "Sturgeon Shipyard"
		          },
		          "id": 4.7809526839201e+18,
		          "stage_b": {
		            "name": "Starfish Mainstage",
		            "id": "2",
		            "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png"
		          },
		          "end_time": 1501401600
		        }
		      ]
		    },
		    "importance": 0.8
		  },
		  "unique_id": "16039570077175261768",
		  "coop": {
		    "importance": -1
		  },
		  "stats": {
		    "recents": [
		      {
		        "elapsed_time": 148,
		        "player_rank": 14,
		        "start_time": 1501351041,
		        "stage": {
		          "name": "Starfish Mainstage",
		          "id": "2",
		          "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png"
		        },
		        "weapon_paint_point": 7473,
		        "game_mode": {
		          "key": "gachi",
		          "name": "Ranked Battle"
		        },
		        "estimate_gachi_power": 1650,
		        "my_team_result": {
		          "key": "victory",
		          "name": "VICTORY"
		        },
		        "battle_number": "134",
		        "rule": {
		          "key": "splat_zones",
		          "multiline_name": "Splat\nZones",
		          "name": "Splat Zones"
		        },
		        "other_team_result": {
		          "name": "DEFEAT",
		          "key": "defeat"
		        },
		        "my_team_count": 100,
		        "player_result": {
		          "player": {
		            "head": {
		              "image": "\/images\/head\/b911d153004f390fafd4e998fc080a3773ca9167.png",
		              "kind": "head",
		              "brand": {
		                "name": "Skalop",
		                "frequent_skill": {
		                  "name": "Quick Respawn",
		                  "id": "8",
		                  "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png"
		                },
		                "id": "7",
		                "image": "\/images\/brand\/8175954b5a7e02b8097dbb484c808c8f39d31f41.png"
		              },
		              "thumbnail": "\/images\/head\/d4fe25a57bdc9eae61ed20932b56ad89b2bdcdea.png",
		              "name": "Jellyvader Cap",
		              "rarity": 2,
		              "id": "1023"
		            },
		            "player_rank": 14,
		            "shoes_skills": {
		              "main": {
		                "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		                "name": "Ink Resistance Up",
		                "id": "11"
		              },
		              "subs": [
		                {
		                  "name": "Bomb Defense Up",
		                  "id": "12",
		                  "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png"
		                },
		                {
		                  "name": "Run Speed Up",
		                  "id": "3",
		                  "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png"
		                },
		                null
		              ]
		            },
		            "star_rank": 0,
		            "weapon": {
		              "image": "\/images\/weapon\/aaead5ff0b63cdcb989b211d649b2552bb3e3a1b.png",
		              "special": {
		                "image_a": "\/images\/special\/e395a50d51459dcee4db62d8d1fbc4bb263bc326.png",
		                "id": "0",
		                "name": "Tenta Missiles",
		                "image_b": "\/images\/special\/4819d9d318668bdd5dab248a23397ec351bc5c60.png"
		              },
		              "sub": {
		                "image_a": "\/images\/sub\/14b4d4ef62e915e87bd7caa8b99fb4e986caea26.png",
		                "id": "8",
		                "image_b": "\/images\/sub\/627ae0ea02ab649a7a482ee7ee7ace85ca307f44.png",
		                "name": "Point Sensor"
		              },
		              "id": "5030",
		              "name": "Dualie Squelchers",
		              "thumbnail": "\/images\/weapon\/3abcd1e1152e6d819bee363311edcf4737d14a45.png"
		            },
		            "principal_id": "3095008c85ee2a64",
		            "shoes": {
		              "rarity": 2,
		              "id": "6003",
		              "name": "Blue Moto Boots",
		              "thumbnail": "\/images\/shoes\/6564c18c77f9d0dc58a100f4b187bd7612187db5.png",
		              "brand": {
		                "frequent_skill": {
		                  "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		                  "id": "3",
		                  "name": "Run Speed Up"
		                },
		                "id": "3",
		                "name": "Rockenberg",
		                "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png"
		              },
		              "image": "\/images\/shoes\/061da7c22c1d15acfc3c737383ced1d6f7ba48d8.png",
		              "kind": "shoes"
		            },
		            "clothes": {
		              "kind": "clothes",
		              "image": "\/images\/clothes\/60e601b160dd7d7a4aecc6ad2a5e51ae2d5b52b7.png",
		              "name": "Zekko Hoodie",
		              "thumbnail": "\/images\/clothes\/158e48710cb726e94f2a5ac1fdb11c1c29f55ede.png",
		              "brand": {
		                "image": "\/images\/brand\/f3d01187fd633e7d48d9e4e16ef31da73279293c.png",
		                "frequent_skill": {
		                  "name": "Special Saver",
		                  "id": "6",
		                  "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png"
		                },
		                "id": "4",
		                "name": "Zekko"
		              },
		              "rarity": 1,
		              "id": "10002"
		            },
		            "head_skills": {
		              "subs": [
		                {
		                  "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png",
		                  "name": "Quick Super Jump",
		                  "id": "9"
		                },
		                {
		                  "name": "Quick Respawn",
		                  "id": "8",
		                  "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png"
		                },
		                null
		              ],
		              "main": {
		                "image": "\/images\/skill\/da8ff08954fd5d890fc8bc4dd4cb761e2a33b703.png",
		                "id": "1",
		                "name": "Ink Saver (Sub)"
		              }
		            },
		            "udemae": {
		              "s_plus_number": null,
		              "name": "B",
		              "number": 4
		            },
		            "nickname": "Zeke",
		            "clothes_skills": {
		              "main": {
		                "image": "\/images\/skill\/f0a99d1ab1a765b992b79610ebdc25b69d88fae9.png",
		                "name": "Ninja Squid",
		                "id": "104"
		              },
		              "subs": [
		                {
		                  "name": "Cold-Blooded",
		                  "id": "13",
		                  "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png"
		                },
		                {
		                  "name": "Special Saver",
		                  "id": "6",
		                  "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png"
		                },
		                null
		              ]
		            }
		          },
		          "kill_count": 5,
		          "special_count": 1,
		          "assist_count": 1,
		          "game_paint_point": 493,
		          "death_count": 5,
		          "sort_score": 4
		        },
		        "udemae": {
		          "number": 4,
		          "name": "B",
		          "s_plus_number": null
		        },
		        "other_team_count": 0,
		        "type": "gachi",
		        "star_rank": 0
		      },
		      {
		        "weapon_paint_point": 6980,
		        "game_mode": {
		          "name": "Ranked Battle",
		          "key": "gachi"
		        },
		        "stage": {
		          "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png",
		          "id": "2",
		          "name": "Starfish Mainstage"
		        },
		        "player_rank": 14,
		        "elapsed_time": 93,
		        "start_time": 1501350877,
		        "star_rank": 0,
		        "udemae": {
		          "number": 4,
		          "name": "B",
		          "s_plus_number": null
		        },
		        "type": "gachi",
		        "other_team_count": 100,
		        "my_team_count": 0,
		        "player_result": {
		          "game_paint_point": 390,
		          "assist_count": 1,
		          "death_count": 4,
		          "sort_score": 6,
		          "player": {
		            "player_rank": 14,
		            "shoes_skills": {
		              "subs": [
		                {
		                  "id": "12",
		                  "name": "Bomb Defense Up",
		                  "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png"
		                },
		                {
		                  "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		                  "id": "3",
		                  "name": "Run Speed Up"
		                },
		                null
		              ],
		              "main": {
		                "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		                "name": "Ink Resistance Up",
		                "id": "11"
		              }
		            },
		            "head": {
		              "image": "\/images\/head\/b911d153004f390fafd4e998fc080a3773ca9167.png",
		              "kind": "head",
		              "name": "Jellyvader Cap",
		              "thumbnail": "\/images\/head\/d4fe25a57bdc9eae61ed20932b56ad89b2bdcdea.png",
		              "brand": {
		                "name": "Skalop",
		                "frequent_skill": {
		                  "name": "Quick Respawn",
		                  "id": "8",
		                  "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png"
		                },
		                "id": "7",
		                "image": "\/images\/brand\/8175954b5a7e02b8097dbb484c808c8f39d31f41.png"
		              },
		              "id": "1023",
		              "rarity": 2
		            },
		            "udemae": {
		              "number": 4,
		              "name": "B",
		              "s_plus_number": null
		            },
		            "clothes_skills": {
		              "main": {
		                "image": "\/images\/skill\/f0a99d1ab1a765b992b79610ebdc25b69d88fae9.png",
		                "name": "Ninja Squid",
		                "id": "104"
		              },
		              "subs": [
		                {
		                  "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		                  "id": "13",
		                  "name": "Cold-Blooded"
		                },
		                {
		                  "name": "Special Saver",
		                  "id": "6",
		                  "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png"
		                },
		                null
		              ]
		            },
		            "nickname": "Zeke",
		            "star_rank": 0,
		            "principal_id": "3095008c85ee2a64",
		            "weapon": {
		              "sub": {
		                "image_a": "\/images\/sub\/14b4d4ef62e915e87bd7caa8b99fb4e986caea26.png",
		                "id": "8",
		                "image_b": "\/images\/sub\/627ae0ea02ab649a7a482ee7ee7ace85ca307f44.png",
		                "name": "Point Sensor"
		              },
		              "image": "\/images\/weapon\/aaead5ff0b63cdcb989b211d649b2552bb3e3a1b.png",
		              "special": {
		                "image_a": "\/images\/special\/e395a50d51459dcee4db62d8d1fbc4bb263bc326.png",
		                "id": "0",
		                "name": "Tenta Missiles",
		                "image_b": "\/images\/special\/4819d9d318668bdd5dab248a23397ec351bc5c60.png"
		              },
		              "name": "Dualie Squelchers",
		              "thumbnail": "\/images\/weapon\/3abcd1e1152e6d819bee363311edcf4737d14a45.png",
		              "id": "5030"
		            },
		            "clothes": {
		              "image": "\/images\/clothes\/60e601b160dd7d7a4aecc6ad2a5e51ae2d5b52b7.png",
		              "kind": "clothes",
		              "id": "10002",
		              "rarity": 1,
		              "brand": {
		                "image": "\/images\/brand\/f3d01187fd633e7d48d9e4e16ef31da73279293c.png",
		                "name": "Zekko",
		                "id": "4",
		                "frequent_skill": {
		                  "id": "6",
		                  "name": "Special Saver",
		                  "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png"
		                }
		              },
		              "thumbnail": "\/images\/clothes\/158e48710cb726e94f2a5ac1fdb11c1c29f55ede.png",
		              "name": "Zekko Hoodie"
		            },
		            "shoes": {
		              "image": "\/images\/shoes\/061da7c22c1d15acfc3c737383ced1d6f7ba48d8.png",
		              "kind": "shoes",
		              "name": "Blue Moto Boots",
		              "thumbnail": "\/images\/shoes\/6564c18c77f9d0dc58a100f4b187bd7612187db5.png",
		              "brand": {
		                "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png",
		                "name": "Rockenberg",
		                "id": "3",
		                "frequent_skill": {
		                  "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		                  "name": "Run Speed Up",
		                  "id": "3"
		                }
		              },
		              "id": "6003",
		              "rarity": 2
		            },
		            "head_skills": {
		              "main": {
		                "image": "\/images\/skill\/da8ff08954fd5d890fc8bc4dd4cb761e2a33b703.png",
		                "name": "Ink Saver (Sub)",
		                "id": "1"
		              },
		              "subs": [
		                {
		                  "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png",
		                  "name": "Quick Super Jump",
		                  "id": "9"
		                },
		                {
		                  "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png",
		                  "name": "Quick Respawn",
		                  "id": "8"
		                },
		                null
		              ]
		            }
		          },
		          "kill_count": 2,
		          "special_count": 0
		        },
		        "other_team_result": {
		          "key": "victory",
		          "name": "VICTORY"
		        },
		        "estimate_gachi_power": 1710,
		        "my_team_result": {
		          "key": "defeat",
		          "name": "DEFEAT"
		        },
		        "battle_number": "133",
		        "rule": {
		          "multiline_name": "Splat\nZones",
		          "name": "Splat Zones",
		          "key": "splat_zones"
		        }
		      },
		      {
		        "rule": {
		          "key": "splat_zones",
		          "name": "Splat Zones",
		          "multiline_name": "Splat\nZones"
		        },
		        "battle_number": "132",
		        "my_team_result": {
		          "name": "VICTORY",
		          "key": "victory"
		        },
		        "estimate_gachi_power": 1750,
		        "player_result": {
		          "player": {
		            "principal_id": "3095008c85ee2a64",
		            "star_rank": 0,
		            "weapon": {
		              "image": "\/images\/weapon\/aaead5ff0b63cdcb989b211d649b2552bb3e3a1b.png",
		              "special": {
		                "name": "Tenta Missiles",
		                "image_b": "\/images\/special\/4819d9d318668bdd5dab248a23397ec351bc5c60.png",
		                "id": "0",
		                "image_a": "\/images\/special\/e395a50d51459dcee4db62d8d1fbc4bb263bc326.png"
		              },
		              "sub": {
		                "image_a": "\/images\/sub\/14b4d4ef62e915e87bd7caa8b99fb4e986caea26.png",
		                "name": "Point Sensor",
		                "image_b": "\/images\/sub\/627ae0ea02ab649a7a482ee7ee7ace85ca307f44.png",
		                "id": "8"
		              },
		              "id": "5030",
		              "thumbnail": "\/images\/weapon\/3abcd1e1152e6d819bee363311edcf4737d14a45.png",
		              "name": "Dualie Squelchers"
		            },
		            "head_skills": {
		              "subs": [
		                {
		                  "name": "Quick Super Jump",
		                  "id": "9",
		                  "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png"
		                },
		                {
		                  "id": "8",
		                  "name": "Quick Respawn",
		                  "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png"
		                },
		                null
		              ],
		              "main": {
		                "name": "Ink Saver (Sub)",
		                "id": "1",
		                "image": "\/images\/skill\/da8ff08954fd5d890fc8bc4dd4cb761e2a33b703.png"
		              }
		            },
		            "shoes": {
		              "kind": "shoes",
		              "image": "\/images\/shoes\/061da7c22c1d15acfc3c737383ced1d6f7ba48d8.png",
		              "name": "Blue Moto Boots",
		              "thumbnail": "\/images\/shoes\/6564c18c77f9d0dc58a100f4b187bd7612187db5.png",
		              "brand": {
		                "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png",
		                "frequent_skill": {
		                  "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		                  "id": "3",
		                  "name": "Run Speed Up"
		                },
		                "id": "3",
		                "name": "Rockenberg"
		              },
		              "rarity": 2,
		              "id": "6003"
		            },
		            "clothes": {
		              "kind": "clothes",
		              "image": "\/images\/clothes\/60e601b160dd7d7a4aecc6ad2a5e51ae2d5b52b7.png",
		              "name": "Zekko Hoodie",
		              "thumbnail": "\/images\/clothes\/158e48710cb726e94f2a5ac1fdb11c1c29f55ede.png",
		              "brand": {
		                "image": "\/images\/brand\/f3d01187fd633e7d48d9e4e16ef31da73279293c.png",
		                "name": "Zekko",
		                "frequent_skill": {
		                  "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png",
		                  "id": "6",
		                  "name": "Special Saver"
		                },
		                "id": "4"
		              },
		              "id": "10002",
		              "rarity": 1
		            },
		            "nickname": "Zeke",
		            "udemae": {
		              "number": 4,
		              "s_plus_number": null,
		              "name": "B"
		            },
		            "clothes_skills": {
		              "subs": [
		                {
		                  "name": "Cold-Blooded",
		                  "id": "13",
		                  "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png"
		                },
		                {
		                  "id": "6",
		                  "name": "Special Saver",
		                  "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png"
		                },
		                null
		              ],
		              "main": {
		                "name": "Ninja Squid",
		                "id": "104",
		                "image": "\/images\/skill\/f0a99d1ab1a765b992b79610ebdc25b69d88fae9.png"
		              }
		            },
		            "head": {
		              "image": "\/images\/head\/b911d153004f390fafd4e998fc080a3773ca9167.png",
		              "kind": "head",
		              "name": "Jellyvader Cap",
		              "thumbnail": "\/images\/head\/d4fe25a57bdc9eae61ed20932b56ad89b2bdcdea.png",
		              "brand": {
		                "name": "Skalop",
		                "id": "7",
		                "frequent_skill": {
		                  "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png",
		                  "name": "Quick Respawn",
		                  "id": "8"
		                },
		                "image": "\/images\/brand\/8175954b5a7e02b8097dbb484c808c8f39d31f41.png"
		              },
		              "id": "1023",
		              "rarity": 2
		            },
		            "player_rank": 14,
		            "shoes_skills": {
		              "subs": [
		                {
		                  "name": "Bomb Defense Up",
		                  "id": "12",
		                  "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png"
		                },
		                {
		                  "id": "3",
		                  "name": "Run Speed Up",
		                  "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png"
		                },
		                null
		              ],
		              "main": {
		                "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		                "id": "11",
		                "name": "Ink Resistance Up"
		              }
		            }
		          },
		          "special_count": 0,
		          "kill_count": 2,
		          "assist_count": 1,
		          "game_paint_point": 348,
		          "death_count": 1,
		          "sort_score": 4
		        },
		        "my_team_count": 100,
		        "other_team_result": {
		          "key": "defeat",
		          "name": "DEFEAT"
		        },
		        "type": "gachi",
		        "other_team_count": 0,
		        "udemae": {
		          "number": 4,
		          "name": "B",
		          "s_plus_number": null
		        },
		        "star_rank": 0,
		        "start_time": 1501350716,
		        "elapsed_time": 83,
		        "player_rank": 14,
		        "stage": {
		          "name": "Starfish Mainstage",
		          "id": "2",
		          "image": "\/images\/stage\/187987856bf575c4155d021cb511034931d06d24.png"
		        },
		        "game_mode": {
		          "name": "Ranked Battle",
		          "key": "gachi"
		        },
		        "weapon_paint_point": 6590
		      },
		      {
		        "my_team_result": {
		          "key": "victory",
		          "name": "VICTORY"
		        },
		        "estimate_gachi_power": 1800,
		        "rule": {
		          "name": "Splat Zones",
		          "multiline_name": "Splat\nZones",
		          "key": "splat_zones"
		        },
		        "battle_number": "131",
		        "other_team_result": {
		          "key": "defeat",
		          "name": "DEFEAT"
		        },
		        "my_team_count": 100,
		        "player_result": {
		          "kill_count": 5,
		          "special_count": 0,
		          "player": {
		            "head": {
		              "image": "\/images\/head\/b911d153004f390fafd4e998fc080a3773ca9167.png",
		              "kind": "head",
		              "rarity": 2,
		              "id": "1023",
		              "brand": {
		                "id": "7",
		                "frequent_skill": {
		                  "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png",
		                  "id": "8",
		                  "name": "Quick Respawn"
		                },
		                "name": "Skalop",
		                "image": "\/images\/brand\/8175954b5a7e02b8097dbb484c808c8f39d31f41.png"
		              },
		              "thumbnail": "\/images\/head\/d4fe25a57bdc9eae61ed20932b56ad89b2bdcdea.png",
		              "name": "Jellyvader Cap"
		            },
		            "shoes_skills": {
		              "main": {
		                "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		                "id": "11",
		                "name": "Ink Resistance Up"
		              },
		              "subs": [
		                {
		                  "id": "12",
		                  "name": "Bomb Defense Up",
		                  "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png"
		                },
		                {
		                  "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		                  "name": "Run Speed Up",
		                  "id": "3"
		                },
		                null
		              ]
		            },
		            "player_rank": 14,
		            "head_skills": {
		              "subs": [
		                {
		                  "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png",
		                  "id": "9",
		                  "name": "Quick Super Jump"
		                },
		                {
		                  "image": "\/images\/skill\/84ab4ba1188849dff63a4314955a53ab103b47df.png",
		                  "id": "8",
		                  "name": "Quick Respawn"
		                },
		                null
		              ],
		              "main": {
		                "image": "\/images\/skill\/da8ff08954fd5d890fc8bc4dd4cb761e2a33b703.png",
		                "id": "1",
		                "name": "Ink Saver (Sub)"
		              }
		            },
		            "shoes": {
		              "id": "6003",
		              "rarity": 2,
		              "name": "Blue Moto Boots",
		              "thumbnail": "\/images\/shoes\/6564c18c77f9d0dc58a100f4b187bd7612187db5.png",
		              "brand": {
		                "frequent_skill": {
		                  "name": "Run Speed Up",
		                  "id": "3",
		                  "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png"
		                },
		                "id": "3",
		                "name": "Rockenberg",
		                "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png"
		              },
		              "image": "\/images\/shoes\/061da7c22c1d15acfc3c737383ced1d6f7ba48d8.png",
		              "kind": "shoes"
		            },
		            "clothes": {
		              "name": "Zekko Hoodie",
		              "thumbnail": "\/images\/clothes\/158e48710cb726e94f2a5ac1fdb11c1c29f55ede.png",
		              "brand": {
		                "image": "\/images\/brand\/f3d01187fd633e7d48d9e4e16ef31da73279293c.png",
		                "frequent_skill": {
		                  "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png",
		                  "id": "6",
		                  "name": "Special Saver"
		                },
		                "id": "4",
		                "name": "Zekko"
		              },
		              "id": "10002",
		              "rarity": 1,
		              "image": "\/images\/clothes\/60e601b160dd7d7a4aecc6ad2a5e51ae2d5b52b7.png",
		              "kind": "clothes"
		            },
		            "star_rank": 0,
		            "principal_id": "3095008c85ee2a64",
		            "weapon": {
		              "sub": {
		                "id": "8",
		                "image_b": "\/images\/sub\/627ae0ea02ab649a7a482ee7ee7ace85ca307f44.png",
		                "name": "Point Sensor",
		                "image_a": "\/images\/sub\/14b4d4ef62e915e87bd7caa8b99fb4e986caea26.png"
		              },
		              "image": "\/images\/weapon\/aaead5ff0b63cdcb989b211d649b2552bb3e3a1b.png",
		              "special": {
		                "image_a": "\/images\/special\/e395a50d51459dcee4db62d8d1fbc4bb263bc326.png",
		                "name": "Tenta Missiles",
		                "image_b": "\/images\/special\/4819d9d318668bdd5dab248a23397ec351bc5c60.png",
		                "id": "0"
		              },
		              "thumbnail": "\/images\/weapon\/3abcd1e1152e6d819bee363311edcf4737d14a45.png",
		              "name": "Dualie Squelchers",
		              "id": "5030"
		            },
		            "nickname": "Zeke",
		            "udemae": {
		              "number": 4,
		              "name": "B",
		              "s_plus_number": null
		            },
		            "clothes_skills": {
		              "main": {
		                "id": "104",
		                "name": "Ninja Squid",
		                "image": "\/images\/skill\/f0a99d1ab1a765b992b79610ebdc25b69d88fae9.png"
		              },
		              "subs": [
		                {
		                  "image": "\/images\/skill\/efa003501e1152ef7b617b9e01517c915e05b7ac.png",
		                  "name": "Cold-Blooded",
		                  "id": "13"
		                },
		                {
		                  "image": "\/images\/skill\/d83b962b84fcea9d02c591c296234f5de77f9682.png",
		                  "id": "6",
		                  "name": "Special Saver"
		                },
		                null
		              ]
		            }
		          },
		          "sort_score": 4,
		          "death_count": 1,
		          "game_paint_point": 384,
		          "assist_count": 1
		        },
		        "udemae": {
		          "number": 4,
		          "s_plus_number": null,
		          "name": "B"
		        },
		        "other_team_count": 0,
		        "type": "gachi",
		        "star_rank": 0,
		        "elapsed_time": 85,
		        "player_rank": 14,
		        "start_time": 1501350557,
		        "stage": {
		          "image": "\/images\/stage\/98baf21c0366ce6e03299e2326fe6d27a7582dce.png",
		          "id": "0",
		          "name": "The Reef"
		        },
		        "weapon_paint_point": 6242,
		        "game_mode": {
		          "key": "gachi",
		          "name": "Ranked Battle"
		        }
		      }
		    ],
		    "importance": 0.69535648148148
		  }
		}


## Nickname and icon [/api/nickname_and_icon{?id}]

+ Parameters
    + id - The id of the user who you would like to retrieve the nickname and icon of. The id can be retrieved from /api/results APIs.

### <a name="GetNicknameIcon"></a> Get user's nickname and icon [GET]

+ Request

    + Headers

            Cookie: [Cookie variable here]

    + Body

		{
		  "nickname_and_icons": [
		    {
		      "nickname": "Zeke",
		      "nsa_id": "user_id_goes_here",
		      "thumbnail_url": "https://cdn-image-e0d67c509fb203858ebcb2fe3f88c2aa.baas.nintendo.com/1/9bf808b1148af78d"
		    }
		  ]
		}


# Group Festivals

## Active Festivals [/api/festivals/active]

### <a name="GetActiveFestivals"></a> Get Active Festivals [GET]

+ Request

    + Headers

            Cookie: [Cookie variable here]

+ Response 200 

	+ Body

		{
		  "festivals": [
		    {
		      "names": {
		        "bravo_long": "Ketchup is better than Mayo!",
		        "alpha_short": "Mayo",
		        "bravo_short": "Ketchup",
		        "alpha_long": "Mayo is better than Ketchup!"
		      },
		      "times": {
		        "announce": 1501293600,
		        "result": 1501999200,
		        "end": 1501992000,
		        "start": 1501905600
		      },
		      "colors": {
		        "middle": {
		          "r": 0.107,
		          "a": 1,
		          "g": 0.692,
		          "css_rgb": "rgb(11%,69%,15%)",
		          "b": 0.148
		        },
		        "alpha": {
		          "b": 0.609,
		          "r": 1,
		          "a": 1,
		          "g": 0.914,
		          "css_rgb": "rgb(100%,91%,61%)"
		        },
		        "bravo": {
		          "r": 0.984,
		          "a": 1,
		          "g": 0.195,
		          "css_rgb": "rgb(98%,20%,12%)",
		          "b": 0.117
		        }
		      },
		      "images": {
		        "alpha": "\/images\/festival\/8d3bacc0ef3479c1bfa5f111cf35f6c5.png",
		        "panel": "\/images\/festival\/941d35ffa3742692c62965cc87876a30.png",
		        "bravo": "\/images\/festival\/273866ecd34058df6bf54e79b18df3ec.png"
		      },
		      "special_stage": {
		        "image": "\/images\/stage\/77f1b9058f27c0215effd00feb5c6b6623b8d5b1.png",
		        "name": "Shifty Station",
		        "id": "9999"
		      },
		      "festival_id": 2050
		    }
		  ]
		}

## Individual Festival Votes [/api/festivals/{festival_id}/votes]

+ Parameters
    + festival_id - The id of the festival you wish to retrieve. This is returned as "festival_id" in a festivals array object element from the /api/festival/active endpoint.

### <a name="GetFestivalVotes"></a> Get festival votes [GET]

+ Request

    + Headers

            Cookie: [Cookie variable here]

+ Response 200 (application/json)

	+ Body

		{
		  "nickname_and_icons": [
		    
		  ],
		  "votes": {
		    "bravo": [
		      
		    ],
		    "alpha": [
		      
		    ]
		  }
		}


# Group Merchandise


## Merchandise List  [/api/onlineshop/merchandises]

### <a name="GetMerchandiseList"></a> Get merchandise list [GET]

+ Request

    + Headers

            Cookie: [Cookie variable here]

+ Response 200 (application/json)

	+ Body
		{
		  "ordered_info": {
		    "price": 14250,
		    "skill": {
		      "name": "Drop Roller",
		      "image": "\/images\/skill\/d0de52e89947803e5b24165335855f39f9e8a6bd.png",
		      "id": "111"
		    },
		    "gear": {
		      "brand": {
		        "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png",
		        "frequent_skill": {
		          "id": "3",
		          "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png",
		          "name": "Run Speed Up"
		        },
		        "id": "3",
		        "name": "Rockenberg"
		      },
		      "image": "\/images\/shoes\/fd5c16ec985483652477eb50591b0bb350f9a3fe.png",
		      "rarity": 2,
		      "id": "8005",
		      "kind": "shoes",
		      "name": "Kid Clams",
		      "thumbnail": "\/images\/shoes\/8b8370b2f5fca2cb13a8c585e986b1749ea7a753.png"
		    }
		  },
		  "merchandises": [
		    {
		      "gear": {
		        "name": "Chirpy Chips Band Tee",
		        "thumbnail": "\/images\/clothes\/3f716dd2e0b869d1fee6dbd74445af2039b91488.png",
		        "kind": "clothes",
		        "rarity": 0,
		        "id": "1042",
		        "brand": {
		          "id": "3",
		          "frequent_skill": {
		            "name": "Run Speed Up",
		            "id": "3",
		            "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png"
		          },
		          "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png",
		          "name": "Rockenberg"
		        },
		        "image": "\/images\/clothes\/5bed2a99692e2320d04cb69efb3d27b1453ba427.png"
		      },
		      "kind": "clothes",
		      "skill": {
		        "image": "\/images\/skill\/33087a476135074af856151a89a6fe4d1d3a996e.png",
		        "id": "11",
		        "name": "Ink Resistance Up"
		      },
		      "price": 2250,
		      "id": "4780952683920163045",
		      "end_time": 1501387200
		    },
		    {
		      "kind": "clothes",
		      "gear": {
		        "name": "Shirt & Tie",
		        "thumbnail": "\/images\/clothes\/2cd7613563ede73573b246c03fd315072481036e.png",
		        "kind": "clothes",
		        "rarity": 2,
		        "id": "8015",
		        "brand": {
		          "frequent_skill": {
		            "id": "0",
		            "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png",
		            "name": "Ink Saver (Main)"
		          },
		          "image": "\/images\/brand\/36bc10db0aa2640c87ad712fc0281515beedcca1.png",
		          "id": "8",
		          "name": "Splash Mob"
		        },
		        "image": "\/images\/clothes\/e394fa214515cde618e3d31204694044e01f9edc.png"
		      },
		      "end_time": 1501394400,
		      "skill": {
		        "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png",
		        "id": "4",
		        "name": "Swim Speed Up"
		      },
		      "price": 12600,
		      "id": "4780952683920163046"
		    },
		    {
		      "skill": {
		        "name": "Ink Saver (Main)",
		        "id": "0",
		        "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png"
		      },
		      "price": 7600,
		      "id": "4780952683920163047",
		      "end_time": 1501401600,
		      "gear": {
		        "kind": "shoes",
		        "name": "Punk Whites",
		        "thumbnail": "\/images\/shoes\/0585889cd0579eab915d05b769827408e4a7694b.png",
		        "brand": {
		          "id": "3",
		          "image": "\/images\/brand\/451a2d0b5ceb7ea4ec4e47c3ff05eee362e9b722.png",
		          "frequent_skill": {
		            "name": "Run Speed Up",
		            "id": "3",
		            "image": "\/images\/skill\/7de1bdfd875ef470b6066c17bed726b5b5113d48.png"
		          },
		          "name": "Rockenberg"
		        },
		        "image": "\/images\/shoes\/7f725fb83d72e41297d15e70319bd7c51a5080c1.png",
		        "id": "6006",
		        "rarity": 1
		      },
		      "kind": "shoes"
		    },
		    {
		      "price": 8200,
		      "id": "4780952683920163048",
		      "skill": {
		        "image": "\/images\/skill\/35f4ec4284fc5a19da58ffb1a7988eb26eb8bd7f.png",
		        "id": "12",
		        "name": "Bomb Defense Up"
		      },
		      "end_time": 1501408800,
		      "gear": {
		        "rarity": 1,
		        "id": "3011",
		        "brand": {
		          "name": "Splash Mob",
		          "frequent_skill": {
		            "id": "0",
		            "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png",
		            "name": "Ink Saver (Main)"
		          },
		          "image": "\/images\/brand\/36bc10db0aa2640c87ad712fc0281515beedcca1.png",
		          "id": "8"
		        },
		        "image": "\/images\/head\/484f496c9062fd10875451cd40d563f65d441205.png",
		        "name": "Half-Rim Glasses",
		        "thumbnail": "\/images\/head\/5bd6835e659e0e9d2d39ae89a9f309c33a8f32d8.png",
		        "kind": "head"
		      },
		      "kind": "head"
		    },
		    {
		      "end_time": 1501416000,
		      "id": "4780952683920163830",
		      "price": 3125,
		      "skill": {
		        "name": "Respawn Punisher",
		        "image": "\/images\/skill\/344e4c16ad4ec9ab8f56711d8d79a1ffb9228a1a.png",
		        "id": "107"
		      },
		      "kind": "clothes",
		      "gear": {
		        "kind": "clothes",
		        "thumbnail": "\/images\/clothes\/d4d96e9a1305901f918b16147e60170aca01e55f.png",
		        "name": "Inkopolis Squaps Jersey",
		        "image": "\/images\/clothes\/cfb16fc9bfc2d1527c3327b69c698c1f6d0f5c20.png",
		        "brand": {
		          "id": "1",
		          "frequent_skill": {
		            "name": "Quick Super Jump",
		            "id": "9",
		            "image": "\/images\/skill\/daf6883039afa62da91eb93eb2a40b673f10b715.png"
		          },
		          "image": "\/images\/brand\/3d4661b3f60f4b74e9bb6760ba7397ecd2502a20.png",
		          "name": "Zink"
		        },
		        "id": "2014",
		        "rarity": 0
		      }
		    },
		    {
		      "end_time": 1501423200,
		      "price": 12600,
		      "id": "4780952683920163831",
		      "skill": {
		        "name": "Ink Saver (Sub)",
		        "id": "1",
		        "image": "\/images\/skill\/da8ff08954fd5d890fc8bc4dd4cb761e2a33b703.png"
		      },
		      "kind": "clothes",
		      "gear": {
		        "id": "8015",
		        "rarity": 2,
		        "image": "\/images\/clothes\/e394fa214515cde618e3d31204694044e01f9edc.png",
		        "brand": {
		          "name": "Splash Mob",
		          "id": "8",
		          "image": "\/images\/brand\/36bc10db0aa2640c87ad712fc0281515beedcca1.png",
		          "frequent_skill": {
		            "name": "Ink Saver (Main)",
		            "id": "0",
		            "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png"
		          }
		        },
		        "thumbnail": "\/images\/clothes\/2cd7613563ede73573b246c03fd315072481036e.png",
		        "name": "Shirt & Tie",
		        "kind": "clothes"
		      }
		    }
		  ]
		}

## Individual Merchandise [/api/onlineshop/order/{item_id}]

+ Parameters
    + item_id - The id of the festival you wish to retrieve. This is returned as "id" in a merchandises array object element from the /api/onlineshop/merchandises endpoint.

### <a name="OrderMerchandise"></a> Order Merchandise [POST]

+ Request

	In the body, the override variable must be specified. If override is set to 0, the requested item will not be ordered if there is already a item ordered and not picked up. In that case, the 400 bad request response will be returned. If override is set to 1, the response will be 200 even if there a pending item order. If there is no pending item, the 200 response will be returned regardless of what override is set to. 

	The `X-Unique-Id` header must be retrieved from the `unique_id` element from the GET /api/timeline API.

    + Headers
    		X-Requested-With: XMLHttpRequest
    		X-Unique-Id: [UniqueID]
    		Content-Type: multipart/form-data;boundary=----WebKitFormBoundaryRubAzu8lBx1RHBLz
            Cookie: [Cookie variable here]

 	+ Body

		 	------WebKitFormBoundaryRubAzu8lBx1RHBLz
			Content-Disposition: form-data; name="override"

			0
			------WebKitFormBoundaryRubAzu8lBx1RHBLz--

+ Response 200 (application/json)

	+ Body

		{
		  "ordered_info": {
		    "gear": {
		      "kind": "clothes",
		      "name": "Shirt & Tie",
		      "brand": {
		        "name": "Splash Mob",
		        "frequent_skill": {
		          "id": "0",
		          "image": "\/images\/skill\/04b1de71fba1f14197b9163503955c52fd74858b.png",
		          "name": "Ink Saver (Main)"
		        },
		        "id": "8",
		        "image": "\/images\/brand\/36bc10db0aa2640c87ad712fc0281515beedcca1.png"
		      },
		      "rarity": 2,
		      "thumbnail": "\/images\/clothes\/2cd7613563ede73573b246c03fd315072481036e.png",
		      "id": "8015",
		      "image": "\/images\/clothes\/e394fa214515cde618e3d31204694044e01f9edc.png"
		    },
		    "price": 12600,
		    "skill": {
		      "name": "Swim Speed Up",
		      "image": "\/images\/skill\/d138c293c8ddac42fadf0e6531100a88c79c81f6.png",
		      "id": "4"
		    }
		  }
		}


+ Response 400 (application/json)

	+ Body

		{
		  "message": null,
		  "code": "ONLINE_SHOP_ALREADY_ORDERED"
		}
