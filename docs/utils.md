# Utils

## new Utils()

### Methods

	(inner) readUint8(buffer, offset) → {number}

Reads 1 byte of data from the Uint8Array passed.

### Parameters

| Name | Type | Description |
|------|------|-------------|
| `buffer` |	Uint8Array | Uint8Array from which the data needs to read. |
| `offset` |	number	| Offset from where the Uint8Array needs to be read.|

### Throws

* ReceiverError

### Returns

1 byte of data read.

#### Type
* number

### Example

```
//Creating sample Uint8Array of length 20 and reading total of 2 bytes of data. In real use case the input would be received from the server.
var input = new Uint8Array([1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]);		
//Setting offset to 0 as we are reading from beginning.
var offset = 0;

//Reading first byte of data
var num1 = citrix.receiver.utils.readUint8(input,offset);
//Incrementing offset by 1 as we read 1 byte of data.
offset +=1;

//Reading second byte of data
var num2 = citrix.receiver.utils.readUint8(input,offset);
//Incrementing offset by 1 as we read 1 byte of data.
offset +=1;
```
## (inner) readUint16(buffer, offset) → {number}

Reads 2 bytes of data from the Uint8Array passed.

### Parameters

| Name | Type | Description |
|------|------|-------------|
| `buffer` |	Uint8Array | Uint8Array from which the data needs to read.|
| `offset` | number	| Offset from where the Uint8Array needs to be read.|

### Throws

* ReceiverError

### Returns

2 bytes of data read.
#### Type

* number

### Example

```
//Using sample Uint8Array created in readUint8 example and reading total of 4 bytes of data. In real use case the input would be received from the server.
//offset will be 2 after reading 2 bytes from previous example of readUint8		

//Reading first 2 bytes of data
var num1 = citrix.receiver.utils.readUint16(input,offset);
//Incrementing offset by 2 as we read 2 bytes of data.
offset +=2;

//Reading next 2 bytes of data
var num2 = citrix.receiver.utils.readUint16(input,offset);
//Incrementing offset by 2 as we read 2 bytes of data.
offset +=2;
```
## (inner) readUint24(buffer, offset) → {number}

Reads 3 bytes of data from the Uint8Array passed.

### Parameters

| Name | Type | Description |
|------|------|-------------|
| `buffer` |	Uint8Array | Uint8Array from which the data needs to read. |
| `offset` | number	| Offset from where the Uint8Array needs to be read. |

### Throws

* ReceiverError

### Returns

3 bytes of data read.

#### Type
* number

### Example

```
//Using sample Uint8Array created in readUint8 example and reading total of 6 bytes of data. In real use case the input would be received from the server.
//offset will be 6 after reading 4 bytes from previous example of readUint16

//Reading 3 bytes of data
var num1 = citrix.receiver.utils.readUint24(input,offset);
//Incrementing offset by 3 as we read 3 bytes of data.
offset +=3;

//Reading next 3 bytes of data
var num2 = citrix.receiver.utils.readUint24(input,offset);
//Incrementing offset by 3 as we read 3 bytes of data.
offset +=3;
```

## (inner) readUint32(buffer, offset) → {number}

Reads 4 bytes of data from the Uint8Array passed.

### Parameters

| Name | Type | Description |
|------|------|-------------|
| `buffer` |	Uint8Array | Uint8Array from which the data needs to read. |
| `offset` | number	| Offset from where the Uint8Array needs to be read. |

### Throws

* ReceiverError

### Returns

4 bytes of data read.

#### Type
* number

#### Example

```
//Using sample Uint8Array created in readUint8 example and reading total of 8 bytes of data. In real use case the input would be received from the server.
//offset will be 12 after reading 4 bytes from previous example of readUint24

//Reading 4 bytes of data
var num1 = citrix.receiver.utils.readUint32(input,offset);
//Incrementing offset by 4 as we read 4 bytes of data.
offset +=4;

//Reading next 4 bytes of data
var num2 = citrix.receiver.utils.readUint32(input,offset);
//Incrementing offset by 4 as we read 4 bytes of data.
offset +=4;
//Reached end of length of Uint8Array.
```
## (inner) writeUint8(buffer, offset, num) → {number}

Write 1 byte of data to the Uint8Array passed with the number at index set by offset.

### Parameters

| Name | Type | Description |
|------|------|-------------|
| `buffer` |	Uint8Array | Uint8Array from which the data needs to read. |
| `offset` | number	| Offset from where the Uint8Array needs to be read. |
| `num` |	number	| Data that needs to be written into the Uint8Array. |

### Throws

* ReceiverError

### Returns

`offset` at which the next write can be written. 

#### Type
* number

#### Example

```
//Creating empty Uint8Array with length of 20 and writing 2 bytes of data. Recommended way to construct reply data to server.
var length = 20; //Length of data packet.
var input = new Uint8Array(length);
//Setting offset to 0 as we are writing from beginning.
var offset = 0;
var number1 = 100;//Data to be written

//Writing first byte of data and storing the offset returned for next write.
offset = citrix.receiver.utils.writeUint8(input,offset,number1);

var number2 = 25;
//Writing second byte of data by passing the offset received from previous call.
offset = citrix.receiver.utils.writeUint8(input,offset,number2);
```

## (inner) writeUint16(buffer, offset, num) → {number}

Writes 2 bytes of data to the Uint8Array passed with the number at index set by offset.

### Parameters

| Name | Type | Description |
|------|------|-------------|
| `buffer` |	Uint8Array | Uint8Array from which the data needs to read. |
| `offset` | number	| Offset from where the Uint8Array needs to be read. |
| `num` |	number	| Data that needs to be written into the Uint8Array. |

### Throws

* ReceiverError

### Returns

`offset` at which the next write can be written. 

#### Type
* number

#### Example

```
//Using the Uint8Array created in example writeUint8 and writing 6 bytes of data. Recommended way to construct reply data to server.		

//offset will be 2 in continuation with previous example of writeUint8
		
var number1 = 400;//Data to be written

//Writing 2 bytes of data at index 2 and storing the offset returned for next write.
offset = citrix.receiver.utils.writeUint16(input,offset,number1);

var number2 = 4;
//Writing next two bytes of data by passing the offset received from previous call.
offset = citrix.receiver.utils.writeUint16(input,offset,number2);
```

## (inner) writeUint24(buffer, offset, num) → {number}

Writes 3 bytes of data to the Uint8Array passed with the number at index set by offset.

### Parameters

| Name | Type | Description |
|------|------|-------------|
| `buffer` |	Uint8Array | Uint8Array from which the data needs to read. |
| `offset` | number	| Offset from where the Uint8Array needs to be read. |
| `num` |	number	| Data that needs to be written into the Uint8Array. |

### Throws

* ReceiverError

### Returns

`offset` at which the next write can be written. 

#### Type
* number

#### Example

```
//Using the Uint8Array created in example writeUint8 and writing 6 bytes of data. Recommended way to construct reply data to server.		

//offset will be 6 in continuation with previous example of writeUint16

var number1 = 70;//Data to be written

//Writing 3 bytes of data at index 6 and storing the offset returned for next write.
offset = citrix.receiver.utils.writeUint24(input,offset,number1);

var number2 = 67;
//Writing next three bytes of data by passing the offset received from previous call.
offset = citrix.receiver.utils.writeUint24(input,offset,number2);
```

## (inner) writeUint32(buffer, offset, num) → {number}

Writes 4 bytes of data to the Uint8Array passed with the number at index set by offset.

### Parameters

| Name | Type | Description |
|------|------|-------------|
| `buffer` |	Uint8Array | Uint8Array from which the data needs to read. |
| `offset` | number	| Offset from where the Uint8Array needs to be read. |
| `num` |	number	| Data that needs to be written into the Uint8Array. |

### Throws

* ReceiverError

### Returns

`offset` at which the next write can be written. 

#### Type
* number

#### Example

```
//Using the Uint8Array created in example writeUint8 and writing 8 bytes of data. Recommended way to construct reply data to server.		
//offset will be 12 in continuation with previous example of writeUint24

var number1 = 110;//Data to be written

//Writing 4 bytes of data at index 12 and storing the offset returned for next write.
offset = citrix.receiver.utils.writeUint32(input,offset,number1);

var number2 = 56;
//Writing next four bytes of data by passing the offset received from previous call.
offset = citrix.receiver.utils.writeUint32(input,offset,number2);	
//Reached end of length of Uint8Array.
```
