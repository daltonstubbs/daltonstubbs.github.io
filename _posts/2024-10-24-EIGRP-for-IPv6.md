---
layout: post
title: Configuring EIGRP for IPv6
gh-repo: daltonstubbs
gh-badge: [star, follow]
tags: [ipv6, eigrp]
comments: false
author: Dalton Stubbs
---

EIGRP (Enhanced Interior Gateway Routing Protocol) is a dynamic routing protocol that helps routers exchange information about connected networks and figure out the best paths for sending data. It quickly adapts to network changes, like when a router fails or a new one comes online, ensuring that traffic keeps flowing smoothly. Unlike static routing, which requires manual updates, EIGRP automates the process, making it ideal for large or frequently changing networks.

With EIGRP for IPv6, this same functionality is extended to IPv6 networks. It allows routers to communicate and learn about available IPv6 routes, automatically updating their routing tables as the network changes. This dynamic routing makes managing IPv6 networks easier, especially as the number of connected devices grows. By using EIGRP, IPv6 networks can quickly respond to changes, avoid downtime, and ensure that data always takes the fastest, most reliable path.

Another interesting feature of EIGRP is its named mode, which allows the protocol to run both IPv4 and IPv6 instances simultaneously on the same router. This means that a single router can handle multiple routing protocols without needing separate configurations for each version of IP. By using named mode, network administrators can manage both IPv4 and IPv6 networks more easily and efficiently. This flexibility is particularly useful as organizations transition to IPv6 while still maintaining their existing IPv4 infrastructure. Now let's dive into the configuration piece!

{: .box-success}
Note to Readers: This article assumes that the reader has a basic understanding of IPv6 and the fundamentals of EIGRP. While we will cover key concepts of both, a foundational knowledge of these topics will help in following the discussion more effectively.

By default, the forwarding of IPv6 packets is turned off on most Cisco platforms. To enable IPv6 packet forwarding, you must first enter the command **ipv6 unicast-routing** in global configuration mode. Only after you enable this feature can you proceed to configure and activate EIGRP for IPv6. Below is an example of attempting to configure classic EIGRP mode on a router that does not have IPv6 enabled, and then it is fixed:

~~~
R1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)#ipv6 router eigrp 1
**% IPv6 routing not enabled**
R1(config)#ipv6 unicast-routing 
R1(config)#ipv6 router eigrp 1
R1(config-rtr)#
~~~