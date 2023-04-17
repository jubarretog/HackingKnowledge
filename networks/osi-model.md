# OSI Model

Open Systems Interconnection Model, is a standardised model which used to demonstrate the theory behind computer networking. Every layer add a header to the data except for Data link Layer which also add a trailer.

* Consist of 7 layers

| Layer # |   OSI Layer  |                                                                                                                                Function                                                                                                                               |      Data name     |
| :-----: | :----------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :----------------: |
|    7    |  Application |                                                                    Provides networking options to programs running on a computer, provides interface for them to use in order to transmit the data                                                                    |        Data        |
|    6    | Presentation |                                                                  Translates the data into a standardised format, as well as handling any encryption, compression or other transformations to the data                                                                 |        Data        |
|    5    |    Session   |                                                               Maintain connection and synchronise communications with other device across the network. Also informs if connection couldn't be stablished                                                              |        Data        |
|    4    |   Transport  |                                                                     Choose the protocol over which the data is to be transmitted (UDP or TCP), divides the transmission up into bite-sized pieces                                                                     | Segments/Datagrams |
|    3    |    Network   |                                                                    Locating the destination of your request, takes the IP address and figures out the best route to take, handles logical adressing                                                                   |       Packets      |
|    2    |   Data Link  | Receives a packet from the network layer and adds it in the physical MAC address of the receiving endpoint. Checks the received information to make sure that it hasn't been corrupted during transmission and present the data in a format suitable for transmission |       Frames       |
|    1    |   Physical   |                                               Convert the binary data of transmission into signals and transmit them across the network, as well as receiving incoming signals and converting them back into binary data                                              |        Bits        |

