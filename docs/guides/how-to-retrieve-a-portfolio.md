---
layout: default
title: How to retrieve a portfolio
parent: Guides
---

# How to retrieve a portfolio

portfolio's contain a client's holding in our system. They are the building block for many of our products.

[API Docs Link](https://www.yourstake.org/api/docs/#operation/Portfolio%20detail)

Things you need:

- [API Access Token]({{ site.baseurl }}{% link docs/guides/how-to-request-api-access.md %}).
- The portfolio `id`. Should be similar to `modelportfolio_A3rNbYtpEw2H52eXBpAEeL`.

### Let's retrieve a portfolio using curl.

There's two options you may pass when retrieving portfolios.

- **Holdings**: Whether or not to include the portfolio holdings in the response. `holdings=true` or `holdings=false`
- **Values**: Comma separated list of [Screen Sets]({{ site.baseurl }}{% link docs/glossary.md %}/#screen-sets) ids, to produce alignment numbers in response. `values=1,2,3,4`

{% include important.html title="These options are not required" body="You do not need to pass these values. However, it's very common to use them when benchmarking." %}


Grab your API Access Token and put it here:

```
-H "Authentication: Token YourTokenGoesHere" 
```

Now paste both into the curl command below:

```
curl -H "Your authentication header here" https://yourstake.org/api/v1/portfolios/
```

Here is a complete example:

```
curl -H "Authorization: Token YourTokenHere1234567890" https://yourstake.org/api/v1/portfolios/modelportfolio_A3rNbYtpEw2H52eXBpAEeL/
```

Just replace the value of the token with yours.

To run the curl command open a terminal and paste the command above.
The JSON response from the API should be similar to:

```
{
    "portfolio":{
        "id":"modelportfolio_A3rNbYtpEw2H52eXBpAEeL",
        "portfolio_type":"modelportfolio",
        "status":"a",
        "editable":true,
        "sources":null,
        "integrations":[],
        "has_holdings":true,
        "name":"My first test portfolio",
        "slug":"my-first-test-portfolio",
        "holdings_as_of_date":"2022-03-22",
        "screen_sets":[],
        "strategies":[],
        "default_benchmark":null,
        "user":null,
        "metadata":{},
        "created_date":"2022-03-22T22:29:00.780635Z",
        "updated_at":"2022-03-22T22:29:07.007499Z",
        "model_sets":[],
        "one_metric_coverage":0.999949679239382,
        "percent_corporate":0.999949679239382,
        "nonzero_metric_coverage":0.999949679239382,
        "has_questionnaire_response":false,
        "accounts":[],
        "personas":[]
    }
}
```

### Retrieve a portfolio and include the holdings

Passing the `holdings` query parameter with the value `true` as `holdings=true` will include the portfolio holdings in the response.

```
curl -H "Authorization: Token YourTokenHere1234567890" https://yourstake.org/api/v1/portfolios/modelportfolio_A3rNbYtpEw2H52eXBpAEeL/?holdings=True
```

To run the curl command open a terminal and paste the command above.

The JSON response from the API should be similar to:

```
{
    "portfolio":{
        "id":"modelportfolio_A3rNbYtpEw2H52eXBpAEeL",
        "portfolio_type":"modelportfolio",
        "status":"a",
        "editable":true,
        "sources":null,
        "integrations":[],
        "has_holdings":true,
        "name":"My first test portfolio",
        "slug":"my-first-test-portfolio",
        "holdings_as_of_date":"2022-03-22",
        "screen_sets":[],
        "strategies":[],
        "default_benchmark":null,
        "user":null,
        "metadata":{},
        "created_date":"2022-03-22T22:29:00.780635Z",
        "updated_at":"2022-03-22T22:29:07.007499Z",
        "model_sets":[],
        "one_metric_coverage":0.999949679239382,
        "percent_corporate":0.999949679239382,
        "nonzero_metric_coverage":0.999949679239382,
        "has_questionnaire_response":false,
        "holdings":[
            {
                "id":58094404,
                "ticker":{
                    "id":5886,
                    "company":6212,
                    "full_name":"Apple Inc.",
                    "benchmark":36294,
                    "benchmark_symbol":"SPY",
                    "symbol":"AAPL",
                    "isin":"US0378331005",
                    "price":"160.55",
                    "total_value":2517000000000.0,
                    "exchange":"NASDAQ",
                    "asset_type":"Stock",
                    "company_name":"Apple Inc.",
                    "company_sector":"Industrial and Commercial Machinery and Computer Equipment",
                    "benchmark_description":null,
                    "expense_ratio":null,
                    "holdings_as_of_date":null,
                    "filing_date":null
                    },
                "dollars":500000.0
                },
            {
                "id":58094405,
                "ticker":{
                    "id":36294,
                    "company":11405,
                    "full_name":"SPDR S&P 500 ETF Trust",
                    "benchmark":24260,
                    "benchmark_symbol":"IWB",
                    "symbol":"SPY",
                    "isin":"US78462F1030",
                    "price":"468.89",
                    "total_value":345001228354.5,
                    "exchange":"NYSEARCA",
                    "asset_type":"ETF",
                    "company_name":"State Street Corporation",
                    "company_sector":"Depository Institutions",
                    "benchmark_description":"Large Blend",
                    "expense_ratio":0.0009,
                    "holdings_as_of_date":"2021-03-31",
                    "filing_date":"2021-05-28"
                    },
                "dollars":500000.0
            }
        ],
        "accounts":[],
        "personas":[]
    }
}
```

### Retrieve a portfolio and include the Screen Sets

Passing the `values` query parameter with a list of Screen Set ids will include the portfolio's alignment with each Screen Set.

Every portfolio will have a list of Screen Sets assigned by default. The default list is assigned  by and to the Firm or Advisor. [Visit the API Docs for the Screen Set Values to learn more](https://www.yourstake.org/api/docs/#tag/Values).

Getting the default Screen Sets requires an additional API call.

```
curl -H "Authorization: Token YourTokenHere1234567890" https://www.yourstake.org/api/v1/screen_sets/
```

To run the curl command open a terminal and paste the command above.

The JSON response from the API should be similar to:

**Note:** The response is typically large. I have included a smaller response on purpose. It does not change anything on your end.

```
{
  "screen_sets": [
    {
      "id": 1,
      "user": null,
      "name": "Friend of Animals",
      "metrics": [
        {
          "threshold": null,
          "metric_description": 6
        }
      ],
      "is_template": true,
      "created_at": "2020-09-30T21:04:16.464245Z",
      "updated_at": "2022-03-22T22:07:49.315409Z"
    },
    {
      "id": 2,
      "user": null,
      "name": "Planet Protector",
      "metrics": [
        {
          "threshold": null,
          "metric_description": 43
        },
        {
          "threshold": null,
          "metric_description": 23
        },
        {
          "threshold": null,
          "metric_description": 15
        },
        {
          "threshold": 0.1,
          "metric_description": 35
        },
        {
          "threshold": 0.1,
          "metric_description": 89
        }
      ],
      "is_template": true,
      "created_at": "2020-09-30T21:04:16.478727Z",
      "updated_at": "2022-03-22T22:07:49.316757Z"
    },
    {
      "id": 3,
      "user": null,
      "name": "Anti-Racist",
      "metrics": [
        {
          "threshold": null,
          "metric_description": 74
        },
        {
          "threshold": null,
          "metric_description": 59
        }
      ],
      "is_template": true,
      "created_at": "2020-09-30T21:04:16.506599Z",
      "updated_at": "2022-03-22T22:07:49.317478Z"
    }
  ]
}
```

You should now grab the value of the `id` fields and pass them as a list parameter `values=1,2,3`. This will tell the API to include the Screen Set data for each id in the portfolio response.

```
curl -H "Authorization: Token YourTokenHere1234567890" https://yourstake.org/api/v1/portfolios/modelportfolio_A3rNbYtpEw2H52eXBpAEeL/?values=1,2,3
```

To run the curl command open a terminal and paste the command above.

The JSON response from the API should be similar to:

```
{
    "portfolio":{
        "id":"modelportfolio_A3rNbYtpEw2H52eXBpAEeL",
        "portfolio_type":"modelportfolio",
        "status":"a","editable":true,
        "sources":null,
        "integrations":[],
        "has_holdings":true,
        "name":"My first test portfolio",
        "slug":"my-first-test-portfolio",
        "holdings_as_of_date":"2022-03-22",
        "screen_sets":[],
        "strategies":[],
        "default_benchmark":null,
        "user":null,
        "metadata":{},
        "created_date":"2022-03-22T22:29:00.780635Z",
        "updated_at":"2022-03-22T22:29:07.007499Z",
        "model_sets":[],
        "one_metric_coverage":0.999949679239382,
        "percent_corporate":0.999949679239382,
        "nonzero_metric_coverage":0.999949679239382,
        "has_questionnaire_response":false,
        "alignments":{
            "composite_values_1":7.0,
            "composite_values_2":5.2,
            "composite_values_3":6.4,
            "overall":6.2
        },
        "accounts":[],
        "personas":[]
    }
}
```

These numbers might not make a lot of sense now. I suggest you learn how to generate reports from portfolios in order to understand what these numbers mean to your clients and you. You can find a guide on how to generate reports [here]({{ site.baseurl }}{% link docs/guides/how-generate-reports-that-compare-portfolios.md %}).

