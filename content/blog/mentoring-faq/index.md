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

draft: false

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

A good reference for this kind of transition for me has been the work of [Patrick Kua][1]
on the topic. [Here][6] is the most influential talk I could find for this.

### What Skills Do I Need to Be A Tech Lead?

I think there are fundamentally 3 skills that you need to develop:

1. Leadership skills, being technical or non-technical,
1. System Design and Architecture skills and,
1. Developer skills, which you may already have.

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

I think this approach has the best results overall because it proofs
that your architecture guidelines and implementations fit into the
software other teams are developing.

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
   
1. Faster time to market. Following from the previous point, once you
   know that the microservice architecture style allows for faster change
   and independence you are able to quickly prototype new ideas because
   you can start new business lines from scratch quickly, [with the right
   tools (spanish)][7].

1. Making innovation cheaper. As a side effect of the previous point,
   microservices enable to quickly prototype new ideas because you can 
   start new business lines from scratch quickly with the right tools.

### Do You Think We Are Ready To Adopt Microservices?

Microservices are not a free meal. [Conway's law][4] is an important
concern if you plan to adopt this architecture style. This is because
there is a social/organizational component to every software architecture
style and having organizations simply jump into microservices without
the proper mindset can be problematic.

If you use Conway's law to your favor, service-based architectures can
help move faster, but without organizational perspective it usually works
against the adoption.

## DevOps

### What Are The Most Common Questions You Are Asked During Interviews?

After quite a bit of interviews I have seen common questions and follow-ups:

1. What is DevOps? The interviewer wants to know if you "get DevOps". Focus
   on why DevOps is more of a practice and cultural mindset instead of titles. 
   
1. What is SRE? Software Reliability Engineering is kind of defined as:

    > One could view DevOps as a generalization of several core SRE principles to 
    > a wider range of organizations, management structures, and personnel. One 
    > could equivalently view SRE as a specific implementation of DevOps with some 
    > idiosyncratic extensions.

   Per [Google's own book on the matter][5].

1. What's the difference between DevOps and SREs? Per the previous question, 
but paraphrasing here, I think of SRE as an implementation of DevOps practices done 
by Google.

1. Can you describe/document a pipeline to deliver code from scratch? This is a
   lengthy question that may deserve its own post! it gets asked often.

[1]: https://twitter.com/patkua
[2]: https://www.youtube.com/watch?v=v_nhv6aY1Kg
[3]: https://evolutionaryarchitecture.com/
[4]: https://en.wikipedia.org/wiki/Conway%27s_law
[5]: https://sre.google/sre-book/introduction/
[6]: https://www.youtube.com/watch?v=iLS6NXMXtLI&t=1153s
[7]: https://www.youtube.com/watch?v=YLq3x-WtaRc&t=26s