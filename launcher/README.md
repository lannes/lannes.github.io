# **VTC Launcher Integration**

## **Version: 1.0**
## **Update History**:

| Version   | Update                                                              | Date        |
|----------:|---------------------------------------------------------------------|-------------|
| **v1.0**  | - The game shortcut call `VTCGame.exe` instead of `VTCLauncher.exe` | 12-08-2019  |
|           | without parameters.                                                 |             |
|           | - Change sequence diagram.                                          |             |
|           | - Add explain `vcoinGame`.                                          |             |
| **v0.3**  | - Add size of parameters.                                           | 30-07-2019  |
|           | - Add the meaning of the `CLIENT ID`.                               |             |
|           | - Add size of user id.                                              |             |
|           | - Add error code table.                                             |             |
| **v0.2**  | - The shortcut call `VTCLauncher.exe` with param `Game`.            | 19-07-2019  |
|           | - Diagram add buy item flow.                                        |             |
|           | - `CLIENT ID` of LIVE environment.                                  |             |
| **v0.1**  | Initialize document.                                                | 17-07-2019  |

## **Table of contents**
* [1. Sequence diagram](#1-Sequence-diagram)
* [2. Folder Structure](#2-Folder-Structure)
* [3. Call game](#3-Call-game)
* [4. Get account detail](#4-Get-account-detail)
	* [4.1. Environment](#41-Environment)
	* [4.2. Get account detail](#42-Get-account-detail)
* [5. The accounts for testing on the SANDBOX](#5-The-accounts-for-testing-on-the-SANDBOX)

## **1. Sequence diagram**

![](./sequence-diagram.svg)

## **2. Folder Structure**

`VTCGame.exe` and `Launcher` folder located in the same where with `Game.exe`. At here, `Game.exe` is execute file of the game, e.g `Ragnarok.exe`, `NewGunbound.exe`, ...

Folder Structure:

```
    game-folder
    |-- + Launcher
    |   | -- VTCLauncher.exe
    |   | -- config.ini (The configuration file for sandbox environment.)
    |   | -- ...
    |-- VTCGame.exe
    |-- Game.exe
```

* SANDBOX environment
	* [Download file](./sandbox/Sandbox.zip)
* LIVE environment
	* Beta testing can do by set `Sandbox` parameter in the `config.ini` file equals `0`.
	* The game installer for public version must don't include `config.ini` file, because it will prevent update mechanism of Launcher.

## **3. Call game**

`VTCLauncher` call the game by the command line as below:
```cmd
Game.exe User=<Username> Token=<AccessToken> BToken=<BillingAccessToken>
```

Parameters:  
* `User`: Username (max: 30 bytes)
* `Token`: Access token to get user information (max: 52 bytes).
* `BToken`: Billing accesss token to do payment in the game (max: 100 bytes).

## **4. Get account detail**

### **4.1. Environment**

* SANDBOX: 
	* `HOST`: http://apisdk1.vtcgame.vn
	* `CLIENT ID`: There is different value for each game.  
* LIVE: 
	* `HOST`: https://apisdk.vtcgame.vn
	* `CLIENT ID`: There is different value for each game.

`CLIENT ID`: application identifier when connect to VTC system.

### **4.2. Get account detail**

* URL: sdk/account/detail
* Method: GET
* Params:
	- client_id: `CLIENT ID`
	- access_token: `Token`
	- username: `User`
* Example:
	* SANDBOX:
		```http
		http://apisdk1.vtcgame.vn/sdk/account/detail?client_id=<CLIENT ID>&access_token=a4596aed-a6ff-4b69-a12e-25704c9c256e&username=vtctest01
		```
	* LIVE:
		```http
		https://apisdk.vtcgame.vn/sdk/account/detail?client_id=<CLIENT ID>&access_token=3ff10246-1bdd-4d77-a300-ab63a659474b&username=zorroxtm
		```
* Result:
	```
	{
		"error": 200,
		"message": "Success",
		"info": {
			"id": "117813683",
			"userName": "vtctest01",
			"password": "",
			"fullName": "vtctest01",
			"email": "Quytn@vtc.vn",
			"birthday": 1177977600000,
			"locationId": 24,
			"userPassport": "",
			"userStatus": 1,
			"mobile": "",
			"gender": 0,
			"address": "",
			"vcoinGame": 0,
			"vcoinPayment": 112406,
			"paygateId": 0,
			"timeStored": null,
			"billingAccessToken": null,
			"gameClientIds": null
		}
	}
	```

_Note:_
* _`id`: user identifier. Type of `id` is BIGINT, it have size is 8 bytes (range: from 1 to 2^63 -1)._
* _`vcoinGame`: coin balance in the game._
* _Errors:_

	| `error` | `message`                                        | description                                 |
	|------:|----------------------------------------------------|---------------------------------------------|
	| 200   | Success                                            | Success                                     |
	| -303  | Phiên đăng nhập đã hết hạn. Vui lòng đăng nhập lại | The session has expired. Please login again |
	| -304  | Kết nối không ổn định. Xin vui lòng thử lại!!!     | Unstable connection. Please try again!!!    |

## **5. The accounts for testing on the SANDBOX**

* accounts: vtctest01 -> vtctest99
* password: 123456

*Note: **vtctest10** account has **OTP** default is 123456.*