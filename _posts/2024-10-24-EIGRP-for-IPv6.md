---
layout: post
title: EIGRP for IPv6
gh-repo: daltonstubbs
gh-badge: [star, follow]
tags: [ipv6, eigrp]
comments: true
author: Dalton Stubbs
---

The Enhanced Interior Gateway Routing Protocol (EIGRP) is a distance-vector, classless routing protocol introduced by Cisco in 1992 with IOS version 9.21. It was developed as an upgrade to the older Interior Gateway Routing Protocol (IGRP) to support classless routing and allow more flexible subnetting. EIGRP also offers additional features that are not typically found in other distance-vector protocols, such as Routing Information Protocol (RIP) or IGRP. Around 2015, Cisco released the core functions of EIGRP to the Internet Engineering Task Force (IETF) through RFC 7868, enabling other vendors to implement it and ensuring compatibility between Cisco and non-Cisco routers. However, advanced features—like EIGRP stub routing, which is essential for Dynamic Multipoint Virtual Private Networks (DMVPN)—were not included in this release. Since RFC 7868 is only informational, Cisco continues to oversee the development and updates of EIGRP.

EIGRP for IPv6 functions much like its IPv4 counterpart but is designed to manage IPv6 prefixes. EIGRP for IPv4 runs over the IPv4 network layer, communicates with other IPv4 neighbors, and advertises only IPv4 routes. Similarly, EIGRP for IPv6 uses the IPv6 network layer, connects with other IPv6-speaking neighbors, and shares IPv6 routes. The overall behavior and functionality remain nearly the same, with the key difference being the type of addresses they handle.

{: .box-success}
Note to Readers: This article assumes that the reader has a basic understanding of IPv6 and the fundamentals of EIGRP. While we will cover key concepts of both, a foundational knowledge of these topics will help in following the discussion more effectively.

