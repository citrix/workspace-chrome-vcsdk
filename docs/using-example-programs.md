# Using example programs

* Provide working examples of code that can be modified to suit your requirements.
* Explore the features and functionality provided in the Virtual Channel SDK.








```
Byte 0-1 uSign; // Signature





```
Byte 0-1 uType // Packet type
The data consists of the structure above followed by the arguments to the function being called. uLen is the total length of the data being sent, including the arguments. DwLen1 is the length of the data pointed to by a pointer argument.


![](./mix.png)

## Over







```
Byte 0-1 uSign; // Signature

### Packet Format - From Client to Server
Byte 0-1 uType; // Type OVERFLOW\_JUMP from client

### Sequence of Events


![](./over.png)