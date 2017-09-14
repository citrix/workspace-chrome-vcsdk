# Namespace: receiver

## receiver

`citrix.receiver`

## Members

### (static) Utils

Utils to read/write from/to an Uint8Array.Supported reading/writing of 1-4 bytes of data.
Refer to individual api examples to construct/parse the packet as per structure. 
You may refer sample VC examples (ping, mix and over) provided for more details on usage.

#### Properties

| Name | Type | Description |
|----|----|----|
| [utils](./utils.md) | Object | Object of Utils |

### (readonly) apiVersion

#### Properties

| Name | Type | Description |
|----|----|----|
| `apiVersion` |	String	| Virtual Channel SDK for Chrome version. |

## Methods

### (static) registerVC(vcInfo) → {CustomVC}

Registers the handlers for the virtual channel and returns the object that needs to be stored. 

!!!tip "Note"
	All the sessions would use the same callbacks for each functionality.Session id should be used to differentiate between different sessions.

#### Parameters

| Name | Type | Description |
|----|----|----|
| `vcInfo` |	Object | Object containing the details of the virtual channel name, version, description and the callbacks for various functionalities |

##### Properties of vcInfo

| Name | Type | Attributes| Description |
|----|----|----|----|
| `streamName` |	String	| Virtual Channel name. |Should be an ASCII string with a maximum of 7 letters. |
| `description`	| String	| <optional> | Description of the Virtual channel |
| `minVersion` |	String	| <optional> | Lowest supported version of this virtual channel, used to allow version negotiation between the client-side and the server-side components. |
| `maxVersion` |	String	| <optional> | Highest supported version of this virtual channel, used to allow version negotiation between the client-side and the server-side components.|
| `driverOpen` |	[driverOpen](./global/#driveropen) |	| Callback that gets called when the virtual channel is about to be opened in the session. Will be called for each session launch. |
| `driverInfo` |	[driverInfo](./global/#driverinfo) | | Callback that gets called to send any information about the virtual channel.Will be called for each session launch. |
| `icaDataArrival`	| [icaDataArrival](./global/#icadata) | | Callback set for receiving the ica packet from the server side component of virtual channel.|
| `driverClose`	| [driverClose](./global/#driverclose)	 |  | Callback set for receiving the virtual channel close in the session. |

#### Throws

Error during registration of Virtual Channel.

#### Type

[ReceiverError](./receiver-error.md)

#### Returns

Object of [CustomVC](./customvc.md).

#### Type

[CustomVC](./customvc.md)

#### Example

```
//Registering CTXPING virtual channel
	var ctxping = citrix.receiver.registerVC({"streamName":"CTXPING",
					 	"driverOpen":pingDriverOpen,
						"driverInfo":pingDriverInfo,
						"icaDataArrival":pingIcaDataArrival,
						"driverClose":pingDriverClose});
```
