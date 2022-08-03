# Endless Space Activation Client

A simple application for activating game ENDLESS™ Space - Definitive Edition on many steam accounts.

## How it works

This application logs into your account, collects some information required for activation, and posts a task with this information to a third-party service. The service performs your task and activates the game on your account. So simple and fast.

#### What kind of info is sent to a third-party service

1. [Steamid](https://help.steampowered.com/en/faqs/view/2816-BE67-5B69-0FEC)
2. [Openid nonce](https://openid.net/specs/openid-connect-core-1_0.html#CodeFlowSteps:~:text=following%20request%20parameters%3A-,nonce,-OPTIONAL.%20String%20value)
3. [Openid sig](https://openid.net/specs/openid-authentication-2_0.html#:~:text=return_to%2Cassoc_handle%2Cresponse_nonce%22.-,openid.sig,-Value%3A%20Base%2064)

#### Ditailed pipeline

1. Steam login
2. Cheking game in library (optional)
3. Openid auth
4. Creating a task with a returned openid response on a third-party service
5. Waiting task result

## Features

#### `Import accounts from` [`farms`](https://github.com/JustArchiNET/ArchiSteamFarm)

You can select more than one farm. The search for accounts is recursive.

#### `Import accounts from file`

CSV format: `username:password`

Examples:

-   `user1:pass1`
-   `user2:pass2:email:emailpass`
-   `user3:pass3:otheroptions`

#### `Ignore List`

You can add a list of usernames that you dont want to import. Each on a new line. Every successfully processed account is added to this list.

#### `2FA auth`

Only when you import accounts from the farm.

#### `Checking the game's existence`

Checks if the game exists on the account. If the game already exists, the script will move to the next account, and the current account will be added to the ignore list.

#### `Requests proxification`

Supported protocols: http, https, socks5

#### `Import proxies from farm`

From file ASF.json

#### `Import proxies from file`

Uri format: `protocol://username:password@host:port`

The ip change link is supported, a GET request will be sent. If there is no response from the server or the server returns a status other than 200, the application will generate an IP change error.

Examples:

-   `http://user1:pass1@1.2.3.5:1235`
-   `socks://1.2.3.5:1235`
-   `socks5://user1:pass1@1.2.3.5:1235`
-   `http://127.0.0.1:1235`
-   `socks://1.2.3.5:1235:https://changeip.com`
-   `https://user1:pass1@1.2.3.5:1235:changeip.com`

#### `Multithreading`

For example, instead of one account, 10 are doing the same job at the same time. This is much faster. It is recommended to use only if you have imported a proxy from a file.

#### `Limit the number of script runs`

You can limit the number of executions by successes or failures.

## Screens

![tab.accounts](./src-docs/tab.accounts.png)
![tab.proxies](./src-docs/tab.proxies.png)
![tab.other](./src-docs/tab.other.png)

## Install

Clone or [download](https://github.com/Sadzurami/ClientEndlessSpaceG2G/archive/refs/heads/main.zip) this repository and run `ClientEndlessSpaceG2G.exe`

## Requirements

-   Windows x64 (7+)
-   1 CPU, 512 MB RAM
-   Internet speed 5MB/s +