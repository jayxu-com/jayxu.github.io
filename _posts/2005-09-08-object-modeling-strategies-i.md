---
id: 15990
title: 'Object Modeling Strategies (I)'
date: '2005-09-08T10:12:45+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=15990'
permalink: /2005/09/08/15990
posturl_add_url:
    - 'yes'
hefo_before:
    - '0'
hefo_after:
    - '0'
views:
    - '2264'
dsq_thread_id:
    - '5287606146'
---

<strong>Activities and model components</strong>

<i><strong>Str#1. "Four Major Activities, Four Major Components" Strategy // activities and model components</strong></i>

- Organize your work around four major activities, within four major components:

- Four major activities:

. Standard: Identify purpose and features, select objects, establish responsibilities, work out dynamics with scenarios.

. Variation 1: You may find it helpful to focus on working out dynamics with scenarios, establishing responsibilities along the way. This is especially suitable for real-time applications.

. Variation 2: You may find it helpful to select transaction, aggregate, and plan objects, then use the corresponding patterns to guide you through selecting additional objects, establishing responsibilities, and working out dynamics with scenarios.

- Four major components:

. Standard: Problem domain, human interaction, data management, system interaction.

. Variation 1: You may find it helpful to begin with human interaction, followed by problem domain, data management, and system interaction. This is especially suitable when your domain experts want to talk in terms of human interaction from the very start.

. Variation 2: You may find it helpful to begin with problem domain and system interaction, followed by human interaction and data management. This is especially suitable for real-time applications, when your domain experts are keenly interested in the data acquisition and control aspects of the system under consideration.

<i>
<strong>Str#1a. "Build an Initial Object Model, then Proceed Feature-by-Feature" Strategy // activities and model components</strong></i>

- Here is a very helpful path for building object models.

- Identify purpose and features.

. Purpose statement. Prioritized list of features.

- Build an initial object model, working with domain experts.

. Select initial objects (using strategies; include participants, transactions, places, items, specific items).

. Establish initial responsibilities (using strategy #86 and the stereotypical responsibilities expressed by object-model patterns).

- Work out dynamics with scenarios, feature-by-feature.

a. Develop a scenario view for the feature.

b. Add objects and responsibilities that you need for the scenario.

<i>
<strong>Str#1b. "Use Feature Milestones" Strategy // activities and model components</strong></i>

- Use your prioritized features list to plan, build, and measure.

- Early in the development effort, use your prioritized features list day-by-day, while developing an initial object model and scenario views (one scenario view for each feature).

- For the rest of the development effort, use your prioritized features list to plan, build, and measure what you produce -- namely, the frequent, tangible, working results.

- Some notes:

. How frequent is "frequent"?

. . Each week, each month, or each quarter -- depends upon the size of the project and the amount of added effort required to make working results available to others.

- Why use features milestones -- and measure features completed, using frequent, tangible, working results?

. In two words: risk reduction.

- How do you estimate percent completion?

. Take the features list, assign a weight to each feature (based upon level of difficulty, relative number of lines of code, and level of skill of the person who will do the work), and then make your estimates.

. Your estimates will improve over time, as you deliver more and more tangible results along the way.

<i>
<strong>Str#1c. "Take Multiple Paths" Strategy // activities and model components</strong></i>

- For each outcome, consider multiple paths for reaching that goal. Travel down one of those paths. When your progress slows somewhat, move to another path, for awhile.

- "All features, all classes, then the top ten classes"

. features -&gt; classes -&gt; top 10 classes -&gt; responsibilities, scenarios for the top 10

- "One feature at a time"

. feature -&gt; small object model -&gt; scenario view

- "Key players first"

. 1-2 participants + 1-2 transactions + line items, items -&gt; responsibilities, scenarios

- "Key transactions first"

. transaction - subsequent transaction - subsequent transaction -&gt; participants, line items, items -&gt; attributes, services