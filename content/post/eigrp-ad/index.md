+++
author = "Dalton Stubbs"
title = "EIGRP Administrative Distances"
date = "2023-03-12"
description = "Understanding the Metrics for Reliable Network Routing"
tags = [
    "eigrp",
]
categories = [
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
image = ""
+++

## What Are EIGRP Administrative Distances?

In Cisco's Enhanced Interior Gateway Routing Protocol (EIGRP), administrative distance (AD) is a metric used to determine the reliability and trustworthiness of a particular route or path. It is used to select the best path among multiple possible paths to a destination network. Administrative distance values are assigned to each type of routing protocol or route source. When EIGRP receives multiple routes to the same destination network from different sources, it selects the route with the lowest administrative distance as the best path.

Here are the default administrative distance values for EIGRP:

    Connected interface: 0
    EIGRP summary route: 5
    Internal EIGRP route: 90
    External EIGRP route: 170

It is important to note that these administrative distances are LOCAL to the router, and are not shared or influenced by another router's information. Even though there is a connection between two router's and they are under the same EIGRP AS number, they do not influence each others EIGRP Administrative Distance.

A connected interface has an AD of 0 because it is directly connected to the router and is considered the most reliable and trustworthy path.

EIGRP summary routes are routes that are manually configured by the network administrator and are used to summarize multiple subnets into a single route. They have an AD of 5, indicating that they are less reliable than connected interfaces but more reliable than internal EIGRP routes.

Internal EIGRP routes are routes that are learned from other EIGRP routers within the same autonomous system (AS). They have an AD of 90, indicating that they are less reliable than connected interfaces and EIGRP summary routes but more reliable than external EIGRP routes.

External EIGRP routes are routes that are learned from routers outside the AS, such as routes from other routing protocols or from the Internet. They have an AD of 170, indicating that they are the least reliable and trustworthy paths. External EIGRP routes are those that are learned from other protocols, such as OSPF and RIP. This is done by a local router using redistribrution lists and pushing that information out. Since the router is participating in EIGRP, if it is connected to other routers via OSPF or RIP, it can pass that information in it's EIGRP packets and allow all other neighbors to hit those routes through it. Think of it as forming a bride between a local EIGRP family and another family of routing protocols.

It's important to note that these default administrative distance values can be changed by the network administrator, and different values may be more appropriate for different network topologies and environments.

## How to View Your Administrative Distances.

To view the EIGRP administrative distances configured on a Cisco router, you can use the `show ip protocols` command. This command displays the current status of all routing protocols running on the router, including EIGRP.

In the output of the show ip protocols command, you should see a section labeled `EIGRP-IPv4 Protocol Information` that displays the administrative distances for connected, summary, internal, and external routes. Here's an example of what the output might look like:

```Router# show ip protocols

***Output omitted for brevity***

Routing Protocol is "eigrp 1"
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Default networks flagged in outgoing updates
  Default networks accepted from incoming updates
  EIGRP-IPv4 Protocol for AS(1)
    Metric weight K1=1, K2=0, K3=1, K4=0, K5=0
    Metric weight K6=0, K7=0, K8=0, K9=0, K10=0
    Maximum hopcount 100
    Maximum metric variance 1
    Automatic summarization is in effect
    Automatic network summarization:
      10.0.0.0/8 for FastEthernet0/0
    Routing for Networks:
      10.0.0.0
    Routing Information Sources:
      Gateway         Distance      Last Update
      192.168.1.1          90      00:00:05
    Distance: internal 90 external 170
```

In this example, the administrative distance for internal routes is 90 and the administrative distance for external routes is 170.

A cleaner way to look at this would be a simple `show ip route eigrp` command. This would output something like this:

```Router# show ip route eigrp

     10.0.0.0/8 is variably subnetted, 3 subnets, 2 masks
D        10.1.1.0/24 [90/2297856] via 192.168.1.1, 00:00:19, FastEthernet0/0
D        10.2.2.0/24 [90/2297856] via 192.168.2.1, 00:00:19, FastEthernet1/0
D        10.3.3.0/24 [90/2297856] via 192.168.3.1, 00:00:19, FastEthernet2/0
     172.16.0.0/16 is variably subnetted, 2 subnets, 2 masks
D        172.16.10.0/24 [90/2297856] via 192.168.1.1, 00:00:19, FastEthernet0/0
D EX     172.16.20.0/23 [170/3072] via 192.168.2.1, 00:00:19, FastEthernet1/0
```

In this example output, there are three EIGRP-learned internal routes and one EIGRP-learned external route. The D in the left column indicates that the routes were learned from EIGRP, and the EX for the last route indicates that it is an external route.

