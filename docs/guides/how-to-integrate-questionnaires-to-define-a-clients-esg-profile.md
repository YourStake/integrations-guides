---
layout: default
title: How to integrate questionnaires to define a client's ESG profile
parent: Guides
---

# How to integrate questionnaires to define a client's ESG profile

Values questionnaires allow you to discover a client's values by having them answer
a set of questions.

The questions are in the form of statements that the client agrees, disagrees, or is neutral about. There are five ways a client may answer to a question. These are:

- Strongly agree

- Agree

- Neutral

- Disagree

- Strongly disagree

Each answer is valued differently. Their answers are used to understand where their personal values align. The alignment is used to generate reports that speak strongly to them.

##### Things you will need

- [API Access Token]({{ site.baseurl }}{% link docs/guides/how-to-request-api-access.md %})
- A prospect's email address


##### Create a prospect

Prospect objects allow you to create personalized ESG profiles for individuals. Every questionnaire requires you to pass either a prospect or client `id`. In this example, I'm showing you how to create a questionnaire with a prospect object. The steps to do it with an existing client is very similar.

First, let's define the request payload.

The [API Docs](https://www.yourstake.org/api/docs/#operation/Create%20a%20Prospect) state that  the only required field is the `email` field.

```
{"email": "my_test_prospect@example.org"}
```

Here's the curl command to create a prospect. Make sure to add your API Access Token and the prospect'e email address to the payload.

```
curl -d '{"email": "prospect email goes here"}' -H "Authorization: Token YourTokenGoesHere"  -H "Content-Type: application/json" -X POST https://yourstake.org/api/v1/prospects/
```

To run the curl command open a terminal and paste the command above.

The JSON response from the API should be similar to:

```
{
	"name": "None None",
	"email": "my_test_prospect@example.org",
	"id": "prospect_nNbfVXEgy39DmuCBGjYB29",
	"portfolio_type": "prospect",
	"metadata": {
	},
	"editable": true,
	"screen_sets": [
	],
	"default_portfolio": null,
	"created_date": "2022-03-24T12:45:42.016911Z",
	"updated_at": "2022-03-24T12:45:42.016914Z",
	"has_questionnaire_response": false
}
```

Save the value of the `id` field. You will need it in the steps below.

##### Working with values questionnaires

Questionnaires allow you to discover your prospect's values as part of a warm conversation. The questions have been carefully designed to create an individual ESG profile based on their answers.

Using our questionnaires is straightforward. You simply host the questionnaire content on your app and then send us the values of the answers collected. We take care of the rest.

To get the default questionnaire, run the command below:

```
curl -H "Authorization: Token YourTokenGoesHere" https://yourstake.org/api/v1/questionnaire/default/

```

The JSON response from the API should be similar to:

```
{
	"questionnaire": {
		"type_id": "default",
		"questions": [
			{
				"scoring_groups": [
					"fair_player"
				],
				"prompt": "Companies should pay workers a living wage, even if that means employing fewer people.",
				"slug": "living_wage_jobs",
				"type": "likert"
			},
			{
				"scoring_groups": [
					"planet_protector"
				],
				"prompt": "I go out of my way to reduce my environmental footprint.",
				"slug": "environmental_footprint",
				"type": "likert"
			},
			{
				"scoring_groups": [
					"female_empowerer"
				],
				"prompt": "A company can’t succeed without gender diversity.",
				"slug": "succeed_diversity",
				"type": "likert"
			},
			{
				"scoring_groups": [
					"anti_racist"
				],
				"prompt": "Prisons effectively deter crime.",
				"slug": "prison_crime",
				"type": "inverse_likert"
			},
			{
				"scoring_groups": [
					"friend_of_animals"
				],
				"prompt": "I avoid eating meat.",
				"slug": "avoid_meat",
				"type": "likert"
			},
			{
				"scoring_groups": [
					"fair_player"
				],
				"prompt": "CEOs should go to jail when their firms commit white-collar crime.",
				"slug": "ceo_jail",
				"type": "likert"
			},
			{
				"scoring_groups": [
					"peace_maker"
				],
				"prompt": "I would (or already do) own a gun.",
				"slug": "gun",
				"type": "inverse_likert"
			},
			{
				"scoring_groups": [
					"peace_maker"
				],
				"prompt": "I go out of my way to avoid buying products linked to forced labor (e.g. sweatshops).",
				"slug": "sweatshops",
				"type": "likert"
			},
			{
				"scoring_groups": [
					"female_empowerer"
				],
				"prompt": "Movie producers should ensure that female lead actresses earn as much as their male co-stars.",
				"slug": "equal_pay",
				"type": "likert"
			},
			{
				"scoring_groups": [
					"friend_of_animals"
				],
				"prompt": "Human lives are more important than animal lives.",
				"slug": "animal_important",
				"type": "inverse_likert"
			},
			{
				"scoring_groups": [
					"health_defender"
				],
				"prompt": "I avoid eating unhealthy fast food.",
				"slug": "healthy_food",
				"type": "likert"
			},
			{
				"scoring_groups": [
					"planet_protector"
				],
				"prompt": "Society should fix problems like healthcare and education before devoting resources to climate change.",
				"slug": "society_climate",
				"type": "inverse_likert"
			},
			{
				"scoring_groups": [
					"anti_racist"
				],
				"prompt": "Society should extend extra opportunities to historically oppressed minorities.",
				"slug": "extra_minority_opportunity",
				"type": "likert"
			},
			{
				"scoring_groups": [
					"health_defender"
				],
				"prompt": "People should not smoke tobacco.",
				"slug": "smoke_tobacco",
				"type": "likert"
			}
		]
	}
}
```

{% include important.html title="A note about questionnaire answers" body="YourStake uses a questionnaire rating of one (1) to five (5). One (1) being the lowest answer and five (5) being the highest. Please see the table below." %}

| Answer            | Rating            |
|:------------------|:------------------|
| Strongly Agree    |  5                |
| Agree             |  4                |
| Neutral           |  3                |
| Disagree          |  2                |
| Strongly Disagree |  1                |

Your app should use the same rating above in order to allow us to generate the prospect's ESG profile.

##### Saving questionnaire responses to create prospect ESG personas

The next step is to save the questionnaire answers.

To do so, you need the following information:

- A `questionnaire_type_id`. Please use `default`

- The prospect's `id`.

First, let's define the request payload.

```
{
    "living_wage_jobs": 3,
    "environmental_footprint": 2,
    "succeed_diversity": 5,
    "prison_crime": 1,
    "avoid_meat": 5,
    "ceo_jail": 3,
	"gun": 4,
    "sweatshops": 3,
	"equal_pay": 5,
    "animal_important": 2,
	"healthy_food": 3,
    "society_climate": 4,	
	"extra_minority_opportunity": 5,
    "smoke_tobacco": 3
}
```
Each key in the payload corresponds to each `slug` key in the question object of the questionnaire above. Example for `living_wage_jobs` below:

```

{
    "questionnaire": {
        "type_id": "default",
        "questions": [
            {
                "scoring_groups": [
                    "fair_player"
                ],
                "prompt": "Companies should pay workers a living wage, even if that means employing fewer people.",
                "slug": "living_wage_jobs",  <-------- 
                "type": "likert"
            }  
    }
}
```

The value of each item in the payload is the rating of the answer as translated with the table posted above.

You are now ready to save the responses through the API.

```
curl -d '{"client_id":"prospect_nNbfVXEgy39DmuCBGjYB29","answers":{"living_wage_jobs": 3,"environmental_footprint": 2,"succeed_diversity": 5,"prison_crime": 1,"avoid_meat": 5,"ceo_jail": 3,"gun": 4,"sweatshops": 3,"equal_pay": 5,"animal_important": 2,"healthy_food": 3,"society_climate": 4,"extra_minority_opportunity": 5,"smoke_tobacco": 3}}' -H "Authorization: Token YourTokenGoesHere" -H "Content-Type: application/json" -X POST https://www.yourstake.org/api/v1/questionnaire/default/responses/
```




To run the curl command open a terminal and paste the command above.

The JSON response from the API should be similar to the one below.

```
{
	"results": {
		"scores": {
			"fair_player": 6,
			"planet_protector": 4,
			"female_empowerer": 10,
			"anti_racist": 10,
			"friend_of_animals": 9,
			"peace_maker": 5,
			"health_defender": 6
		},
		"mappings": [
			{
				"target_identifier": "Friend of Animals",
				"target_type": "TemplateScreenSet",
				"rules": [
					"friend_of_animals > 7"
				]
			},
			{
				"target_identifier": "Anti-Racist",
				"target_type": "TemplateScreenSet",
				"rules": [
					"anti_racist > 7"
				]
			},
			{
				"target_identifier": "Female Empowerer",
				"target_type": "TemplateScreenSet",
				"rules": [
					"female_empowerer > 7"
				]
			}
		],
		"id": "questionnaireresponse_MrhsUhkzpeq6CAwStWzAs8",
		"client": {
			"name": "None None",
			"email": "my_test_prospect@example.org",
			"id": "prospect_nNbfVXEgy39DmuCBGjYB29",
			"portfolio_type": "prospect",
			"metadata": {
			},
			"editable": true,
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
				},
				{
					"id": 4,
					"user": null,
					"name": "Female Empowerer",
					"metrics": [
						{
							"threshold": null,
							"metric_description": 40
						},
						{
							"threshold": 0.1,
							"metric_description": 98
						},
						{
							"threshold": 0.1,
							"metric_description": 30
						}
					],
					"is_template": true,
					"created_at": "2020-09-30T21:04:16.539870Z",
					"updated_at": "2022-03-22T22:07:49.318153Z"
				}
			],
			"default_portfolio": null,
			"created_date": "2022-03-24T12:45:42.016911Z",
			"updated_at": "2022-03-24T12:45:42.016914Z",
			"has_questionnaire_response": true
		}
	}
}
```

The response returns:

- The prospects's ESG profile
- The questionnaire `id` (save it!)
- The prospect's values as Screen Sets
    - These are later used with the portfolio

The prospect's ESG profile is returned in this part of the response:

```
...
"scores": {
    "fair_player": 6,
    "planet_protector": 4,
    "female_empowerer": 10,
    "anti_racist": 10,
    "friend_of_animals": 9,
    "peace_maker": 5,
    "health_defender": 6
}
...
```

Each value ranges from zero (0) to ten (10).

Zero being the lowest and ten being the highest. 

A lower value means the prospect is less aligned with the ESG issue.

A higher value means the prospect is more or absolutely aligned with the ESG issue.

Show these values in your app to enable an investment conversation with your prospects.

![Sample prospect ESG profile](/assets/images/sample-prospect-esg-profile.png)
