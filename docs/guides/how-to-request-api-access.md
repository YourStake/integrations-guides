---
layout: default
title: How to request API access
parent: Guides
nav_order: 1
---

# How to request API access

[Request sandbox access](https://www.yourstake.org/info/api)

API access is oriented around a specific user account. YourStake account holders and API sandbox users can access the API with a `bearer token` with access restricted to their user account. If you're an existing YourStake client please [contact us for API access](https://www.yourstake.org/info/api).

If tokens have been provisioned for your account you can find them [here](https://www.yourstake.org/api/auth/). 

To authenticate via Bearer Token simply pass it in the authorization header:

`Authorization: Token exampleTokenRightHere0123456789`



We also support delegated access to user accounts via OAuth, if you're interested in building an application that tightly integrates access to YourStake please [contact us here](https://www.yourstake.org/info/api).