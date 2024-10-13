---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# OSI Model

Open Systems Interconnection Model, is a standardized model used to demonstrate the theory behind computer networking. Every layer adds a header to the data except for the Data Link Layer which also adds a trailer. Consist of 7 layers:

<table><thead><tr><th width="106" align="center">Layer #</th><th width="141" align="center">OSI Layer</th><th width="298" align="center">Function</th><th align="center">Data Unit Name</th></tr></thead><tbody><tr><td align="center">7</td><td align="center">Application</td><td align="center">Provides networking options to programs running on a computer, and provides an interface for them to use to transmit the data</td><td align="center">Data</td></tr><tr><td align="center">6</td><td align="center">Presentation</td><td align="center">Translates the data into a standardized format, as well as handling any encryption, compression, or other transformations to the data</td><td align="center">Data</td></tr><tr><td align="center">5</td><td align="center">Session</td><td align="center">Maintain connection and synchronize communications with other devices across the network. Also informs if a connection can't be established</td><td align="center">Data</td></tr><tr><td align="center">4</td><td align="center">Transport</td><td align="center">Choose the protocol over which the data is to be transmitted (UDP or TCP), divide the transmission up into bite-sized pieces</td><td align="center">Segments/Datagrams</td></tr><tr><td align="center">3</td><td align="center">Network</td><td align="center">Locates the destination of your request, taking the IP address, and figuring out the best route to take, handles logical addressing</td><td align="center">Packets</td></tr><tr><td align="center">2</td><td align="center">Data Link</td><td align="center">Receives a packet from the network layer and adds it to the physical MAC address of the receiving endpoint. Check the received information to make sure that it hasn't been corrupted during transmission and present the data in a format suitable for transmission</td><td align="center">Frames</td></tr><tr><td align="center">1</td><td align="center">Physical</td><td align="center">Convert the binary data of transmission into signals and transmit them across the network, as well as receiving incoming signals and converting them back into binary data</td><td align="center">Bits</td></tr></tbody></table>
