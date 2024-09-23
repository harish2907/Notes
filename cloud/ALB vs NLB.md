The components
The components are the same for both the ALB and the NLB. The following figure illustrates the components.
    • The load balancer acts as the entry point into your system.
    • The listener listens for incoming connections
    • The load balancer forwards requests to a target group.
    • The target group consists of one or multiple targets.
    • A target might be an EC2 instance, container, or internal service.
    • The health check monitors the targets.


    ALB	NLB
Protocols	HTTP/1, HTTP/2, gRPC	TCP, UDP
Performance	Low Latency	Very Low Latency
Traffic Spikes	⚠️ Inform AWS Support about huge traffic spikes	✅ Deals with huge and unexpected traffic spikes
Static IP Addresses	❌ No. However, you could place an NLB in front of an ALB.	✅ Yes
TLS Termination	✅ Yes	✅ Yes
Targets	EC2 Instance, IP Address, Lambda	EC2 Instance, IP Address, ALB
Client IP preservation	Use HTTP header X-Forwarded-For	Optional, but comes with limitations
Routing Algorithm	Round Robin or Least Outstanding Requests	Random
Deregistering targets	ALB stops sending requests and waits for open requests	NLB stops opening new connections, but the application needs to terminate connections properly
Multiplexing	✅ Yes, reuses connections to targets	❌ No, does not reuse connections to targets
Maximum number of targets	1000-5000	500-1000
Security Group	Security group of ALB controls inbound traffic, targets reachable from ALB only	Security group of targets control inbound traffic, targets reachable from clients
Request based routing	✅ Yes, based on hostname, path, header, …	❌ No
WAF	✅ Yes	❌ No
Authentication	✅ Yes (OpenID Connect, SAML, …)	❌ No
Slow Start Mode	✅ Yes	❌ No
Sticky Session	✅ Yes	❌ No
IPv6	✅ Yes	✅ Yes
Costs	💰💰💰	💰💰 (But causes more connections and therefore higher loa
        d on targets.)

From <https://blog.cloudcraft.co/alb-vs-nlb-which-aws-load-balancer-fits-your-needs/> 

Difference Table :  HTTP vs TCP
PARAMETER	TCP	HTTP
Acronym for	Transmission Control Protocol	Hypertext Transfer Protocol
OSI Layer	Transport Layer (Layer 4)	Application Layer (Layer 7)
Philosophy	TCP protocol is used for session establishment between two machine.	HTTP protocol is used for content access from web server.
TCP ports	No Port number	HTTP uses TCP’s port number 80.
Authentication	TCP-AO (TCP Authentication Option)	HTTP does not perform authentication.
Usage	TCP is used extensively by many internet applications.	HTTP is useful in transferring smaller files like web pages.
State	Connection-Oriented Protocol	Stateless but not session less
Type of Transfer	Establishes Connection between Client and Server.	Transfers records between the Web client and Web server.
URL	No URL	When you are managing HTTP, HTTP will appear in URL.
Communication	3-Way Handshake (SYN, SYN-ACK, ACK)	One-way communication system.
Use	HTTP, HTTPs, FTP, SMTP, Telnet	Most widely used for web based applications
Download speed	The speed for TCP is slower.	HTTP is faster than TCP.
        

From <https://networkinterview.com/http-vs-tcp-know-the-difference/> 


