---
id: 15997
title: 'Object Modeling Strategies (II)'
date: '2005-09-19T15:23:21+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=15997'
permalink: /2005/09/19/15997
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '1371'
---

<i><strong>Str#1d. "Invest an Hour" Strategy // activities and model components</strong></i>

- Rather than philosophize endlessly, invest an hour in each of several different ways of modeling a particularly challenging area. Compare your results -- and decide which way to go (based upon actual results, rather than the outcome of a multiweek debate).

<i><strong>
Str#1e. "Consider the Domain First, Artifacts After That" Strategy // activities and model components</strong></i>

- Build an object model with a domain expert first. Then add-in content that you can extract from artifacts (existing data models, source code, whatever).

- Reason why: you need the benefit of the former (fresh insights, new ideas) to help you grapple with the latter (what to include, what to exclude).

<i><strong>
Str#1f. "Extract Useful Content From An Existing Data Model" Strategy // activities and model components</strong></i>

- Yes, it can be done.

- Best practice: build an initial object model with a domain expert first. Then use that model to help you filter out the classes and attributes (in an previous data model) that are no longer needed. Why: the added domain understanding will help you do a better job leaving unneeded things behind, rather than dragging everything from the past along with you once again.

- For the entities:

. List them. Delete correlation tables. Delete (or revise) names that do not fit the problem domain vocabulary (words that a domain expert uses and understands). Collapse supertypes-subtypes that do not express domain-based generalization-specialization.

- Then, when you work on attributes:

. List them. Delete (or revise) names that do not fit the problem domain vocabulary (words that a domain expert uses and understands). Delete flags, indicators, sequence numbers, and unique keys -- nearly all of which are simply leftover implementation mechanisms from a previous system.