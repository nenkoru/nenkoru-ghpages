---
title: "Introduction into OpenZiti and Zero Trust Networks"
date: 2024-12-17
---
**DISCLAIMER: No marketing pun intended upon "Zero Trust" term, it's explained further!**

This is the first article in a series dedicated to exploring a complex yet powerful project designed to address the security challenges posed by current approaches to enterprise private networking. 

This article is for engineers out there who may found themselves in a situation where conventional VPN solutions and their security model does not fulfill demands and want to explore other possibilities.

Been exploring the topic for just under a year, hence my non-professional grasp of Zero Trust. But I am confident in my ability to share my perspective and draw attention to this well-crafted solution.  

I want the project to thrive and gain attention to make it be an option when deploying networks.
### The project that I want to share with you is called *OpenZiti*.  
Hop onto the main page, and start your journey right away: <https://openziti.io>  

## "Zero Trust"?

Let's first define "Zero Trust." 

In simple terms, this is a security model specifying that no principal should have an implicit trust by default to the other principal. 
This requires continuous verification of identities and explicit grant of access to each resource they attempt to access. 
Having access to the corporate network's inner perimeter should not be granting trust by default. On the contrary, it should be default denying the access.


### A foundational aspect of the Zero Trust principle is the concept of Least Privilege.
#### TODO:


### The second thing is: Default Deny
#### TODO: 

---
Numerous excellent discussions exist concerning simplification and demystification of the term.

From Clint of OpenZiti: <https://www.youtube.com/live/ctdyAzvByR8?si=0rFBV8fL6eNPQGZl&t=160>  
From IBM: <https://www.youtube.com/watch?v=yn6CPQ9RioA>  
And CISO: <https://www.youtube.com/watch?v=DLQAbJm4gFM>  


## OpenZiti's Zero-Trust
The name ‘Open’ reflects its open-source nature, much like successful projects such as OpenTelemetry, OpenSSL, and OpenCV. ‘Zero Trust’ is the origin of the term ‘Ziti,’ showing that zero trust forms the core of this solution. 
The project is under an Apache 2.0 License, thus granting considerable freedom regarding usage. 

Once the principle of Zero Trust is defined, OpenZiti’s offerings become easier to grasp. This includes every piece needed for a network built on Zero Trust Networking principles. 
Whether it's through application-embedded solutions referred to as Zero Trust Application Access. 
Zero Trust Host Access where an encryption and trust ends on the hosts. 
Zero Trust Network Access where an encryption stops at the "routers" and bytes are being sent to the respective hosts over the underlay network. 

![alice-edge-dial-svg](https://raw.githubusercontent.com/nenkoru/nenkoru-ghpages/refs/heads/main/_images/2024-12-17-openziti-intro/simplified-dial-alice.svg)
### Underlay vs Overlay

The question might arise: how to implement Zero Trust over existing network infrastructures? 
You need to have the network be programmable, I’d call it “bendable”. 

To achieve this, you must be able to control network behavior by simplifying the fundamental concepts of the underlying TCP/IP network. 
And build on top of it an "overlay" network which would allow for logical addressing of the endpoints. A strong example is XMPP’s “username@example.com” format.
The same does OpenZiti. It creates an abstraction, a logical layer between an identity that wants to send bytes to the other identity.

So underlay means our usual TCP/IP network and OpenZiti being an overlay. 

## OpenZiti overlay network features

### High Availability
The network’s high availability results from its design, and the system calculates costs across the fabric from the source to the destination through every possible path. 
The overlay routes according to the lowest cost regardless of the underlay - circumventing standard BGP, as well as providing higher uptime and reliability. 

It means that you might deploy multiple routers closer to the edge where your users operate, making the network more responsive to the end-users and more optimized for your multi-datacenter workloads. 

![simplified-cost-calc-svg](https://raw.githubusercontent.com/nenkoru/nenkoru-ghpages/refs/heads/main/_images/2024-12-17-openziti-intro/simplified-cost-calc.svg)

### No Port Inference
# TODO: 

### End-to-End Encryption
# TODO: 

### Continuous Identity Verification (authorization)

To ensure a Zero Trust network functions, you must verify the claimed user identity. In OpenZiti it's done by posture checks, which allow for checking a wide range of things before an identity could make any dial requests and enter the network.

For example:
- Has identity passed an MFA?
- Is identity running a certain version of the operating system?
- Is identity within some Windows Domain?
- Has identity got a certain process running?

Posture checks are performed on the edge devices (e.g laptops) and are constantly sent as a telemetry to the controller which at the end determines whether an identity could dial a service.

With this approach, you could eliminate the possibility of identity theft by a bad actor and ensure the network level security.


---
You can find more features here: <https://openziti.io/docs/learn/introduction/features/#zero-trust>  
As well as a great talk about this here: <https://www.youtube.com/watch?v=l5ktiI-j3eg>  
And a setup of self-hosted BrowZer here: <https://www.youtube.com/watch?v=98cGSnEBzOE>  


## Conventional solutions(VPNs, firewalls)
VPNs and firewalls provided a perimeter-based defense model. VPNs create secure, encrypted tunnels for data transmission across public networks, extending a private network over the internet. 
Firewalls act as gatekeepers, filtering incoming and outgoing traffic based on predefined security rules. 
People designed these technologies for an era with more clearly defined corporate network boundaries, focused on keeping external threats out.  
However, the traditional perimeter model struggles in an environment characterized by cloud computing, remote work, and increased mobile device usage. The once-clear boundary between internal and external networks has blurred, rendering perimeter defenses less effective. 
VPNs can introduce latency and bottlenecks, while firewalls may not address threats that originate within the network or bypass perimeter defenses altogether. 


## Conclusion
I believe OpenZiti represents a significant step forward in implementing Zero Trust principles by offering a comprehensive suite of features designed to secure network communications in a modern enterprise environment. 
As I continue to explore its capabilities in subsequent articles, we will delve deeper into its architecture, use cases, and how it stands as a robust alternative to conventional networking solutions. 
Stay tuned for more insights into how OpenZiti can transform your approach to network security.
