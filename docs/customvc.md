# Class: CustomVC


**new CustomVC()**

## Properties

| Name | Type | Description |
|----|----|----|
| `streamName	`| string	| Virtual Channel name.|
| `description` |	string	 | Description of the Virtual channel. |
| `minVersion`	| string	| Lowest supported version of this virtual channel, used to allow version negotiation between the client-side and the server-side components. |
| `maxVersion	`| string	| Highest supported version of this virtual channel, used to allow version negotiation between the client-side and the server-side components. |
| `driverOpen`	| [driverOpen](./global.md#driveropen)	| Callback set for receiving virtual channel open from the session |
| `driverInfo`	| [driverInfo](./global.md#driverinfo)	| Callback set for sending virtual channel information from the session|
| `icaDataArrival`	| [icaDataArrival](./global.md/#icadata)	| Callback set for receiving the ica packet from the server side component of virtual channel. |
| `driverClose` |	[driverClose](./global.md#driverclose)	| Callback set for receiving the virtual channel close in the session. |

## Methods

`(inner) sendData(data)`

Sends the packet to the server side component of the virtual channel for the session.

### Parameters

| Name | Type | Description |
|----|----|----|
| `data` | [sendDataPacket](./global.md#senddata) | Data packet that needs to be sent to server .|

### Throws

Error during `sendData`

#### Type

[ReceiverError](./receiver-error.md)

### Example

Sample reply packet construction to CTXPING Virtual channel

```
//In continuation with the pingIcaDataArrival function implementation
	var reply = {};
	reply["data"] = new Uint8Array(length);
	reply["length"] = length;
	var offset =0;
	reply["offset"] = offset;
		
	offset = citrix.receiver.utils.writeUint16(reply["data"],offset,uSign);
	offset = citrix.receiver.utils.writeUint16(reply["data"],offset,uType);
	offset = citrix.receiver.utils.writeUint16(reply["data"],offset,uLen);
	offset = citrix.receiver.utils.writeUint16(reply["data"],offset,uCounter);
	offset = citrix.receiver.utils.writeUint32(reply["data"],offset,ulServerMS);		
	offset = citrix.receiver.utils.writeUint32(reply["data"],offset,new Date().getMilliseconds());	

	ctxping.sendData({"sessionId":msg.sessionId,"packet":reply,"streamName":msg.streamName});
```

