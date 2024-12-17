---
title: "Introduction into OpenZiti and Zero Trust Networks"
date: 2024-12-17
---
This is the first article in a series dedicated to exploring a complex yet powerful project designed to address the security challenges posed by current approaches to enterprise private networking. 

My intended audience includes network security specialists, DevSecOps professionals, and network administrators who may be familiar with the concept of zero trust but are seeking effective implementations. 

I have been exploring the topic for just under a year, hence my non-professional grasp of Zero Trust. I am confident in my ability to share my perspective and draw attention to this well-crafted solution. The project that I want to share with you is called OpenZiti.

The name ‘Open’ reflects its open-source nature, much like successful projects such as OpenTelemetry, OpenSSL, and OpenCV. ‘Zero Trust’ is the origin of the term ‘Ziti,’ showing that zero trust forms the core of this solution. The project is under an Apache 2.0 License, thus granting considerable freedom regarding usage. 

## "Zero Trust"?

Let's first define "Zero Trust." 

In simple terms, this is a security model specifying that no device or user should trust, even on a particular network. 
This requires continuous verification of identities and explicit granting of access to each resource they attempt to access. 
Having access to the corporate network's inner perimeter does not grant trust. 


### A foundational aspect of the Zero Trust principle is the concept of Least Privilege.
With questions to be answered: 
- Is an identity able to dial the service?
- Is an identity able to host the service?
- Can the router end the encryption and transmit the bytes to the service?

Least Privilege boils down to allowing an identity only what is vital to perform its functions.


### The second thing is: Strong Identity Verification 
You must confirm a principal’s asserted identity when accessing the service. Although it’s possible cryptographically in multiple ways, OpenZiti’s PKI handles it.


### The third key principle is: Mutual Authentication.
I mean, at some point, you would still need to trust something. 

But not thoughtlessly, just because the service is accessible and you have the ability to send requests to it, but because you check that the trusted authority authenticated the identity it displays. 

The service operates in the opposite direction as well. It needs verification of the caller’s identity. 

Numerous excellent discussions exist concerning simplification and demystification of the term.

From Clint of OpenZiti: <https://www.youtube.com/live/ctdyAzvByR8?si=0rFBV8fL6eNPQGZl&t=160>

From IBM: <https://www.youtube.com/watch?v=yn6CPQ9RioA&pp=ygUSd2hhdCBpcyB6ZXJvIHRydXN0>

And CISCO: <https://www.youtube.com/watch?v=DLQAbJm4gFM&pp=ygUSd2hhdCBpcyB6ZXJvIHRydXN0>


## OpenZiti's Zero-Trust
Once the principle is defined, OpenZiti’s offerings become easier to grasp. This includes every piece needed for a network built on Zero Trust Networking principles. 
Whether it's through application-embedded solutions referred to as Zero Trust Application Access. 
Zero Trust Host Access where an encryption and trust ends on the hosts. 
Zero Trust Network Access where an encryption stops at the "routers" and bytes are being sent to the respective hosts over the underlay network. 

![alice-edge-dial-svg](https://raw.githubusercontent.com/nenkoru/nenkoru-ghpages/refs/heads/main/_images/2024-12-17-openziti-intro/simplified-dial-alice.svg)
#### Woah, hold on for a second.

What is underlay network in this context means?

The question might arise how to implement Zero Trust over existing network infrastructures. 
You need to have the network be programmable, I’d call it “bendable”. 

To achieve this, you must be able to control network behavior by simplifying the fundamental concepts of the underlying TCP/IP network. 
And build on top of it an "overlay" network which would allow for logical addressing of the endpoints. A strong example is XMPP’s “username@example.com” format. 
The same does OpenZiti. It creates an abstraction, a logical layer between an identity that wants to send bytes to the other identity (service in most of the cases).

So underlay means our usual TCP/IP network and OpenZiti being an overlay. 

## OpenZiti overlay network (fabric) features

### High-Availability
The network’s high availability results from its design, and the system calculates costs across the fabric from the source to the destination through every possible path. 
The overlay routes according to the lowest cost regardless of the underlay - circumventing standard BGP, as well as providing higher uptime and reliability. 

It means that you might deploy multiple routers closer to the edge where your users operate, making the network more responsive to the end-users and more optimized for your multi-datacenter workloads. 

![simplified-cost-calc-svg](https://raw.githubusercontent.com/nenkoru/nenkoru-ghpages/refs/heads/main/_images/2024-12-17-openziti-intro/simplified-cost-calc.svg)
### Continuous Identity Verification (authorization)

To ensure a Zero Trust network functions, you must verify the claimed user identity. In OpenZiti it's done by posture checks, which allow for checking a wide range of things before an identity could make any dial requests and enter the network.

For example:
- Has identity (user) passed an MFA with
- Is identity running a certain version of the operating system
- Is identity within some Windows Domain
- Has identity got a certain process running

Posture checks are performed on the edge devices (e.g laptops) and are constantly sent as a telemetry to the controller which at the end determines whether an identity could dial a service.

With this approach, you could eliminate the possibility of identity theft by a bad actor and ensure the network level security.


### BrowZer
Do you want to allow users to access some users outside of the domain to access some platform, but don't want them to get into the network and don't want to expose the service to the public internet? 
BrowZer could potentially address this issue by allowing users to simply complete the OIDC challenge and connect to the service through OpenZiti routers in the browser. 

![simplified-browzer-oidc-flow-svg](https://raw.githubusercontent.com/nenkoru/nenkoru-ghpages/refs/heads/main/_images/2024-12-17-openziti-intro/simplified-browzer-oidc.svg)
---
These features are just the ones that I think are worth noting in the first article, more and in-depth coming later. This here is just to bind Zero Trust and OpenZiti together for the following threads. 

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
