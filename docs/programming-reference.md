# Programming reference
Virtual Channel SDK for Receiver for Chrome enables third-party Chrome apps to write custom virtual channels.
These channels negotiated are initialized with the app/desktop sessions launched using Receiver for Chrome or using HDX SDK for Chrome.
Also, the Virtual Channel SDK gives an easy way to write and receive the data from the third-party Chrome app and the app/desktop.
## Getting Started
1.	Copy `CitrixChromeVCSDK.js` to the third-party Chrome app.2.	Include `CitrixChromeVCSDK.js` in the background scripts of the third-party Chrome app.3.	Ensure to use the APIs only after all the background scripts are loaded.4.	Register the virtual channel and store the virtual channel object returned.5.	Appropriate callbacks registered would be called for various actions.6.	Use sendData method to send any packet to the session.7.	All the registered virtual channels are now initialized with each app/desktop session launched.
## Prerequisite
Each third-party Chrome app along with the Virtual channel stream name has to be sent as configuration to the Receiver

