# Building examples
## Building a server-side example using `Nmake`
Examples of the latest server-side executables have been provided for testing. You can download the latest Windows Virtual Channel SDK in order to develop the server-side component.## Building a client-side exampleFor example on sample apps, see the [download](https://www.citrix.com/downloads/citrix-receiver/chrome/receiver-for-chrome-sdk-latest.html) page. 
### Loading Sample virtual channel appsCitrix provides Chrome packaged apps for each of the example virtual channel. You can load the apps using the following steps* Open new tab in Chrome browser
* Open `chrome://extensions`
* Ensure the Developer mode checkbox is ticked.
* Click on load unpacked extensions
* Point to the third-party sample app (for example, Ping)
* You can see the app Id which needs to be used to configure Receiver.### Configuring the Receiver
Use one of the configuration methods provided for Receiver for Chrome configuration.<give link>
Recommended is to push policy using Google Admin Console. The following represents a sample policy file:

```{	"settings": {		"Value": {			"settings_version": "1.0",			"engine_settings": {				"customVC": [ 					{ // Should be repeated for each virtual channel to be added. Up to 3 virtual channels are supported.					 "appId": "<third_party_chrome_app_id1>", //Id of the ping or mix or over apps or your own app.					 "streamName": "<virtual channel name1>" //Here, CTXPING, Mix, or CTXOVER based on the VC you want to try.					} 				]			}		}	}}```
### Running an Example Virtual Channel1. Copy the server side executables.
2. On the client,
	* Install the third-party Chrome app implementing the virtual channel
	* Configure Receiver for Chrome.
	* Launch session using Receiver for Chrome.