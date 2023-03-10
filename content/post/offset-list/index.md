+++
author = "Dalton Stubbs"
title = "Beyond the Basics: Using Offset Lists to Fine-Tune Network Performance"
date = "2023-03-10"
description = "a detailed explanation of what offset lists are, how they work, and how they can be used to modify the metric of specific routes in order to influence the flow of traffic."
tags = [
    "eigrp",
    "routing",
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
image = ""
+++

## What is an Offset List?

An offset list in EIGRP (Enhanced Interior Gateway Routing Protocol) is a tool used to modify the metric (or cost) of specific routes in order to influence how traffic is directed through the network. Think of it like a secret code that changes the directions on a map to get to a destination faster or slower. EIGRP uses a metric to determine the best path for traffic to flow through the network. The metric is based on factors such as bandwidth, delay, reliability, and load.

With an offset list, a network administrator can add or subtract a fixed value from the metric of certain routes, which can change the cost of those routes and thus influence how traffic flows. This can be useful in situations where the administrator wants to prioritize certain types of traffic or avoid congested links in the network. For example, if there are two paths to a destination, and one is faster but more expensive in terms of cost, the network administrator can use an offset list to decrease the cost of the faster path, making it more attractive for traffic to use.

## An Example Use Case for Offset Lists.

Imagine a scenario where a network has two links to the internet, one with a faster bandwidth but a longer delay, and another with a slower bandwidth but a shorter delay. By default, EIGRP may select the faster link for all traffic, causing congestion and slower response times. However, a network administrator can use an EIGRP offset list to increase the metric of the faster link, making it less attractive for routing traffic. This will encourage EIGRP to balance the traffic load across both links, providing better performance and reliability for end-users.

In this example, the EIGRP offset list is used to influence the metric of the faster link to make it less desirable. The offset list adds a fixed value to the metric of that link, effectively increasing its cost. This can be achieved by configuring an offset-list command with a specific value for the outgoing interface of the faster link. By using EIGRP offset lists to balance traffic across multiple paths, network administrators can improve network performance, reduce congestion, and provide better user experiences.

## Do You Have to Tie Offset Lists to Access Control Lists?

No, EIGRP offset lists do not have to be tied to an access control list (ACL). While it is common to use an ACL to specify the routes that the offset list should apply to, it is not mandatory. The offset list can also be applied to a specific interface or a range of interfaces, or even to all interfaces. 

When the offset list is applied to an interface or a range of interfaces, it will affect all routes that pass through those interfaces. However, it is important to note that this approach can have unintended consequences if the offset list affects other routes that were not intended to be modified. Using an ACL to apply the offset list provides greater control and specificity over which routes the offset list should apply to, and can help avoid unintended consequences. It is recommended to use an ACL whenever possible to ensure that the offset list only affects the desired routes.

## Configuring Offset Lists on Cisco Routers.

Create an access list that identifies the routes that the offset list should apply to. For example, to apply the offset list to all routes except for those in the 10.1.1.0/24 subnet, you could use the following access list:

	`access-list 10 permit any`
	`access-list 10 deny 10.1.1.0 0.0.0.255`

Create the EIGRP offset list and specify the offset value that should be applied to the selected routes. For example, to increase the metric of selected routes by 5000, you could use the following command:

	`router eigrp 100`
	`offset-list 1 in 5000`

In this example, "1" is the number of the access list created in step 1, "in" indicates that the offset should be applied to routes received by the router, and "5000" is the value of the offset.

Apply the access list to the appropriate EIGRP interfaces. For example, to apply the access list to all EIGRP interfaces, you could use the following command:

	`router eigrp 100`
	`distribute-list 10 in`

In this example, "10" is the number of the access list created in step 1, and "in" indicates that the access list should be applied to inbound traffic.

It's important to note that the specific configuration steps may vary depending on your network setup and requirements. Additionally, it's recommended to test any changes to your network configuration in a lab environment before applying them to a production network.

