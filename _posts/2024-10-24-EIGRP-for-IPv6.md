---
layout: post
title: EIGRP for IPv6
gh-repo: daltonstubbs
gh-badge: [star, follow]
tags: [ipv6, eigrp]
comments: true
author: Dalton Stubbs
---

Enhanced Interior Gateway Routing Protocol (EIGRP) is a distance-vector, classless routing protocol that Cisco introduced in 1992 with IOS version 9.21. As the name implies, it’s an improved version of Cisco’s older Interior Gateway Routing Protocol (IGRP). The main reason Cisco developed EIGRP was to make IGRP classless, meaning it could handle more flexible subnet masks. EIGRP also offers extra features not typically found in other distance-vector protocols like IGRP or Routing Information Protocol (RIP).

In 2016, Cisco shared the core features of EIGRP with the Internet Engineering Task Force (IETF) through RFC 7868, allowing other vendors to use EIGRP and make it compatible with Cisco and non-Cisco routers. However, some advanced features, such as EIGRP stub routing, which is important for Dynamic Multipoint Virtual Private Networks (DMVPN), were not included in the public release. Since RFC 7868 is for informational purposes only, Cisco still controls the development and updates of EIGRP.

EIGRP for IPv6 works very similar EIGRP for IPv4, but it handles IPv6 prefixes instead of IPv4 routes. EIGRP for IPv4 operates over an IPv4 network layer, communicates with other EIGRP IPv4 neighbors, and only shares IPv4 routes. In the same way, EIGRP for IPv6 uses IPv6 as its transport layer, talks to other EIGRP for IPv6 neighbors, and advertises IPv6 prefixes.

{: .box-success}
Note to Readers: This article assumes that the reader has a basic understanding of IPv6 and the fundamentals of EIGRP. While we will cover key concepts of both, a foundational knowledge of these topics will help in following the discussion more effectively.

