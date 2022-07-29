---
id: 16012
title: 'Object Modeling Strategies (IV)'
date: '2005-10-11T16:51:43+08:00'
author: Jay
layout: post
guid: 'https://www.jayxu.com/?p=16012'
permalink: /2005/10/11/16012
posturl_add_url:
    - 'yes'
views:
    - '1264'
hefo_before:
    - '0'
hefo_after:
    - '0'
---

<i><strong>Str#6. "Four Kinds of Features" Strategy // identifying purpose and features</strong></i>

- Be certain to include features that cover the following:

1. Log important information.

2. Conduct business.

3. Analyze business results.

4. Interact with other systems.

<i>
<strong>Str#6a. "Add Features, Inspired by Patterns" Strategy // identifying purpose and features</strong></i>

- Add features inspired by the stereotypical responsibilities of a participant (in Patt#3, Participant-Transaction), transaction (in Patt#6, Transaction - Transaction Line Item), and place (in Patt#4, Place-Transaction).

- Examples: assess the performance of a participant (how many, how much), calculate the total of a transaction, assess the performance of a place (how many, how much).

<i>
<strong>Str#6b. "Organize and Prioritize Features" Strategy // identifying purpose and features</strong></i>

- Organize the features into &amp;quotfeature categories" (also known as &amp;quotuse cases").

. Example: maintaining employee info; assigning employees; assessing employee performance

- Prioritize the features.

. Identify the prioritization criteria. For example: normal sequence of business usage; greatest risk; customer interest; management interest; ease of implementation.

<i>
<strong>Str#7. "Calculation Results and Decision Points" Strategy // identifying purpose and features</strong></i>

- Add features that deliver calculation results.

- Add features that support decision points.

<i>
<strong>Str#8. "Best and Worst Features" Strategy // identifying purpose and features</strong></i>

- Ask users:

- What are the best features of the current system? Of competitive systems?

- What are the worst problems of the current system? Of competitive systems?

- What are the unneeded features of the current system? Of competitive systems?

<i>
<strong>Str#9. "Top 10" Strategy // identifying purpose and features</strong></i>

- Build a list of features.

- When you face an abundance of features (or classes, attributes, services), go after the top 10.

- Why: avoid being overwhelmed by a sea of low-level details.

<i>
<strong>Str#10. "Now and Later" Strategy // identifying purpose and features</strong></i>

- Consider current capabilities--and anticipated future capabilities.

- Ask, "How is it done now? How will it be done later, with the new system?"

- Look at things that people do to objects now, and consider features you can add (your automated objects might be able to do those actions to themselves).

<i>
<strong>Str#11. "Reengineer on the Boundaries" Strategy // identifying purpose and features</strong></i>

- Look at each organization or automated system boundary.

- Look for duplicate efforts on each side of such a boundary.

- Model the capability one time--and encourage some reengineering improvements for the organization.

<i>
<strong>Str#12. The "Smarter Devices" Strategy // identifying purpose and features</strong></i>

- Look for opportunities to use smarter devices, simplifying your object model and reducing software development schedule and costs.

- When building an object model in a field with rapidly changing data acquisition and control technology, be sure to take a systems perspective, spanning both hardware and software.