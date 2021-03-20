---
title: "DevOps and SRE Interview Guide"
description: "After a lot of interviews, here is my compilation of frequently asked questions and sections"
date: "2020-11-27T14:46:58-06:00"
categories: 
  - DevOps
  - SRE  
  - Interviewing

draft: false

canonical_link: https://blog.eldermael.io/interviewing-devops-guide
redirect_from:
  - /interviewing-devops-guide
---

I had the fortune of having fantastic mentors at the beginning of my career and one thing always sticked to me very
early during my formative years. One of the engineers I consider a mentor on all aspects of software development 
mentioned that he interviews more or less every year on companies regardless of the situation i.e. if he is looking
for a job or not. He mentioned that he interviews to know if he is being underpaid, to know which technologies he should
be studying and are hot on the market, and of course, to maybe get something better and switch jobs.

Because of this, I seasonally take interviews at different companies and startups. I think I have been doing this
for at least 8 years since I got out of my first tech lead position.

Now, interviewing is hard and very broken in our industry, many companies have tried to solve it, but they are mostly
doing the same thing with different flavors. You can see the patterns of course and books like "Cracking the Code 
Interview" exist for a reason.

I have been working on SRE/DevOps roles for at least 5 years now and here are common sections and some sort of
explanation of such and frequently asked questions as well as follow-ups.

## Programming Section

Around 70% of the interviews I took had a programming section. This is not surprising because most SRE/DevOps roles do
require programming knowledge.

### Take Home Assignment

The two most common take home assignments these days are to build a CLI or an API. Huge home assignments also require
logging in to a sandbox and deploy your API by building a pipeline and somehow make it available to the internet to
query. Usually they are intermingled with pipeline design for CI/CD questions.

### Live Coding

This is no surprise, live coding a small program to solve a predefined problem is the go to of most programming 
sections. One of the most common problems are:

- Read a log file and sort it, count the number of lines that match a pattern, explain the performance implications
  of your algorithm

### Website Programming Challenges

This is usually the first filter I have seen in places where they do not want to do a take home assignment, or a live
pair programming challenge. Sometimes this is OK because it removes a lot of hours from the interview process. 
HackerRank is the most common website for this.

### Usual Follow-Ups

- Explain the code to interviewers, specially from take home assignments
- Add a small but not trivial improvement to the project you delivered
- Deploy the code itself to a sandbox environment, modify it to have some sort of observability

## System Design Section

Around 50% of the interviews had a system design section. This is also a section I enjoy and I kinda have a script for
such interviews.

1. I tend to ask the business need for such system. Not advocating for a change, just explaining that most of the time
   we have to deal with value-based delivery and seeing the business justification for a system tends to help to focus
   on the right questions.
   
1. I ask for hardware constraints or any kind of cloud restrictions. Also, expected number of users/operations as well
   as future usage. This gives me a way to figure out if I need to design for vertical or horizontal scale.
   
1. I tend to stick to 4+1 architectural view model to describe the system I am designing and zooming in or out depending
   on the questions asked. It's always a good idea to start from the higher views to the lower views and ask clarifying
   questions before proceeding to the next level. This tends to have good results (I even mention the model explicitly).

### Usual Follow-Ups

- What would you change in your current work regarding architecture?
- Have you worked on companies where they have good implementations of this problem? If true, explain it so.

## Scale Given System

Around 25% of the interviews had a section to discuss how to scale out a given system. This section is kinda 
descriptive and with some kind of overlap with the System Design section but is also different enough to differentiate 
it from the others.

The most common scenarios are:

- Given N servers with the same hardware, how would you deploy applications to best scale the system. This question
  usually involves an orchestrator but sometimes the twist is given is to not use it.
  
- How would you scale a service where the database server is the current bottleneck? Sharding and horizontal slicing
  are handy concepts here.
  
- You are tasked to design a system to scale the deployment of new versions of an artifact in different regions. I have
  seen variants of these that require the use of P2P networks or clients within the servers themselves along a pipeline
  to execute them. 
  

## Past Projects and Experience Section

Around 60% of the interviews had a section to talk about past projects and experience on them. This section is the one
I enjoy the most because this is just a talk, and it tends to go very well because I really like to talk about what I
have done and seen!

I try to align my conversation to whatever technologies the company I am interviewing for is using. I also try to talk
about different strategies used in different companies and give context of why each one is a better fit for each one.


### Usual Follow-Ups

- What would you change if you had the power in your past projects?

## Pipeline Design Section

Around 30% of the interviews had a section to design a pipeline for a small service. Note that many times you deploy
the service you just created in the programming section or as part of the home assignment.

This section is common enough that I already have a "script" to follow up. Most of the time I try to design pipelines
using 3 mayor sections:

- Build i.e. generate artifacts and configuration bundles
- Deploy i.e. place an artifact in order to await for traffic
- Release i.e. make the artifact operational e.g. start receiving traffic
- Compliance i.e. pipelines that run cross-cutting concerns, etc.

Optionally, I pinpoint that there are pipelines that are going to process artifacts/code through compliance stages
such as security scans, architecture fitness functions, performance testing, etc. These tasks are not common and
they should not fail the build in case issues are found (the discussion about why is another interesting topic but
outside scope)

### Usual Follow-Ups

- How would you handle rollbacks?
- What happens if I need to deploy a hotfix fast?
- How do you manage promotion?

## Troubleshooting System Section

Around 25% of the interviews had a section in which you will be described a situation where you are to troubleshoot and
fix production systems.

While this is more of a freeform stage, most companies really only go so far. A typical scenario starts with how you
would set an alarm for a specific time series (HTTP requests failing for example). Then they ask you how would you
find the issue and provide you with a response for each question.

In more than one occasion I have said that I would try to fix the issue myself in the code (or rebooting, or whatever)
if possible to avoid bothering engineers on-call. This tends to be a double-edged sword as some companies have a culture
of just handing off the problem to the next person on call and suggesting fixing the problems in-place is a form of
anarchy. I tend to avoid those companies, the least bureaucracy the better.

Another point of conflict is the use of small commits and trunk based development in conjunction with roll-forwards
instead of rollbacks.


### Usual Follow-Ups

- Explain an issue you have had on your project and how did you troubleshoot it.
- How would you design a rollback strategy for errors in production?

## What is what I ask often?

- What's the most bureaucratic task that you have to do on you every day work? This lets me know the kind of culture I 
  would expect from the company.

- What's the benefit you like the most from your company? I want to know what kind of benefits people enjoy and use at
  work. This gives me an idea about why people are there.
  
- When was the last time you worked overtime? I really want to know if they overwork you and how often. Crunch time? Is
  overtime paid?

## Curious Findings

Only one company asked CyberSec questions, this is kinda alarming now that I have had to focus more on these areas
on different companies and platforms.