- balance request between multiple backends on the backend, while a reverse proxy doesn’t have to balance, it makes requests on your behalf (but the RP doesn’t have balancing logic necessarily
- So every load balancer is a reverse proxy but not every reverse proxy is a load balancer

- L4 vs L7

- Load balancer (aka fault tolerant system)
    - LB/reverse proxy starts multiple TCP connections with each backend server (this is known as warrming up, keeping things hot) -
    

### **Layer 4 LB (L4 is stateful)**

- when a client connects to the L4 LB, the LB chooses one server and all segments for that connections go that server. That connection will have state and it will tag it to one and only 1 connection coz L4 only deals with ports, IP addresses
- there’s also something called a NAT mode which makes everything into a single TCP connection
- TCP connection is taken to reverse proxy then the reverse proxy rewrites it into a brand new TCP connection

- Pros
    - simpler load balancing (simple coz it doesn’t do with the data and mainly the ports, IP addresses and TCP connections, does not understand L7 content is)
    - efficient (no data lookup, just looks at ports and IPs)
    - more secure (with L7, data needs to be decrypted and encrypted but in L4 none of that is needed coz its end to end)
    - works with any protocol (coz it doesn’t look at the content, its agnostic. you send segments and it sends it back to the server)
    - one TCP connection (NAT)

- Cons
    - No smart load balancing
    - Not applicable for micro services
    - Sticky per connection (requests only go to one connection per server)
    - No caching (coz you dont know what data is there, cant cache)
    - Protocol unaware (can be dangerous) bypass rules - instead you need to play with ports

- If you are using L7 and want to support any protocol you use move to L4
    - but once you move to L4, any L7 LB logic you have like blocking users or any auth methods, block certain headers, you cant do anymore of that
- and you can just downgrade the protocol using the HTTP UPGRADE method for other protocols.
    - 

### **Layer 7 LB**

- same concept, uses TCP connection
- when a client connects to the L7 LB, it becomes protocol specific. Any logical “request” will be forwarded to a new backend server. This could be more one or more segments
    - logical requests will be buffered and will be loaded by the L7 LB in the middle
    - the data needs to be read and if it’s encrypted, it needs to decrypt the data
    - and to decypt the data, you need to have a secure connection between you and the LB server
    - that means if you ever want to host a site, the cert has to live in the L7 LB. People dont like that coz your private key has to live in the L7
- the LB parses and understands the segments. HTTP is stateless so i can pick another server
- and this is how the HTTP smuggling attacks happen

- Pros
    - Smart load balancing (due to paths, diff rules) like you are going to /about, i can take you to this server and if you’re going to /contactus, i can take you to this server etc
    - Caching/CDN -
    - Great for micro services
    - API gateway logic
    - Auth

- Cons
    - Expensive (looks at data, decrypt, encrypt)
    - Decrypts (decrypting content, terminates the address, so it terminates TLS - thats why its called TLS Terminator) - L7 LB is always called TLS terminator coz it always terminates connection
    - 2 TCP connections (not sure if its really a con)
    - must share TLS cert
    - Needs to buffer (it needs to read the request once it arrives from the client, LB can be a bottleneck and could slow things down)
    - needs to understand the protocol (people always ask NGINX and HAProxy to support different protocols - YOU simply cannot do L7 LB if the LB does not understand the protocol) we need to undestand the protocol coz we are reading the data so we need to know how to read and respond to the data.


## **NGINX**

What is Nginx?

- web server
    - serves web content
    - listens on an HTTP endpoint

- reverse proxy
    - load balancing
    - backend routing
    - Caching
    - API gateway

- concepts
    - nginx frontend: communication with the client
    - nginx backend: communication with the backend servers

- L4 and L7 recap
    - L4 (TCP)
        - IP, TCP, ports
    - L7 (HTTP)
        - more context, app info, HTTP req etc

- TLS Termination
    - Nginx has TLS
    - NGINX terminates TLS, decrypts, optionally rewrite and then re-encrypt the content to the backend
    - need to look at a method of creating certs or vertifying the nginx - nginx can create its own key or cert?

- TLS passthrough
    - backend is TLS
    - NGINX proxies/streams the packets directly to the backende
    - just like a tunnel - the nginx does not decrypt any data
    - no cahcing, L4 check only but more secure. NGINX doesn’t need the backend cert here.
        - here you cant cache coz the nginx cant see the L7 content anymore. so only pure L4 checks only

- Nginx architecture
