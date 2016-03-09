##Computer Network
###TCP 3-way handshake
####Definition - What does Three-Way-Handshake mean?
- Before the sending device and the receiving device start the exchange of data, both devices need to be synchronized
- A three-way-handshake is a method used in a TCP/IP network to create a connection between a local host/client and server. It is a three-step method that requires both the client and server to exchange SYN and ACK (acknowledgment) packets before actual data communication begins.
A three-way-handshake is also known as a TCP handshake.

####Explain
- A three-way-handshake is primarily used to create a TCP socket connection. It works when:
- A client node sends a SYN data packet over an IP network to a server on the same or an external network. The objective of this packet is to ask/infer if the server is open for new connection.
- The target server must have open ports that can accept and initiate new connections. When the server receives the SYN packet from the client node, it responds and returns a confirmation receipt - the ACK packet or SYN/ACK packet.
- The client node receives the SYN/ACK from the server and responds with an ACK packet

[example](http://www.omnisecu.com/tcpip/tcp-three-way-handshake.php)

###TCP UDP
Transmission Control Protocol (TCP) and User Datagram Protocol (UDP) are the major protocols operating at Transport Layer.
####TCP
- TCP stands for Transmission Control Protocol and it guarantees delivery of data packets. This protocol provides extensive error checking mechanisms such as flow control and acknowledgment of data.
- Transmission Control Protocol (TCP) is a connection oriented protocol. Before transmitting data, a connection must be established between the devices participating in data transmission. If your Application require guaranteed delivery of data, then you must choose TCP as the Transport layer protocol.

####UDP
- UDP stands for User Datagram Protocol and it operates in Datagram mode. The main difference you should notice here is User Datagram Protocol (UDP) is a connection-less protocol. User Datagram Protocol (UDP) has only the basic error checking mechanism using checksums.

####TCP VS UDP
- Transmission Control Protocol (TCP) is a connection oriented protocol, which means the devices should open a connection before transmitting data and should close the connection gracefully after transmitting the data, while UDP is not
- Transmission Control Protocol (TCP) assure reliable delivery of data to the destination, while UDP does not
- Transmission Control Protocol (TCP) protocol provides extensive error checking mechanisms such as flow control and acknowledgment of data, while UDP just provides basic error checking
- Sequencing of data is a feature of Transmission Control Protocol (TCP), but there is no sequencing of data in UDP
- Transmission Control Protocol (TCP) is comparatively slow because of these extensive error checking mechanisms, while UDP is faster
- Retransmission of lost packets is possible in Transmission Control Protocol (TCP). There is no retransmission of lost packets in User Datagram Protocol (UDP).


###http / https
[http / https](https://www.instantssl.com/ssl-certificate-products/https.html)
###Http
Client and server agreed on a procedure for exchanging information and called it HyperText Transfer Protocol (HTTP).
- HyperText Transfer Protocol (HTTP) use port 80

####Https
-  HyperText Transfer Protocol Secure (HTTPS).  is the secure version of HTTP, use port 443
-  It means all communications between your browser and the website are encrypted
-  Using HTTPS, the computers agree on a "code" between them, and then they scramble the messages using that "code" so that no one in between can read them. This keeps your information safe from hackers.
- HTTPS is often used to protect highly confidential online transactions like online banking and online shopping order forms.

####How does Https work
HTTPS pages typically use one of two secure protocols to encrypt communications - SSL (Secure Sockets Layer) or TLS (Transport Layer Security). Both the TLS and SSL protocols use what is known as an 'asymmetric' Public Key Infrastructure (PKI) system. An asymmetric system uses two 'keys' to encrypt communications, a 'public' key and a 'private' key. Anything encrypted with the public key can only be decrypted by the private key and vice-versa.

As the names suggest, the 'private' key should be kept strictly protected and should only be accessible the owner of the private key. In the case of a website, the private key remains securely ensconced on the web server. Conversely, the public key is intended to be distributed to anybody and everybody that needs to be able to decrypt information that was encrypted with the private key.

####Https certificate
When you request a HTTPS connection to a webpage, the website will initially send its SSL certificate to your browser. This certificate contains the public key needed to begin the secure session. Based on this initial exchange, your browser and the website then initiate the 'SSL handshake'. The SSL handshake involves the generation of shared secrets to establish a uniquely secure connection between yourself and the website.

When a trusted SSL Digital Certificate is used during a HTTPS connection, users will see a padlock icon in the browser address bar. When an Extended Validation Certificate is installed on a web site, the address bar will turn green.

####Why Is an SSL Certificate Required?
All communications sent over regular HTTP connections are in 'plain text' and can be read by any hacker that manages to break into the connection between your browser and the website. This presents a clear danger if the 'communication' is on an order form and includes your credit card details or social security number. With a HTTPS connection, all communications are securely encrypted. This means that even if somebody managed to break into the connection, they would not be able decrypt any of the data which passes between you and the website.



3.输入www.google.com 会发生什么；What happens when you type [url]www.google.com in your browser?[/url]

####Post vs Get

#### HTTP Status Messages

|HTTP Status|Description|Message|
|------|----|--------|
|200|The request is OK (this is the standard response for successful HTTP requests)|OK|
|301|The requested page has moved to a new URL | Moved Permanently|
|304|Indicates the requested page has not been modified since last requested|Not Modified|
|400|The request cannot be fulfilled due to bad syntax|Bad Request|
|401|The request was a legal request, but the server is refusing to respond to it, For use when authentication is possible but has failed or not yet been provided|Unauthorized|
|403|The request was a legal request, but the server is refusing to respond to it|Forbidden|
|404|The requested page could not be found but may be available again in the future|Not Found|
|500|A generic error message, given when no more specific message is suitable|Internal Server Error|


####What is URL?

	http://www.github.com:8080/index.html?user=rwang23&lang=zh-CN#home
	  |          |          |       |                  |          |
	protocol     |          |       |                  |          |
	          hostname     port     |                  |          |
	              \        /    pathname             search      hash
	                 host

###Client Server Model
[Client-Server Model](https://www.techopedia.com/definition/18321/client-server-model)
####Definition - What does Client-Server Model mean?
The client-server model is a distributed communication framework of network processes among service requestors, clients and service providers. The client-server connection is established through a network or the Internet.

The client-server model is a core network computing concept also building functionality for email exchange and Web/database access. Web technologies and protocols built around the client-server model are:
- Hypertext Transfer Protocol (HTTP)
- Domain Name System (DNS)
- Simple Mail Transfer Protocol (SMTP)
- Telnet

Clients include Web browsers, chat applications, and email software, among others. Servers include Web, database, application, chat and email, etc.

####Explains Client-Server Model

A server manages most processes and stores all data. A client requests specified data or processes. The server relays process output to the client. Clients sometimes handle processing, but require server data resources for completion.

The client-server model differs from a peer-to-peer (P2P) model where communicating systems are the client or server, each with equal status and responsibilities. The P2P model is decentralized networking. The client-server model is centralized networking.
One client-server model drawback is having too many client requests underrun a server and lead to improper functioning or total shutdown. Hackers often use such tactics to terminate specific organizational services through distributed denial-of-service (DDoS) attacks.



##系统及其它
ACID/CAP 分布式系统
Java多线程： extend Tread类，Implement Runnable接口/blockingqueue
序列化的几种方式：JSON／Object Serialize／ProtoBuf
what is dead lock?死锁问题／如何解决
Design Pattern 设计模式（singleton，factory, builder, decorator）
Linux command: kill -9   / scp / telnet / ps
