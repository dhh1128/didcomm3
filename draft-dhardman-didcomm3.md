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
  DID:
    target: https://www.w3.org/TR/did-core/
    title: "Decentralized Identifiers (DIDs) v1.0: Core architecture, data model, and representations"

informative:

  RFC9039:
    title: Uniform Resource Names for Device Identifiers
    target: https://www.rfc-editor.org/rfc/rfc9039.html

  DIDComm1:
    target: https://github.com/hyperledger/aries-rfcs/blob/main/concepts/0005-didcomm/README.md
    title: "Aries RFC 0005: DID Communication"

  DIDComm2:
    target: https://identity.foundation/didcomm-messaging/spec/
    title: DIDComm Messaging

  ToIPArch:
    target: https://github.com/trustoverip/TechArch/blob/main/spec.md
    title: Trust over IP (ToIP) Technology Architecture Specification

  KERI:
    target: https://arxiv.org/abs/1907.02143
    title: Key Event Receipt Infrastructure (KERI)
    author:
      ins: S. Smith
      name: Samuel M. Smith
      org: ProSapien LLC
      date: 2021

  JSON:
    target: https://www.json.org/json-en.html
    title: JavaScript Object Notation Delimiters

  RFC4627:
    target: https://datatracker.ietf.org/doc/rfc4627/
    title: The application/json Media Type for JavaScript Object Notation (JSON)

  CBOR:
    target: https://en.wikipedia.org/wiki/CBOR
    title: CBOR Mapping Object Codes

  RFC8949: CBOR

  MGPK:
    target: https://github.com/msgpack/msgpack/blob/master/spec.md
    title: Msgpack Mapping Object Codes

  NaCL:
    target: https://nacl.cr.yp.to
    title: NaCl Networking and Cryptography library

  IPFS:
    target: https://richardschneider.github.io/net-ipfs-core/api/Ipfs.Registry.HashingAlgorithm.html
    title: IPFS MultiFormats

  Base58Check:
    target: https://en.bitcoin.it/wiki/Base58Check_encoding
    title: Base58Check Encoding

--- abstract

Decentralized Identifier Communication (DIDComm) lets two or more peers securely conduct cryptographically robust, message-based interactions in a highly decentralized fashion. Strong privacy guarantees are achievable. Messages can build threads and rich, application-level protocols. Unlike many secure chat technologies, no servers, APIs, web hooks, API keys, or similar client-server constructs are required. Offline is a first-class mode. Messages can flow over any transport or combination of transports, and security is portable to arbitrary contexts, including ones that do not understand DIDComm.

--- middle

# Introduction

## Problem Domain
Decentralized Identifier Communication ("DIDComm") specifies how peer groups can leverage the cryptographic properties of DIDs and similar identifiers to securely exchange messages. Such exchanges can use any combination of transports -- HTTP, WebSockets, SSE, email, Bluetooth, NFC, LoRa, QR codes, message queues, radio broadcast, sneakernet, the file system...

Of course, robust mechanisms for secure communication already exist. However, most rely on key registries, identity providers, certificate authorities, browser or app vendors, or similar centralizations. Many also assume a single transport, making it difficult to use the same solution for both human and machine conversations, online and offline, simplex and duplex, across a broad set of modalities. And most existing options are siloed -- messages must flow within the ecosystem provided by a single vendor or community, or else the security context is reset. You can't start a conversation on secure chat, and continue it on email or a VOIP call, without reauthenticating (often based on a different method and different secrets).

DIDComm fixes this.

Some secure communications technologies deliberately treat higher-level constructs as out of scope. TLS is an example: having guaranteed the cryptographic integrity of a session, its mandate ends with the movement of arbitrary bytes. This is wonderfully general-purpose, but it means that every higher-level protocol has to re-invent login, timeouts, error handling, and so forth.

Other secure communication technologies are tightly bound to a specific set of higher-level behaviors. Signal's protocol may be capable of flexible use, but in practice it is only applied to the problems of VOIP and unstructured messaging. Making payments, booking a vacation, or applying for a loan don't fit in an obvious way atop the Signal foundation, unless done by humans on a phone call or a chat client.

DIDComm fixes this, too.

DIDComm's posture on higher-level constructs is the best of both worlds. It moves messages, not arbitrary bytes, and it specifies how messages are encapsulated in envelopes, how they are typed and versioned, how they are associated with threads and protocol instances, how timeouts and ACKs work, and how errors can be raised and recognized. But message content can match any schema a developer imagines. This lets developers build arbitrary higher-level protocols atop DIDComm, but frees them to focus on just the unique problem domain of those protocols. It also unlocks powerful composability. Any number of DIDComm protocols can run at a single endpoint. Each has an independent state; each is discoverable; each can be connected to others in flexible ways. Because the security and privacy features are part of a common foundation, rich workflows can combine them without creating seams for an attacker to exploit. And such workflows can easily and safely cross back and forth between the previously siloed worlds of humans and automation.

The unintended consequence of existing secure communications technologies is to perpetuate an asymmetry between institutions and ordinary people. The former maintain certificates and always-connected servers, and publish APIs under terms and conditions they dictate; the latter suffer with usernames and passwords, poor interoperability, and a Hobson’s choice between privacy and convenience. But with DIDComm, there is no distinction between clients and servers. Individuals on semi-connected mobile devices become full peers of highly available web servers operated by IT experts. Registration is self-service, intermediaries require little trust, and terms and conditions can come from any party. And all of this is portable to whatever tools and transports happen to be convenient.

## Related Technologies

This document embodies the third generation of DIDComm, and may thus be described as "DIDComm v3" if it is helpful to disambiguate. It is substantially similar to its predecessors {{DIDComm1}} and {{DIDComm2}} in intent and core concepts, but compatibility across versions is not an explicit goal of this document, and is explicitly out of scope here.

As used here, "decentralized identifier" matches the term in the identifier ontology from {{ToIPArch}}. It thus encompasses the definition in the W3C's DID spec {{DID}}, but also AIDs from {{KERI}} and potentially other decentralized identity schemes such as {{RFC9039}}.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

## Terms


# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

This version of DIDComm builds on {{DIDComm2}}, incubated at DIF, and {{DIDComm1}}, incubated at Hyperledger. Each of those efforts had many contributors. Thank you, everyone! Some portions of the explanatory text in this document is paraphrased or copied from those earlier specs (under their respective Apache 2 licenses).
