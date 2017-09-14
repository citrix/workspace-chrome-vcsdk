# Global

## Type Definitions




### <a name="driverclose">driverClose(msg)</a> 

Callback that gets called when the virtual channel is closed for a session
Do any cleanup of the virtual channel in your implementation inside the callback.

#### Parameters

| Name | Type | Description |
|----|----|----|
| `msg` | driverCloseMsg | Details of the session containing the session id and virtual channel name. |

#### Example

```
//Driver close for CTXPING virtual channel. You can handle any cleanup for each session.
	function pingDriverClose(msg){
		console.log("driver close received for stream " + msg["streamName"] + " for session " + msg["sessionId"]);
	}
```

### driverCloseMsg

Contains the details of the session for which the virtual channel is closed.

#### Type

* Object

#### Properties

| Name | Type | Description |
|----|----|----|
| `driverCloseMsg.sessionId` |	string	 | Id of the session launched. |
| `driverCloseMsg.streamName`|	string	| Virtual channel name. |



### <a name="driverinfo">driverInfo(msg) → {driverInfoReply}</a>

Callback that gets called for each session provided the virtual channel is enabled through driverOpen callback. 
Use this to send any of the virtual channel information to the session.

#### Parameters

| Name | Type | Description |
|----|----|----|
| `msg` | driverInfoMsg	 | Message from Session with session id and stream name. |

#### Returns

##### Type

* driverInfoReply

#### Example

Example 1: Sending Pingcount for the Ping VC

```
var counter = 3;
function pingDriverInfo(msg){			
	var reply = {};
	reply["data"] = new Uint8Array(4);
	reply["length"] = 4;
	var offset =0;
	reply["offset"] = offset;
	offset = citrix.receiver.utils.writeUint16(reply["data"],offset,2048);
	offset = citrix.receiver.utils.writeUint16(reply["data"],offset,counter);
		
	return {"sessionId":msg["sessionId"], "streamName": msg["streamName"], "packet" :reply};
}
```

Example 2: No data to be sent

```
function driverInfoCb(msg){
	return {"sessionId":msg["sessionId"], "streamName": msg["streamName"],"packet":null};
}
```
### driverInfoMsg

Message received from session for driverOpen callback

#### Type

* Object

#### Properties

| Name	| Type	| Description |
|---|---|---|
| `driverInfoMsg.sessionId`| string	| Id of the session launched.|
| `driverInfoMsg.streamName` | string | Virtual channel name. |

### driverInfoReply

Reply to be sent by the driverInfo callback for each session.

#### Type

* Object

#### Properties

| Name | Type |	Description |
|----|---|---|
| `driverInfoReply.sessionId`	| string	| Id of the session launched|
| `driverInfoReply.streamName` |	string	| Virtual channel name |
| `driverOpenReply.packet` |	packet	| Set the information in Uint8Array with offset and length appropriately or set null if no data to be sent. |




### <a name="driveropen">driverOpen(msg) → {driverOpenReply}</a>

Callback that gets called when the virtual channel is about to be opened upon each session launch.

VC will be enabled based on the driverOpenReply for each session.

#### Parameters

| Name |	Type	| Description|
|---|---|---|
| `msg`	| driverOpenMsg |	Details of the session containing the session id and virtual channel name. |

#### Returns

##### Type

* driverOpenReply

#### Example

```
//Driver Open callback for CTXPING virtual channel. You can handle any code initialization for this virtual channel for each session.
function pingDriverOpen(msg){
	//Enable/Disable the VC for the session with id = msg["sessionId"] by replying with enable flag true/false
	return {"sessionId" : msg["sessionId"],"streamName":msg["streamName"],"enable":true};
}
```

### driverOpenMsg

Contains the details of the session for which driver is going to be opened.

#### Type

* Object

#### Properties

| Name	| Type	 | Description |
|---|---|---|
| `driverOpenMsg.sessionId` |	string	 | Id of the session launched.|
| `driverOpenMsg.streamName` | string | Virtual channel name.|

### driverOpenReply

Reply to be sent by the driverOpen callback for each session.

#### Type

* Object

#### Properties

| Name	| Type	 | Description |
|---|---|---|
| `driverOpenReply.sessionId` |	string | Id of the session launched |
| `driverOpenReply.streamName` |	string	 | Virtual channel name |
| `driverOpenReply.enable` |	boolean | Setting to true/false will enable/disable the VC open for the session with id = driverOpenMsg.sessionId. By default enable will be false.



### <a name="icadata"></a>icaDataArrival(msg)

Callback that gets called when an ica packet is sent by the server component of virtual channel. 

Should parse the packet received inside this callback.

!!!tip "Note"
		Same callback will be called when data arrives from any session launched for that Virtual channel. Use sessionId to differentiate between the sessions.

#### Parameters

| Name	| Type	 | Description |
|---|---|---|
| `msg` | icaDataArrivalMsg |	Details of the session containing the session id and virtual channel name. |

#### Example

```
//Received packet from CTXPING virtual channel.

function pingIcaDataArrival(msg){
	var input = msg["packet"]["data"];
	var offset = msg["packet"]["offset"];
	var length = msg["packet"]["length"];
	
	var uSign = citrix.receiver.utils.readUint16(input,offset);
	offset +=2;
	var uType = citrix.receiver.utils.readUint16(input,offset);
	offset +=2;
	var uLen = citrix.receiver.utils.readUint16(input,offset);
	offset +=2;
	var uCounter = citrix.receiver.utils.readUint16(input,offset);
	offset +=2;		
	var ulServerMS = citrix.receiver.utils.readUint32(input,offset);
	offset +=4;
	var ulClientMS = citrix.receiver.utils.readUint32(input,offset);
	offset +=4;
	
	//need to send reply here . Refer example for sendData for full implementation
}
```

### icaDataArrivalMsg

Contains the details of the session and the ica packet received.

#### Type

* Object

#### Properties

| Name	| Type	 | Description |
|---|---|---|
| `icaDataArrivalMsg.sessionId` |	 string | Id of the session launched. |
| `icaDataArrivalMsg.streamName` | string | Virtual channel name. |
| `icaDataArrivalMsg.packet` | packet | ICA packet sent by the server side component of virtual channel. |

### packet

Packet received/sent by session will have the following format.

#### Type

* Object

#### Properties

| Name	| Type	 | Description |
|---|---|---|
| `packet.data` | Uint8Array | Contains the data to be sent to session or when received from the session. Refer [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array) for more details on Uint8Array. |
| `packet.offset` |	number	 | Offset from where data needs to read/written from/to the Uint8Array (i.e. packet.data). |
| `packet.length` | number	 | Length of the data to be read for that packet starting from the offset specified. |


<a name="senddata"></a>

### sendDataPacket

Data to be sent to server has the following format.

#### Properties

| Name	| Type	 | Description |
|---|---|---|
| `sendDataPacket.sessionId` | String |	id of the session. |
| `sendDataPacket.streamName` | String	| Virtual channel name. |
| `sendDataPacket.packet` | packet | Packet format to be sent to server. |





