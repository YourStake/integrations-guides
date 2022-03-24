---
layout: default
title: How to create a portfolio
parent: Guides
nav_order: 2
---

# How to create a portfolio


portfolio's contain a client's holding in our system. They are the building block for many of our products.

[API Docs link](https://www.yourstake.org/api/docs/#operation/Create%20a%20Portfolio)

Things you need:

- [API Access Token]({{ site.baseurl }}{% link docs/guides/how-to-request-api-access.md %})
- A list of the portfolio holdings with their respective tickers or ISINs

### Let's create a portfolio using curl.

First, define the request payload.

```
{
  "total_value": 1000000,
  "name": "My first test portfolio",
  "holdings": [
    {
      "identifier_type": "ticker",
      "identifier": "AAPL",
      "percentage": 0.5
    },
    {
      "identifier_type": "ticker",
      "identifier": "SPY",
      "percentage": 0.5
    }
  ]
}
```

Grab your API Access Token and put it here:

```
-H "Authorization: Token YourTokenGoesHere" 
```

Now paste both into the curl command below:

```
curl -d 'Your Payload Here' -H "Authorization: Token YourTokenGoesHere"  -H "Content-Type: application/json" -X POST https://yourstake.org/api/v1/portfolios/
```

Here is a complete example:

```
curl -d '{"total_value": 1000000,"name":"My first test portfolio","holdings":[{"identifier_type":"isin","identifier":"US0378331005","percentage":0.5},{"identifier_type":"isin","identifier":"US78462F1030","percentage":0.5}]}' -H "Authorization: Token YourTokenHere1234567890" -H "Content-Type: application/json" -X POST https://yourstake.org/api/v1/portfolios/
```

Just replace the value of the token with yours.

To run the curl command open a terminal and paste the command above.
The JSON response from the API should be similar to:

```
{
    "id":"modelportfolio_A3rNbYtpEw2H52eXBpAEeL",
    "holdings_received":2,
    "holdings_matched":2,
    "unmatched_holdings":[],
    "screen_sets":[],
    "name":"My first test portfolio"
}
```

Make sure to save the `id` to use it for the following guides.


