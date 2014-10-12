Microservice communication protocol
======

Binary protocol based on [Protocol Buffers](https://code.google.com/p/protobuf/) inspired by [HTTP](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol).

### Varint

All integers are encoded using varint encoding (encoded integer takes 1 or more bytes).
Smaller numbers take smaller number of bytes.

The encoding used is the same one that is used in Protocol Buffers.

Specification: [http://code.google.com/apis/protocolbuffers/docs/encoding.html](http://code.google.com/apis/protocolbuffers/docs/encoding.html)

### Message

Every message consists of one main message (`Message`) and any number (`n`) of additional headers.
Both headers and the main message (message part in the rest of the document) are using the same encoding.

    +------------+------------+-----------+------------+-------------+
    |  Header 1  |  Header 2  |    ...    |  Header n  |   Message   |
    +------------+------------+-----------+------------+-------------+

### Message part

Every message part starts with `varint` encoded size of the message part.
It is followed by the message part `type` encoded as `varint` and the actual message part `data`.
Size is the sum of `type` and `data` size.

    +-------+------------------------------------+
    |       |+------+---------------------------+|
    | size  || type |           data            ||
    |       |+------+---------------------------+|
    +-------+------------------------------------+
