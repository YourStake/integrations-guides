---
layout: default
title: How to generate reports that show values alignment
parent: Guides
nav_order: 10
---

# How to generate reports that show values alignment

Clients want to know the values alignment of different portfolios.
They want to compare to make data driven decisions.

**Generating reports that show how a client's values align is done in four steps.**



1 - Create a portfolio model set

You create a portfolio for the client and post it to the API.

[Guide to create a portfolio for the client through the API]({{ site.baseurl }}{% link docs/guides/how-to-create-a-portfolio.md %}).


2 - Discover and capture a client's values alignment.

A client completes a values questionnaire.

[Guide to complete a questionnaire through the API]({{ site.baseurl }}{% link docs/guides/how-to-integrate-questionnaires-to-define-a-clients-esg-profile.md %}).

<img src="{{ site.baseurl }}/assets/images/sample-questionnaire.png" width="75%" height="75%">


3 - Apply the client's values to the portfolio model set

[Guide to work with model sets through the API](% link docs/guides/how-to-work-with-model-sets.md %)

4 - Generate a report that compares the portfolios in the model set. This will allow you to build similar reports into your application and wow your clients.

Get the comparison report (customized to the client's values preferences) from the API and render it in your app.

[Guide to generate reports that compare portfolios for the client through the API]({{ site.baseurl }}{% link docs/guides/how-to-generate-reports-that-compare-portfolios.md %}).

##### Rendering an HTML comparison report for the model set

[Download Sample Comparison Report]({{ site.baseurl }}/templates.zip)

We have created an HTML template using the report and portfolio data
and generated a sample report for you.

This allows you to see a working example and get a hands on understanding of how to incorporate the reports data in your app.

The samples are built using the [Bootstrap framework](https://getbootstrap.com) for ease of use.

![Sample impact report template screenshot]({{ site.baseurl }}/assets/images/sample-comparison-report.png)




