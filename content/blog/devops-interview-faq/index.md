---
title: "DevOps and SRE Interview Guide"
description: "After a lot of interviews, here is my compilation of frequently asked questions and sections"
date: "2020-11-27T14:46:58-06:00"
categories: 
  - DevOps
  - SRE  
  - Interviewing

draft: true

canonical_link: https://blog.eldermael.io/interviewing-devops-guide
redirect_from:
  - /interviewing-devops-guide
---

I had the fortune of having fantastic mentors at the beginning of my career and one thing always sticked to me very
early during my formative years. One of the engineers I consider a mentor on all aspects of software development 
mentioned that he interviews more or less every year on companies regardless of the situation i.e. if he is looking
for a job or not. He mentioned that he interviews to know if he is being underpaid, to know which technologies he should
be studying and are hot on the market, and of course, to maybe get something better and switch jobs.

Is because of this that I seasonally take interviews at different companies and startups. I think I have been doing this
for at least 8 years since I got out of my first tech lead position.

Now, interviewing is hard and very broken in our industry, many companies have tried to solve it, but they are mostly
doing the same thing with different flavors. You can see the patterns of course and books like "Cracking the Code 
Interview" exist for a reason.

I have been working on SRE/DevOps roles for at least 5 years now and here are very common sections and some sort of
explanation of such and frequently asked questions as well as follow-up questions.

## Programming Section

Around 70% of the interviews I took had a programming section. This is not surprising because most SRE/DevOps roles do
require programming knowledge.

### Take Home Assignment

### Live Coding

### Website Programming Challenges

### Usual Follow-Ups

- Explain the code to interviewers
- Add a small but not trivial improvement to the project
- Deploy the code itself to a sandbox environment

## System Design Section

Around 50% of the interviews had a system design section.

### Usual Follow-Ups

### Scale Given System

### Usual Follow-Ups

## Past Projects and Experience Section

Around 60% of the interviews had a section to talk about past projects and experience on them.

### Usual Follow-Ups

## Pipeline Design Section

Around 30% of the interviews had a section to design a pipeline for a small service. Note that many times you deploy
the service you just created in the programming section or as part of the home assignment.

This section is common enough that I already have a "script" to follow up. Most of the time I try to design pipelines
using 3 mayor sections:

- Build i.e. generate artifacts and configuration bundles
- Deploy i.e. place an artifact in order to await for traffic
- Release i.e. make the artifact operational e.g. start receiving traffic

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


### Usual Follow-Ups

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