---
layout: default
title: How to generate a buy and sell list based on client values
parent: Guides
nav_order: 11
---

# How to generate a buy and sell list based on client values

[API Docs](https://www.yourstake.org/api/docs/#tag/Screening)

This guide shows how to generate a buy and sell list of securities based on your client's values.

The information is very useful when rebalancing portfolios basedon client values alignment.

## Things you'll need

- [API Access Token]({{ site.baseurl }}{% link docs/guides/how-to-request-api-access.md %})

**Generating the buy and sell list is done in three steps.**

**1 -** Client selects their values

A client completes a values quiestionnaire.

[Guide to complete a questionnaire through the API]({{ site.baseurl }}{% link docs/guides/how-to-integrate-questionnaires-to-define-a-clients-esg-profile.md %}).

<img src="{{ site.baseurl }}/assets/images/sample-questionnaire.png" width="75%" height="75%">

**2 -** An universe is selected

{% include important.html title="What is an universe?" body="An universe refers to the group of indentifiers (companies/stocks) in a fund or portfolio." %}

Your universe may be one of two:

- A fund

When working with funds, please refer to their [API Docs page](https://www.yourstake.org/api/docs/#operation/v1_screening_fund_retrieve)


- A portfolio

When working with portfolios, please refer to their [API Docs page](https://www.yourstake.org/api/docs/#operation/v1_screening_portfolio_retrieve)


**3 -** Generate the list

Let's say our universe is one of our portfolios. That means we ae going to be using the following [API endpoint](https://www.yourstake.org/api/docs/#operation/v1_screening_portfolio_retrieve).

Grab your API Access Token and put it here:

```
-H "Authentication: Token YourTokenGoesHere" 
```

Now paste both into the curl command below:

```
curl -H "Your authentication header here" https://www.yourstake.org/api/v1/screening/portfolio/{portfolio_id}/
```

Here is a complete example:

```
curl -H "Authorization: Token YourTokenHere1234567890" "https://www.yourstake.org/api/v1/screening/portfolio/modelportfolio_A3rNbYtpEw2H52eXBpAEeL/?screen_sets=1,3,4"
```

Just replace the value of the token with yours and replace the screen sets values with the results from the questionnaire.

To run the curl command open a terminal and paste the command above.
The JSON response from the API should be similar to:

```
{
	"results": [
		{
			"company_id": 6212,
			"company_name": "Apple Inc.",
			"primary_ticker": "AAPL",
			"impact_factors": {
				"98": {
					"percentile": 0.84426695,
					"publication_date": "2021-03-31",
					"exclusion": false,
					"inclusion": false
				},
				"6": {
					"percentile": 1.0,
					"publication_date": "2019-06-30",
					"exclusion": false,
					"inclusion": false
				},
				"40": {
					"percentile": 1.0,
					"publication_date": "2021-07-21",
					"exclusion": false,
					"inclusion": true
				},
				"74": {
					"percentile": 1.0,
					"publication_date": "2019-10-30",
					"exclusion": false,
					"inclusion": false
				},
				"59": {
					"percentile": 1.0,
					"publication_date": "2019-10-30",
					"exclusion": false,
					"inclusion": false
				}
			}
		}
	]
}
```

The response will tell you if you should include or exclude each security in your buy/sell list based on the values alignment. The fiels `exclusion` and `inclusion` provide a clear signal. See [here](https://www.yourstake.org/api/docs/#operation/v1_screening_portfolio_retrieve).

