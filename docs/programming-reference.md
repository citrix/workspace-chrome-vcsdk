# Programming reference

Virtual Channel SDK for Workspace app for Chrome enables third-party Chrome apps to write custom virtual channels.

These channels negotiated are initialized with the app/desktop sessions launched using Workspace app for Chrome or using HDX SDK for Chrome.

Also, the Virtual Channel SDK gives an easy way to write and receive the data from the third-party Chrome app and the app/desktop.

Click [here](./namespace-receiver.md) to access the full API documentation. 

## Getting Started

1.	Copy `CitrixChromeVCSDK.js` to the third-party Chrome app.
2.	Include `CitrixChromeVCSDK.js` in the background scripts of the third-party Chrome app.
3.	Ensure to use the APIs only after all the background scripts are loaded.
4.	Register the virtual channel and store the virtual channel object returned.
5.	Appropriate callbacks registered would be called for various actions.
6.	Use sendData method to send any packet to the session.
7.	All the registered virtual channels are now initialized with each app/desktop session launched.

## Prerequisite

Each third-party Chrome app along with the Virtual channel stream name has to be sent as configuration to the Workspace app.

A sample policy file is shown below:

```
{
	"settings": {
		"Value": {
			"settings_version": "1.0",
				"engine_settings": {
					"customVC": [
						{
							"appId": "<third_party_chrome_app_id>",
							"streamName": "<VC_NAME>"
                     }
                             ]
                }
			}
	}
}
```

!!!tip "Note"
		`third_party_chrome_app_id` is the id of the chrome app implementing custom VC and `VC_NAME` is the name of the VC. Repeat the `appid` and `streamName` parameters to add more than one VC. Maximum of 3 VCs supported.

