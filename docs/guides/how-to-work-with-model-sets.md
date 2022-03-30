---
layout: default
title: How to work with model sets
parent: Guides
nav_order: 9
---

# How to work with model sets

[API Docs](https://www.yourstake.org/api/docs/#tag/Model-Matchmaker)

A Model Set is a collection of portfolios that can be screened by a set of Values. They are part of the Model Matchmaker functionality.


## How to create a model set

To create a model set, you need the following.

- [API Access Token]({{ site.baseurl }}{% link docs/guides/how-to-request-api-access.md %})
- A unique name to be used as the unique identifier
- Your firm `id`
- A name

See the sample payload below.

```
{
  "firm": 1,
  "name": "Model set for client ABC"
}
```

Grab your API Access Token and put it here.

```
-H "Authorization: Token YourTokenGoesHere" 
```

Now paste your payload and token into the curl command below.

```
curl -d 'Your Payload Here'  -H "Authorization: Token YourTokenGoesHere"  -H "Content-Type: application/json" -X POST https://www.yourstake.org/api/v1/model_sets/
```

Here is a complete example.

```
curl -d '{"id":"my_unique_model_set_name","firm":1,"name":"Model set for client ABC"}' -H "Authorization: Token YourTokenGoesHere" -H "Content-Type: application/json" -X POST https://www.yourstake.org/api/v1/model_sets/
```

To run the curl command open a terminal and paste the command above.
The JSON response from the API should be similar to:

```
{
    "id":"modelset_N9xGLucMPcyHKHCbmPetHQ,
    "internal_identifier":null,
    "firm":1,
    "name":"Model set for client ABC",
    "created_at":"2022-03-30T16:39:32.112016Z",
    "updated_at":"2022-03-30T16:39:32.112044Z",
    "editable":true
}
```

The response contains the field `editable`. It let's you know if the user in  context is able to edit the model set data. A firm admin typically is the user allowed to edit.


## How to add portfolios to a model set

[API Docs](https://www.yourstake.org/api/docs/#operation/Partial%20update%20a%20Model%20Set)

Adding portfolios to a model set requires the following.

- A model set `id`
- A list of portfolio `id`s


See the sample payload below.

```
{
  "model_ids": [
      "modelportfolio_A3rNbYtpEw2H52eXBpAEeL",
      "modelportfolio_CLWecXizzZJzC3KpzX7JX7"
    ]
}
```

Grab your API Access Token and put it here.

```
-H "Authorization: Token YourTokenGoesHere" 
```

Now paste your payload and token into the curl command below.

```
curl -d 'Your Payload Here'  -H "Authorization: Token YourTokenGoesHere"  -H "Content-Type: application/json" -X PATCH https://www.yourstake.org/api/v1/model_sets/modelset_N9xGLucMPcyHKHCbmPetHQ/
```

Here is a complete example.

```
curl -d '{"model_ids":["modelportfolio_A3rNbYtpEw2H52eXBpAEeL","modelportfolio_CLWecXizzZJzC3KpzX7JX7"]}' -H "Authorization: Token YourTokenGoesHere" -H "Content-Type: application/json" -X PATCH https://yourstake.org/api/v1/model_sets/modelset_N9xGLucMPcyHKHCbmPetHQ/
```

To run the curl command open a terminal and paste the command above.
The JSON response from the API should be similar to:

```
{
	"id": "modelset_N9xGLucMPcyHKHCbmPetHQ",
	"internal_identifier": null,
	"firm": 1,
	"name": "Model set for client ABC",
	"model_portfolios": [
		{
			"id": "modelportfolio_CLWecXizzZJzC3KpzX7JX7",
			"nickname": "My second test portfolio",
			"status": "a",
			"slug": "my-second-test-portfolio",
			"created_date": "2022-03-23T21:44:43Z",
			"updated_at": "2022-03-24T14:44:32.575879Z",
			"fact_sheet_url": null,
			"meta_external_id": null,
			"external_id": "modelportfolio_CLWecXizzZJzC3KpzX7JX7",
			"strategies": [
			]
		},
		{
			"id": "modelportfolio_A3rNbYtpEw2H52eXBpAEeL",
			"nickname": "My first test portfolio",
			"status": "a",
			"slug": "my-first-test-portfolio",
			"created_date": "2022-03-22T22:29:00Z",
			"updated_at": "2022-03-24T14:44:23.653886Z",
			"fact_sheet_url": null,
			"meta_external_id": null,
			"external_id": "modelportfolio_A3rNbYtpEw2H52eXBpAEeL",
			"strategies": [
			]
		}
	],
	"created_at": "2022-03-30T17:57:48.331267Z",
	"updated_at": "2022-03-30T18:01:33.853021Z"
}
```


## How to check a model set alignment with a client's values

[API Docs](https://www.yourstake.org/api/docs/#operation/Model%20Set%20Detail)

Checking how a model set aligns with a client's values requires the following.

- A model set `id`.
- The client's Screen Sets values `id`s. These are passed as query parameters. Example: `values=1,2,3`.

The curl command is straightforward.

```
curl  -H "Authorization: Token YourTokenGoesHere" "https://www.yourstake.org/api/v1/model_sets/modelset_N9xGLucMPcyHKHCbmPetHQ/?values=1,3,4"
```

To run the curl command open a terminal and paste the command above.
The JSON response from the API should be similar to:

```
{
	"id": "modelset_N9xGLucMPcyHKHCbmPetHQ",
	"internal_identifier": null,
	"firm": 1,
	"name": "Model set for client ABC",
	"model_portfolios": [
		{
			"id": "modelportfolio_CLWecXizzZJzC3KpzX7JX7",
			"nickname": "My second test portfolio",
			"status": "a",
			"slug": "my-second-test-portfolio",
			"created_date": "2022-03-23T21:44:43Z",
			"updated_at": "2022-03-24T14:44:32.575879Z",
			"alignments": {
				"composite_values_1": 1.4,
				"composite_values_3": 10.0,
				"composite_values_4": 5.1,
				"overall": 5.5
			},
			"fact_sheet_url": null,
			"meta_external_id": null,
			"external_id": "modelportfolio_CLWecXizzZJzC3KpzX7JX7",
			"strategies": [
			]
		},
		{
			"id": "modelportfolio_A3rNbYtpEw2H52eXBpAEeL",
			"nickname": "My first test portfolio",
			"status": "a",
			"slug": "my-first-test-portfolio",
			"created_date": "2022-03-22T22:29:00Z",
			"updated_at": "2022-03-24T14:44:23.653886Z",
			"alignments": {
				"composite_values_1": 7.0,
				"composite_values_3": 6.4,
				"composite_values_4": 5.9,
				"overall": 6.433333333333334
			},
			"fact_sheet_url": null,
			"meta_external_id": null,
			"external_id": "modelportfolio_A3rNbYtpEw2H52eXBpAEeL",
			"strategies": [
			]
		}
	],
	"created_at": "2022-03-30T17:57:48.331267Z",
	"updated_at": "2022-03-30T18:01:33.853021Z"
}
```

Each portfolio in the response `model_portfolios` field will contain alignment values for every screen set in the field `alignments`. [Learn more about working with these values]({{ site.baseurl }}{% link docs/guides/how-to-integrate-questionnaires-to-define-a-clients-esg-profile.md %}).

You may use each individual alignment value to compare how different portfolios compare or use the overall alignment. Each value may represent a different perspective for your clients. We suggest making use of all values whenever possible.