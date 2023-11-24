# Protocols

### OSI Recap ✅

- **Abstraction or Concept of the Internet**
- **Layers 1 to 7:**
  - Layer 1: Physical
  - Layer 2: Data frames and more
  - Layer 3: IP
  - Layer 4: TCP/UDP, Ports
  - Layer 5: Session layer (e.g., Linkerd)
  - Layer 6: Presentation
  - Layer 7: Application layer (HTTP, HTTPS, etc.)

- **TCP/IP Model**
  - A simplified model focusing on Layers 3/4 & 7

### TCP ✅ (Layer 4)

- **Transmission Control Protocol**
  - Controls transmission, unlike UDP which is like a firehose
  - Connection-oriented
  - Requires a handshake
  - 20-byte header segment
  - Stateful
  - Ideal for reliable communications, SSH, database connections, web communications, etc.
- **TCP Connection**
  - Connection represents a session
  - An agreement between client and server
  - Identified by four properties: SourceIP-SourcePort and DestinationIP-DestinationPort
  - Requires a 3-way TCP handshake (SYN, SYN-ACK, ACK)
  - Segments are sequenced, ordered, acknowledged, and retransmitted if lost
- **Multiplexing and Demultiplexing**
  - Sender multiplexes applications into TCP connections
  - Receiver demultiplexes TCP segments to apps based on connection pairs
- **Connection Establishment**
  - Three-way handshake process described with an example
- **Sending Data**
  - Data encapsulation in segments and acknowledgement process
  - Hint: Can new segments be sent before the acknowledgement of old segments?
- **Handling Lost Data**
  - Resending lost segments
- **Closing Connection**
  - Four-step process: FIN, ACK, FIN, ACK
- **Summary**
  - Layer 4 protocol
  - Introduces the concept of connection
  - Features retransmission, acknowledgement, and guaranteed delivery
  - Stateful with a defined state for connections
- **Pros & Cons of TCP**
  - Pros: Guaranteed delivery, flow control, ordered packets, secure
  - Cons: Larger overhead, higher bandwidth usage, stateful nature, high latency for certain workloads, issues like TCP meltdown


### **UDP ✅ (Layer 4)**

- **User Datagram Protocol**
  - A simple protocol for sending and receiving data.
  - No prior communication required (this can be convenient but also a security risk).
  - Stateless - no information is stored on the host.
  - Features an 8-byte header datagram.
  - Use cases: video streaming, VPN, DNS, WebRTC.
- **Multiplexing & Demultiplexing**
  - Sender multiplexes all its applications into UDP.
  - Receiver demultiplexes UDP datagrams to each application.
- **Source & Destination Port**
  - Example: App1 on 10.0.0.1 sends data to AppX on 10.0.0.2.
  - Destination Port = 53.
  - AppX responds back to App1.
  - Source Port is necessary for return data (e.g., Source Port = 5555).
- **UDP Pros & Cons**
  - Pros:
    - Simplistic protocol.
    - Small header size results in smaller datagrams.
    - Uses less bandwidth.
    - Stateless nature.
    - Consumes less memory (no state stored on server/client).
  - Cons:
    - No acknowledgements (Acks).
    - No guaranteed delivery.
    - Connection-less – anyone can send data without prior knowledge.
    - No flow control.
    - No congestion control.
    - Unordered packets.
    - Security concerns – susceptibility to spoofing.
- **Summary**
  - UDP is a Layer 4 protocol.
  - Utilises ports to address processes.
  - Stateless in nature.


### TLS (Typically Layer 5 due to its stateful nature)

- **Transport Layer Security (TLS)**
  - Generally associated with Layer 5 due to its session management capabilities.

- **Vanilla HTTP**
  - Client sends a GET request (without a body) to the Server.
  - Process:
    - Transforms into a TCP segment.
    - Becomes an IP packet.
  - The server listens on port 80.
  - Server receives the segment and understands the request.
  - The application responds with headers and the requested content (e.g., index.html).

- **HTTPS (HTTP over TLS)**
  - Begins with establishing a connection and performing a handshake.
  - Handshake aims to exchange symmetric keys for encryption.
  - Client's GET request is encrypted using these keys.
  - The server decrypts the received data using the same key.
  - Encryption methods:
    - Symmetric key: The same key is used for both encryption and decryption.
    - Asymmetric keys: Different keys are used for encryption and decryption.

- **TLS 1.2**
  - Uses a private key to encrypt the symmetric key.
  - The Heartbleed OpenSSL bug (2012-2014) led to scepticism about using RSA, as it lacks forward secrecy.

- **Diffie-Hellman Key Exchange**
  - Utilises two private keys and one symmetric key.
  - One private key for the client and one for the server.

- **TLS 1.3 Improvements**
  - An enhanced version using the Diffie-Hellman algorithm.
  - Mathematical basis:
    - Server-side equation: \((g^x \% n)^y = g^{xy} \% n\).
    - Client-side equation: \((g^y \% n)^x = g^{xy} \% n\).
  - TLS 1.3 is currently the preferred standard due to its security and efficiency.



## **HTTP/1.1**

- HTTP request
    - Method (GET, POST, PUT, DELETE, PATCH, OPTIONS)
    - Path (/, /about, etc etc)
    - Protocol (HTTP/HTTP 1.1, HTTP 1.2, gRPC)
    - Headers (key-value, like User-Agent, host header etc)
    - Body (GET request doesn’t have any, POST, DELETE and other methods do)
    - example: `curl -v http://google.com/about`

- HTTP response
    - Protocol (HTTP/1.1, HTTP/2)
    - Code (200, 301, etc etc)
    - Location: url
    - content-type: text/html
    - server: where site is hosted.
    
    HTTPS (port 444 is introduced here too) 
    
    - after TCP, do a TLS handshake
        - in TLS handshake, both the client and the server will agree on the symmetric key (and symmetric encryption is used here, much faster than asymmetric encryption)
        - same key encrypts and same key decrypts - because its same key used, key exchange is critical. so we use something called RSA or diffi hellman to exchange keys
        - then keys are used to encrypt the GET request and headers are sent back and content using encrypted keys
- HTTP 1.0
    - New TCP connection with each request (after each request, the connection is closed to save CPU & memory)
    - Slow
    - Bufferring (trasnfer-encoding: chubked didnt exist)
    - No multi-home websites (HOST header)
    
- HTTP 1.1
    - Persisted TCP connection: Connection is not closed immediately with each request. All use same TCP connection.
    - Low latency & Low CPU usage
    - HTTP request smuggling could happen. When server doesn’t know where requests end or start
    - Streaming with chunked transfer
    - Pipelining (can run multiple requests in parallel without having to wait for response. Disabled by default and not guaranteed it will work correctly
    - Proxying & multi-homed websites (1 IP can host 1000s of websites, the URL of the website is searched when looking for the site and not the IP)
    
- HTTP/2
    - Used to be called SPDY & invented by Google
    - Compression (both headers and the body). Header compression was disabled in HTTP/1 due to an attack called Crime (hackers were able to extract key info due to the way headers were compressed)
    - Multiplexing
    - Sever push
    - Secure by default (coz of protocol ossification)
    - Protocol negotiation during TLS

- HTTP over QUIC (HTTP/3)
    - Replaces TCP with QUIC (UDP with congestion control)
    - All HTTP/2 features
    - Without HOL (head of line blocking?)

## **Websockets**

- Bidirectional communication designed for the web
- Websockets are built on top of HTTP
- HTTP 1.0 (connection is not persistent, keeps closing), HTTP 1.1 (persisitent connection), then an opportunity for websockets coz connection is alive now
- Websocket proces
    - Open connection
    - Websocket handshake (just a HTTP request with a special semantic. You get a connection which now says your connection is now web sockety
    - Because the connection is alive, we can do loads of bidirectional communication. (This couldn’t be done with HTTP 1.0 coz connection is not always alive)
- Websockets handshake
    - ws:// or wss:// (secure version)
    - Client server example
        - Req for websocket
            - GET /chat HTTP/1.1
            - Host: server.exmaple.com
            - websocket
        - Response for ws
            - HTTP/1.1 - 101 Switching protocol code
            - Upgrade: websocket
            - Some more headers like key etc etc
- Use cases: chatting, live feed, multiplayer gaming, showing client progress/logging , whatsApp, discord
- Some other useful info; Ping Pong is sent frequently to keep the websocket connection alive.
- Pros & Cons
    - Pros:
        - Full duplex (no polling) - left and right - bidirectional comms
        - HTTP compatible (more friendly) (note: if you used TCP, you would have to build your own port)
        - Firewall friendly (standard)
    - Cons
        - Proxying is tricky (need to terminate websocket connection & read message & establish another websocket connection
        - L7 LB challenging (due to timeouts) (L4 LB can be done but kind of consuming on the backend)
        - Stateful (knowledge of both client and server), difficult to horizontally scale
- Do you have to use websockets?
    - No
    - Rule of thumb - do you absolutely need bidirectional comms
    - Long polling
    - Plus websockets have extra headers and stuff to be managed. Just extra stuff
    - Server Sent Events
    - Note: Clients are connected to 1 server where messages are received. No one is connected to each other directly except through server where messages are broadcasted
    - 

## **HTTP/2 (improved version of HTTP/1)**

- HTTP 1.1 recap
    - make req, you get 200, OK and get HTML docs (index.html, main.css, main.js, img1.jpg)
    - Browser can can use 6 concurrent request using 6 SEPARATE tcp connections (not sure why 6 but chrome picked it?)

- HTTP/2
    - Send all concurrent requests using same TCP connection.
    - Every request is tagged with a unique stream ID
    - Client uses odd stream ID numbers to send (thats how you know its the client sending
    - and the Server sends responses using an even stream ID number to send back responses
- HTTP/2 Push
    - legacy and not commonly used
    - Push mechanism is not scaleable
- Pros
    - Multiplexing over single connection (save resources - 1 connection instead of 6 resources like in HTTP/1.1)
    - Compress both headers and data/body
    - Server Push
    - secure by default (because of protocol ossification)
    - Protocol negotiataion during TLS
- Cons
    - TCP head of line blocking (when you send a request like 5/6 streams and you send in order, the TCP will label the bytes/segments in order. For e.g. if you send 10 requests and lets say the first req is dropped. If the server recieves req 2-10, the server will not process any of them.
    - Server push never picked up
    - High CPU usage
    
- Main reason why HTTP/2 was designed was because the client sends a lot of requests in the same connection. That’s the only reason why it was built. Because we want to send multiple requests concurrently.

## HTTP/3 - HTTP over QUIC multiplexed streams

- HTTP 1.1 recap
    - using 1 connection per request (slow)

- How HTTP/2 works? Recap
    - multiple streams for requests in 1 connection

- HTTP/2 cons recap
    - TCP head of line blocking
        - TCP segments must be delivered in order
        - but streams dont have to
        - blocking requests
- 

- How HTTP/3 & QUIC saves the day
    - HTTP/3 is built on top of QUIC (and QUIC is built on UDP)
    - like HTTP/2, QUIC has streams
    - but QUIC uses UDP instead
    - HTTP/3 streams - (the request are now datagrams instead of TCP segments)
        - QUIC manages the streams and sequences (its kind of like a “TCP connection” for each stream
- Pros
    - Merges connection setup & TLS in one handshake (secure by default), I want QUIC to be secure by default
    - TLS 1.3 and the handshake in one handshake. So one round trip give you a connection setup, the security and the encryption
    - Congestion control at stream level
    - Connection migration (coz UDP is stateless, we have to send the connectionID with every single packet we send. The connectionID is used to uniquely identify the connection. So multiple connections can be running. And coz we send the connectionID, every datagram is labelled with the connectionID, every datagram is labelled with the streamID
        - Interestingly, the connectionID is not encrypted and is in plaintext. There’s a paper talking about connection hijacking
    - Why not HTTP/2 over QUIC?
        - Header compression algorithm

- Cons
    - Takes a lot of CPU (due to parsing logic), more than HTTP/2
    - UDP could be blocked (sometimes proxies like in enterprise systems block UDP
    - IP fragmentation issues (coz QUIC uses UDP and UDP has no order etc, segments can be spoofed etc etc)
    - 

- Interesting; QUIC is actually the reverse of HTTP/2 - odd streams are server while even streams are the client
- QUIC is a connection based system. Yes it’s built on top of UDP, they built this virrtual connection concept at the endpoint

## **gRPC (Google remote procedural call)**

- built on top of HTTP
- takes advantage of HTTP/2 streams feattures to give various features such as bidirectional.
- All in 1 protocol??

- Client server comms
    - SOAP, REST< GraphQL
    - SSE, WebSockets
    - raw TCP
- Problerm with client librarries
    - each library has its own language
    - patching issues etc etc

- why gRPC was invvented?
    - one library for popular langs
        - 
    - Protocol: HTTP/2 (hidden implementation)
    - Message format: protocol buffers as format
- gRPC modes
    - unary RPC (basically req response)
    - server streaming RPC
    - client streaming RPC
    - bidirectional streaming RPC

- Pros
    - Fast & compact
    - One client library
    - Progress feedback (upload)
    - Cancel req (H2)
    - H2/protobuf

- Cons
    - Schema
    - Thick client
    - proxies are tricky to implement in gRPX but its been done
        - can do L7 LB/reverse proxy using nginx with gRPC but its tricky.
        - you can build a gRPC web proxy, where you can point your web app to the gRPC proxy and proxy will convert them into an actual gRPC course (like a sidecar pattern)
    - error handling (need to build your own, no native one)
    - no native browser support
        - (gRPC is entrenched to HTTP/2, uses low level calls to HTTP/2 streams
        - those APIs dont exist in the browser because hte browser doesn’t expose them
        - 
    - timeouts (pub/sub)

- Can I write my own protocol?
    - yes, you can. Spotify did something similar. Look at “The Story of Whhy we migrate to gRPC and How We Go about it” talk in kubecon Europe 2019 (Matthias Gruter, Spotify)
    - Their protocol was called Herms (written in 2012, based on zeroMQ, JSON or Protobuf payload, not a PRC framework
    - Spotify moved to gRPC eventually not because of limitation of Hermes but because they are isoalated. gRPC is most popular.

- gRPC is most popular in microservices now. if 2 services want to talk to each other, the de-facto is gRPC.

--------

## **Many ways to HTTPS**

**HTTP Communication basics**

- Establish connection with backend
- establish encryption (HTTPS right. TLS!)
- Send data
- Close connection (when done)

**HTTPS over TCP with TLS1.2**

- TCP connect (syn syn/ack ack) >> establish TCP connection
- handshake (client hello, server hello, client fin, server fin) >> client and server do handshake in order to agree on symmetric key. They both do key exchange algorithm and both have the symmetric key for encrypting and decrypting
- data send (GET /, 200 OK)

**HTTPS over TCP with TLS 1.3**

- same as HTTPS over TCP with TLS 1.2 but with one less roundtrip (on the key exchange part)
- better to use TLS 1.3 unless you have a backward compatibility issue

**HTTPS over QUIC aka HTTP/3** 

- the 3 way handshake and the TLS handshake happens in the same router. It’s a matter of carrying the same packets in the same time
- so we effectively combined TLS 1.3 with the handshake of QUIC
- all of it is built on UDP
- so all of the requests are a bunch of UDP segments - datagrams going back and forth

**HTTPS over TFO with TLS 1.3 (TCP Fast Open, not really secure)**

- 

**HTTP over TCP with TLS1.3 0RTT (0 round trip)**

- if a prior TLS connection existed between client and server, a pre shared key could have been shared to the client
- 0 round trip so less waiting time so less latency

**HTTPS over QUIC 0RTT**

- if pre shared key was shared before and client knows about it, it can effectively send the QUIC handshake
- This is the fastest you can go. You can set the connection req for QUIC, in the same breath, send TLS - use pre-shared key to encrypt and also send GET req in the same breath.
- if this can be done, you can get extreme response time! very very fast
- so far only Cloudflare can manage to do this effectively in their environment (read article by Cloudflare called “Even faster connection with QUIC 0-RTT resumption”
- This is quite difficult to do but really fast.
