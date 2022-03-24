---
layout: default
title: Impact
parent: Reports
---

# When to use an impact report

An impact report is best used to highlight the social impact of a person's investment portfolio.
You can use this data to show your clients how their investment impacts the environment, health, human rights, etc. 

The impact report creates a very clear picture of a client's portfolio in terms of ESG factors.


## How to create an impact report


The general steps to create an impact report are:

- Get or create a portfolio in YourStake through our dashboard or an [API call](https://www.yourstake.org/api/docs/#operation/Create%20a%20Portfolio).
    - **Note**: Write down the portfolio `id`. It looks like this `modelportfolio_xyz12345ab67890`.

- Get or create the [Screen Sets](/docs/glossary/#screen-sets) for the user or portfolio through an [API call](https://www.yourstake.org/api/docs/#operation/List%20Screen%20Sets).

- Make an API call to the [reports API endpoint](https://www.yourstake.org/api/docs/#tag/Reports). This requires that you also include the [Screen Sets](/docs/glossary/#screen-sets) as part of the request.
    - Don't worry about details. We will cover those in depth next.

- Use the JSON data from the reports API response to add to your UI.
    - To see a simple demo template in action [click here](/)

