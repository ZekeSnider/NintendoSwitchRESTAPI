# Reverse Engineered Nintendo Switch App REST API

## Introduction

This is documentation of the REST APIs used for the Nintendo Switch app, and embedded Splatoon 2 web app. 

All testing was done on an iPhone 7 running iOS 10.3.3 using version 1.0.4 of the Nintendo Switch app on 07/30/17. I reverse-engineered using [mitmproxy](https://mitmproxy.org). It was quite easy as the app does not use cert-pinning at all. I have not tested using the Android app at all, but I would assume that everything is identical (besides obvious user-agent differences). I am using a US account with the language set to English. There may be small differences for other regions.

A [Paw](https://paw.cloud) project is included for macOS users which should help tinkering with the API. I highly recommend trying this out first to figure out how the API works. Take a look at the environment variables to see what you need to fill in. Once you fill in `Client ID`, `Login Page Token Code`, `Login Page Token Code Verifier`, and `Birthday` you can execute the auth requests in order and you should be good to go.

Note: I recommend setting the `User-Agent` on all requests to the Splatoon 2 API to the following string to blend in. There doesn't appear to be any checking for this but better safe than sorry. `Mozilla/5.0 (iPhone; CPU iPhone OS 10_3_3 like Mac OS X) AppleWebKit/603.3.8 (KHTML, like Gecko) Mobile/14G60`

## Blueprints
* [Nintendo Account](NintendoAccountBlueprint.md)
* [Nintendo Switch](SwitchBlueprint.md)
* [Splatoon 2](Splatoon2Blueprint.md)

## Open Source Components

If you are curious about the open source components used in the app, I have compiled them [here](OpenSource.md).

## Authentication Steps

1. Visit authorization link in browser

This page is an HTML page which loads the auth flow which you would normally see first when logging into the app. Follow through the flow by logging in with an account.

https://accounts.nintendo.com/connect/1.0.0/authorize?state=[state here]&redirect_uri=[... continues]

I currently have no idea how this URL is generated. I recommend signing out of the Switch app, then sign back in and open the sign flow link in Safari. You can then open it on your computer and follow from there.

Once you sign in, you will be redirected to a page like `npf71b963c1b7b6d119://auth#session_state=[SessionStateReturnedHere]&session_token_code=[codehere]&state=[StateReturnedHere]` 

2. Get a session token

Extract the session_state and state from that url, and request from [POST /connect/1.0.0/api/session_token](NintendoAccount.md#GetSessionToken)

3. Get a service access token

Make a request to [POST /connect/1.0.0/api/token](NintendoAccount.md#GetServiceToken) using `session_token` from 2.

4. Login to account

Make a request to [POST /v1/Account/Login](SwitchBlueprint.md#LoginAccount). Use `id_token` from 3.

5. Get game list

Use your access token to retrieve the game list from [GET /v1/Game/ListWebServices](SwitchBlueprint.md#GetGameList). Use `webApiServerCredential["accesstoken"]` from 4. 

6. Get access token for Splatoon

Make a request to [GET /v1/Game/GetWebServiceToken](SwitchBlueprint.md#GetGameWebServiceToken). Use the ID of Splatoon 2 from 5 and `webApiServerCredential["accesstoken"]` from 4.

7. Get cookie to use for splatoon requests

Make a request to [GET /](Splatoon2Blueprint.md#GetHomepage). Use the `accessToken` from 6.

8. Play with the Splatoon 2 API

You can now make any request from the [Splatoon 2 API](Splatoon2Blueprint.md) using the cookie retrieved from 7. Have fun!
