---
layout: default
title: Glossary
---

# Glossary
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---


## API Token

An API token allows applications to login to access our API without using your username and password.
API access is oriented around a specific user account. YourStake account holders and API sandbox users can access the API with a bearer token with access restricted to their user account. If you're an existing YourStake client please [contact us](https://www.yourstake.org/info/api) for API access.

If tokens have been provisioned for your account you can find them [here](https://www.yourstake.org/api/auth/).


## Portfolio

A portfolio contains the range of investments held by an entity.


## Screen Sets

[API Docs](https://www.yourstake.org/api/docs/#tag/Values)

Reports use what we call **Screen Sets**. They are collections of Impact Factor metrics with a threshold for each metric. They are created automatically after a user takes the [Questionnaire]({{ site.baseurl }}{% link docs/guides/how-to-integrate-questionnaires-to-define-a-clients-esg-profile.md %}), and can be directly associated with a Prospect or Portfolio.

Screen Set ids can be passed as parameters to other endpoints to tailor the information that's returned.

{% include important.html title="Important Note About Screen Sets" body="Screen sets may also be known in our documentation as <strong>Impact factors</strong>" %}

