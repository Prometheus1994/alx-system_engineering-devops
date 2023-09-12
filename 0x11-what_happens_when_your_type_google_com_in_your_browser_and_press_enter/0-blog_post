# STEP 1: THE DNS.

Domain Name System is like an address book for websites. When you type a web address in your browser(www.google.com), the browser looks at the DNS to find the website’s IP address before it can retrieve the website. The browser needs to find out which server the website lives on, so it can send HTTP messages to the right place (the diagram above illustrates).

Web addresses aren’t that appealing, the strings you type into your address bar to find your favorite website (www.google.com). DNS servers translate requests for names into IP addresses, controlling which server an end user will reach when they type a domain name into their web browser. These requests are called queries.

# STEP 2: TCP/IP

TCP/IP stands for Transmission Control Protocol/Internet Protocol and is a suite of communication protocols used to interconnect network devices on the internet. TCP/IP is also used as a communications protocol in a private computer network. Having resolved the IP address associated with www.google.com, Browser begins communicating with the corresponding servers.

TCP, (transport-layer) protocol, is responsible for establishing the connection between the client and server. TCP is defined by its reliability — packet (ie. request/response data) delivery in TCP is guaranteed, even if it takes more time. An alternative transport-layer protocol, User Datagram Package (UDP) is faster but less reliable — packet delivery is not double-checked. UDP is typical of streaming services where instant content takes priority; TCP is used most everywhere else.

IP addresses are unique to computers and are representative of the network addressing and routing that guide the destination points of TCP.

Here the browser communicates with the server hosting www.google.com over TCP.

# STEP 3: SSL/HTTPS

SSL stands for Secure Socket Layer. It is responsible for protecting sensitive information as it travels through the network. it is essential for protecting our website(www.google.com), it provides privacy, critical security, and data integrity for the website and personal information.

The browser sends to the resolved IP address of www.google.com the message containing Transport Security Layer(TLS a symmetric cryptography encryption method used to keep communication data secure).

Upon receiving this initial communication, the server chooses its preferred TLS algorithm and method and responds with a certificate and a security approval including the server’s TLS public key. Back at the client side, the browser uses this public key to encrypt a pre-master key that is sent back to the server.

If the public key sent to our browser was authentic, then the server is able to decrypt the pre-master key with its TLS private key. Upon proof of successful decryption, the browser and server have effectively established a trusted connection and symmetric method of sending messages back and forth.

This entire security process is referred to as the TLS handshake and is responsible for that cool green lock displayed in your browser whenever you connect to a website through HTTPS.

    The HTTPS

Hyper Text Transfer Protocol Secure (HTTPS) is the secure version of HTTP, the protocol over which data is sent between the browser and the website to that you are connected(www.google.com). The ‘S’ at the end of HTTPS stands for ‘Secure’. It means all communications between your browser and the website are encrypted. HTTPS is often used to protect highly confidential online transactions like online banking and online shopping order forms.

Web browsers normally display a padlock icon in the address bar to visually indicate that an HTTPS connection is in effect.
HTTPS encryption.

HTTPS works as follows;

HTTPS pages typically use one of two secure protocols to encrypt communications — SSL (Secure Sockets Layer) or TLS (Transport Layer Security). Both the TLS and SSL protocols use what is known as an ‘asymmetric’ Public Key Infrastructure (PKI) system. An asymmetric system uses two ‘keys’ to encrypt communications, a ‘public’ key and a ‘private’ key. Anything encrypted with the public key can only be decrypted by the private key and vice-versa.

As the names suggest, the ‘private’ key should be kept strictly protected and should only be accessible to the owner of the private key. In the case of a website, the private key remains securely ensconced on the web server. Conversely, the public key is intended to be distributed to anybody and everybody that needs to be able to decrypt information that was encrypted with the private key.

In a nutshell, the browser sends a TLS-encrypted HTTP GET request to the resolved IP of www.google.com to fetch the web page configured at the root of the host server.

# STEP 4: LOAD-BALANCER

It is estimated that 4.3 billion users around the globe use google hence the need to use load balancers to handle such huge traffic. Google our host has many servers hence web traffic needs to be distributed to these servers, and that is the role of a load-balancer.
An illustration of how a load balancer works.

When you have an enterprise application or website that gets a lot of hits, your server might be under heavy load. In that case, you may want to consider distributing the load across multiple servers.

The load balancer will distribute the workload of your system to multiple individual systems, or groups of systems to reduce the amount of load on an individual system, which in turn increases the reliability, efficiency, and availability of your enterprise application or website.

Backtracking in our example, the resolved IP address of www.google.com was truly the IP address of the load balancer server. Browser completed the TLS handshake with this load balancer server, thus making it the TLS termination proxy. Almost like a post office, this server, which we’ll imagine is configured with a round-robin algorithm on HAProxy, was the receiver of our HTTP GET request. HAProxy took the request, pulled up the IP address of the next web server in its queue, and sent it off that way.

# STEP 5: FIREWALL

Firewalls are designed with modern security techniques that are used in a wide range of applications.

Firewalls filter network traffic within a private network. It analyses which traffic should be allowed or restricted based on a set of rules. It welcomes only incoming traffic that has been configured to accept. It distinguishes between good and malicious traffic and either allows or blocks specific data packets on pre-established security rules.

These rules are based on several aspects indicated by the packet data, like their source, destination, content, and so on. They block traffic coming from suspicious sources to prevent cyberattacks.

Firewalls are simple to install, they are relatively configured anywhere data is received, including load balancers and host servers just as illustrated in our first picture. In our example, our GET request has passed one firewall installed on the load balancer. it will pass through other installed NGINX servers distributed.

# STEP 6: HOST SERVER

The host server is a web stack consisting of multiple parts that are traditionally set up along the lines of what is termed the LAMP (for our case we will use NGINX as our web server) model. The LAMP model breaks down as follows:

*    Linux — is basically the operating system that the host server runs.
*    NGINX — the HTTP web server that servers our static contents. Apache web server is quite capable.
*    MySQL — the database server. Database software is normally a relational database.
*    Python — It is a high-level language supported by web servers that handle dynamic content.

Delivery of a web page works as follows:

*    A GET request is received by the web server. The web server pulls up the file configured at the given location (in our example, the HTML file configured at the root (/) of the machine).
*    If the file contains dynamic content, the application server is run (ie. the corresponding Python scripts are run). The result of these scripts is inserted into the web page.
*    If the dynamic content involves stored data, the Python scripts query from the database server (probably through Python libraries such as MySQLdb or SQLAlchemy).
*    The web server delivers the web page.

Our web infrastructure design is configured with three host servers, running an ubuntu Linux distribution. one each for an NGINX web server, Python app, and MySQL database server. This will be an active-active setup; in other words, all servers will be running and handling requests simultaneously (as opposed to an active-passive setup). The database container on the first host server will be the master, while the others will be replicants.

# MONITORING

Websites are touchy, and a smoothly running website requires constant surveillance and fine-tuning according to statistics such as the amount of traffic, the speed of request handling, and the status of servers. Such statistics are collected by monitoring software. in our case, we are using Sumo-logic a monitoring client which collects statistics by installing agents in corresponding host servers.

# STEP 7: PAGE RENDERING

Our web browser has finally received the web page we requested. After pulling up the HTML file configured at the root of www.google.com, the host server sent it back to the web browser in an HTTP response message.
