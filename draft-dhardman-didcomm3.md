---
title: "DIDComm3"
category: info

docname: draft-dhardman-didcomm3-latest
submissiontype: IETF  # also: "independent", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
# area: AREA
# workgroup: WG Working Group
keyword:
 - decentralization
 - ssi
 - self-sovereign identity
 - mesh networking
 - web3
 - web5
venue:
#  group: WG
#  type: Working Group
#  mail: WG@example.com
#  arch: https://example.com/WG
  github: "dhh1128/didcomm3"
  latest: "https://dhh1128.github.io/didcomm3/draft-dhardman-didcomm3.html"

author:
 -
    fullname: Daniel Hardman
    organization: Provenant, Inc
    email: "daniel.hardman@gmail.com"

normative:

informative:


--- abstract

DIDComm3 lets two or more peers securely exchange messages in a highly decentralized fashion. Strong privacy guarantees are achievable. Messages can build threads and rich, application-level protocols. Unlike many secure chat technologies, no servers, APIs, web hooks, API keys, or similar client-server constructs are required. Offline is a first-class mode. Messages can flow over any transport or combination of transports, and security is portable to arbitrary contexts.

--- middle

# Introduction

DIDComm3 (hereafter, just "DIDComm") specifies how peer groups can leverage the cryptographic properties of DIDs and similar identifiers to securely exchange messages. Such exchanges can use any combination of transports -- HTTP, WebSockets, SSE, email, Bluetooth, NFC, LoRa, QR codes, message queues, radio broadcast, sneakernet, the file system...

Of course, robust mechanisms for secure communication already exist. However, most rely on key registries, identity providers, certificate authorities, browser or app vendors, or similar centralizations. Many also assume a single transport, making it difficult to use the same solution for human and machine conversations, online and offline, simplex and duplex, across a broad set of modalities. And most existing options are siloed -- messages must flow within the ecosystem provided by a single vendor or community, or else the security context is reset. You can't start a conversation on secure chat, and continue it on email or a VOIP call, without reauthenticating (often based on a different method and different secrets).

DIDComm fixes this.

Some secure communications technologies deliberately treat higher-level constructs as out of scope. TLS is an example: having guaranteed the cryptographic integrity of a session, its mandate ends with the movement of arbitrary bytes. This is wonderfully general-purpose, but it means that every higher-level protocol has to re-invent login, timeouts, error handling, and so forth.

Other secure communication technologies are tightly bound to a specific set of higher-level behaviors. Signal's protocol may be capable of flexible use, but in practice it is only applied to the problems of VOIP and unstructured messaging. Making payments, booking a vacation, or applying for a loan don't fit atop the Signal foundation, unless done by humans on a phone call or a chat client.

DIDComm fixes this, too.

DIDComm's posture on higher-level constructs is the best of both worlds. It moves messages, not arbitrary bytes, and it specifies how messages are encapsulated in envelopes, how they are typed and versioned, how they are associated with threads and protocol instances, how timeouts and ACKs work, and how errors can be raised and recognized. But message content can match any schema a developer imagines. This lets developers build arbitrary higher-level protocols atop DIDComm, but frees them to focus on just the unique problem domain of those protocols. It also unlocks powerful composability. Any number of DIDComm protocols can run at a single endpoint. Each has an independent state; each is discoverable; each can be connected to others in flexible ways. Because the security and privacy features are part of a common foundation, rich workflows can combine them without creating seams an attacker can exploit. And such workflows can easily and safely cross back and forth between the previously siloed worlds of humans and automation.

The unintended consequence of existing secure communications technologies is to perpetuate an asymmetry between institutions and ordinary people. The former maintain certificates and always-connected servers, and publish APIs under terms and conditions they dictate; the latter suffer with usernames and passwords, poor interoperability, and a Hobson’s choice between privacy and convenience. But with DIDComm, individuals on semi-connected mobile devices become full peers of highly available web servers operated by IT experts. Registration is self-service, intermediaries require little trust, and terms and conditions can come from any party.

# Conventions and Definitions

{::boilerplate bcp14-tagged}


# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
