---
title: "Frequently Asked Questions During Mentorship Sessions"
description: "WIP"
date: "2020-11-27T14:46:58-06:00"
categories: 
  - Architecture
  - Engineering
  - Mentoring
  - Microservices
  - Technical Leadership
  - Technical Roles

draft: true

canonical_link: https://blog.eldermael.io/mentoring-faq
redirect_from:
  - /mentoring-faq
---

## Technical Leadership

### I Feel I Am Programming Less And Less \[As A Tech Lead], Is This Normal?

Yes. Technical leaders are moving to a path where you are no longer just
producing software i.e. an individual contributor. This is probably the most
asked question regarding transition from senior developers to tech leads.

What's important here is a bit of time management skills. I suggest having
a balanced schedule allowing new tech leads to still program while considering
the other skills required. Here is an ideal example:

- 30% of your time could be spent on the mentorship of yor team members,
- 30% could be spent on meetings/product development,
- 30% could be spent on coding,
- 10% can be spent on growing your own skills.

### What Skills Do I Need to Be A Tech Lead?

I think there are fundamentally 3 skills that you need to develop:

1. Leadership skills, being technical or not technical
1. System Design and Architecture skills, 
1. Developer skills, which you may already have

## Architecture

### As An Architect, Should I Still Develop Software?

Yes. Undoubtedly you don't want to become the proverbial [Ivory Tower 
Architect][2]. If you detach from programming completely, most probably
your solutions will also be detached from the code teams produce and
thus it becomes counterproductive because developers will be forced
to retrofit your solution instead of fit it more organically.

### What Coding Tasks An Architect Should Focus On?

In my experience, the best architects I have worked with usually spend
time on proofs of concepts and foundational technology. I have worked
with architects that usually pair program with developers to unravel
solutions that can fit the actual working code instead of coming up
with solutions that may or may not fit the current architecture.

## Microservices

### What's The Point Of Microservices?

This is a tough question, but I usually focus on these points that
work well with the _evolution analogy_:

1. Microservices are about _change independence_. As an example of
   a [evolutionary architecture][3], microservices allow evolution
   on different parts of your system quickly. Some services will be
   very stable once they reach a certain point but others need to 
   often change to accommodate business needs. Again, some parts of the
   organism evolve while others remain stable.  

[2]: https://www.youtube.com/watch?v=v_nhv6aY1Kg
[3]: https://evolutionaryarchitecture.com/