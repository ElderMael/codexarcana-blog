---
title: Shared Pipeline Libraries To Deploy Microservices
description: >-
  Previously in my post about Digital Platform Accelerators, I wrote about
  Delivery Workflow Tools. A pattern within these tools was Shared…
date: '2019-07-12T08:44:08.147Z'
categories: []
keywords: []
slug: /@eldermael/shared-pipeline-libraries-to-deploy-microservices-d8859d53e20
---

![](img/0__GTo__So9b7zkKgBJz.jpg)

Previously in my post about [Digital Platform Accelerators](https://medium.com/@eldermael/digital-platform-accelerators-a897ec4b92f4), I wrote about Delivery Workflow Tools. A pattern within these tools was Shared Pipeline Libraries.

So far I have implemented pipelines on three different microservice platforms for three different companies and I intend to explain my experience in this post.

### Reasoning: Do Not Repeat Yourself And Avoid A Death By A Thousand Cuts

About three years ago I was working on a project that had started with relatively few services, only five of them and three front end applications. By instructions of the CTO at the time, I was assigned to the testing team as a quality engineer in charge of writing Cucumber tests for a series of Web Services made using JAX-WS that were going to be “refactored” into modern technologies.

I am glad to say that I proved my CTO wrong because I wanted to go to the team in charge of building the tooling that these new services were going to use. This team was branded the DevOps team and they were going to be in charge of provisioning the infrastructure and maintain a single Jenkins server that will be used for all of this. By implementing the pipeline for running my own tests against the web services I was able to ask for a chance to work on that team because they were understaffed at the moment.

I was very new to Jenkins so the first thing that we tried to do was to program the Jenkinsfiles for each project ourselves in the eight repositories that were available.

Soon I found that I had a lot of repetition on these files. I mostly had copy-pasted the code there and changed a few things such as project names and other parameters.

As you can see this was not good but at the time the idea was that the teams in charge of those projects were going to write themselves those files once we had set up the patterns to deploy to the infrastructure we provided. Of course, software is organic and more requirements come and pipelines need to evolve thus we had to oil those Jenkinsfiles many times to add new features such as security scans, SonarQube quality gates, etc.

Our developers were busy delivering value features so the work of our team was to introduce patterns for these features and hopefully they will implement them in their Jenkinsfiles. Alright? For the clever reader, yes, we had to also write these in each repository Jenkinsfile.

### Jenkins Shared Libraries

Updating every repository with these new features implied that we first worked on one repository at a time by modifying the Jenkinsfile by hand and then run the pipeline to see if it worked. Remember, I was very new to Jenkins and the rest of my team was very much understaffed so they were busy gathering requirements and trying to get order out of the chaos.

I started to research Jenkins shared libraries that will allow me to define the common steps and encapsulate them into a single parameterizable abstraction.

We started to replace many stages in our Jenkinsfiles with a single line of code with the new custom steps. This development outcome was that we finally started to remove duplication from our Jenkinsfiles but our pipelines still look very much alike.

During my last two weeks at that company, I started to implement the whole pipeline as a single step. This required to standardize the projects running such pipeline definitions to use the same tooling and define the same build system tasks.

### Testing Steps And Definitions

My next project had Jenkins up and running already and it had a really nice shared library but in hindsight, testing by triggering the pipeline time and time again is not very efficient because you will be waiting a lot of time for the pipeline to reach the steps that you are interested.

What we found is that testing Jenkins shared libraries is a very complex matter because from the beginning Jenkins introduced this feature without any mechanism to test them in isolation. Having to use Groovy is also a challenge as the dynamic nature of the language makes you test double on finger errors such as the number of parameters and their types.

Fortunately, this is not a new problem thus there are projects that ease these steps.

[**jenkinsci/JenkinsPipelineUnit**  
_Framework for unit testing Jenkins pipelines . Contribute to jenkinsci/JenkinsPipelineUnit development by creating an…_github.com](https://github.com/jenkinsci/JenkinsPipelineUnit "https://github.com/jenkinsci/JenkinsPipelineUnit")[](https://github.com/jenkinsci/JenkinsPipelineUnit)

We extensively used jenkinsPipelineUnit to test our workflows and it helped us mainly to avoid regression bugs but testing the integration with external systems (such as SonarQube, Fortify, Terraform, AWS) still was very time-consuming.

### Convention Over Configuration Plus Flexible DSLs

Once I experienced a somewhat mature shared library, I started a new project which required to scale things to a new level as the number of microservices was many times more than I had seen so far. When this situation happens there are always going to be edge cases.

These can be in the form of projects that require to skip steps, projects that require a slightly different task order and various other changes. When you start to see this problem emerging a useful pattern is creating your DSL for pipelines within the Digital Platform of your company.

This means that instead of defining steps with pipeline definitions, you will define a DSL that will be focused on the Platform and following Convention over Configuration to detect the needs of a project.

This is also a highly conceptual task but I can enumerate a few things that we have had implemented:

*   Detect project types and configure the steps that run depending on the type
*   Detect requirements of the project from its structure e.g. if you have a file with a database definition, apply automatically a step to provision it within your orchestrator
*   Inspect for tasks and skip if they are not found, for example, check if there is a Gradle task for checking style and execute it if needed
*   Apply fixes to common mistakes within projects and alert developers early of this problem through notifications. For example, fail/touch files required for the pipeline to run properly like required manifests

All these integrations are very context-dependent thus they will change with your platform. It is important to keep backward compatibility through the support of older models as you evolve the pipeline DSL.

Again, the important part here is that the DSL reflects the standardized way you want application pipelines to behave to support your organization workflow i.e. they become [Delivery Workflow Tools](https://medium.com/@eldermael/digital-platform-accelerators-a897ec4b92f4).