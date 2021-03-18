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

## Programming Section

Around 70% of the interviews I took had a programming section. These 

### Take Home Assignment

### Live Coding

### Website Programming Challenges

### Usual Follow Ups

- Explain the code to interviewers
- Add a small but not trivial improvement to the project
- Deploy the code itself to a sandbox environment

## System Design Section


### Usual Follow Ups

### Scale Given System

### Usual Follow Ups

## Past Projects and Experience Section

### Usual Follow Ups

## Pipeline Design Section

This section is common enough that I already have a "script" to follow up. Most of the time I try to design pipelines
using 3 mayor sections:

- Build i.e. generate artifacts and configuration bundles
- Deploy i.e. place an artifact in order to await for traffic
- Release i.e. make the artifact operational e.g. start receiving traffic

Optionally, I pinpoint that there are pipelines that are going to process artifacts/code through compliance stages
such as security scans, architecture fitness functions, performance testing, etc. These tasks are not common and
they should not fail the build in case issues are found (the discussion about why is another interesting topic but
outside scope)

### Usual Follow Ups

## Troubleshooting System Section

### Usual Follow Ups

## Curious Findings

Only one company asked CyberSec questions