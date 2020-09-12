---
title: Project Kickstarters for Microservices
description: >-
  Previously in my post about Digital Platform Accelerators, I wrote about
  Project Kickstarters. In this post, I will try to get deep into…
date: '2019-08-01T23:53:29.886Z'
categories: []
keywords: []
slug: /@eldermael/project-kickstarters-for-microservices-748780bf6a51
---

![A kick start lever](img/0__GGGNHbCKmYLowqJe.jpg)
A kick start lever

Previously in my post about [Digital Platform Accelerators](https://medium.com/@eldermael/digital-platform-accelerators-a897ec4b92f4?source=post_page---------------------------), I wrote about Project Kickstarters. In this post, I will try to get deep into the patterns I have seen and implemented.

In many companies I have worked we usually implement authentication and authorization, logging, telemetry, etc. I have implemented these in many project templates as a means of showing the capabilities of the platform on which the software runs and the fundamental structures that it provides to layout cross-cutting concerns. The idea behind project kickstarters is that they already give you an implementation of these concerns that is ready to be used and allows developers focusing into implementing business logic.

### Reasoning: Reference Architecture

Many of the problems I have had with Software Architects is that whenever I have worked in a big company with many teams, architecture is usually _retrofitted_ not _implemented_. The proverbial Ivory Tower Architect is one that gets a cross-cutting concern and then thinks of the solution without taking a look at the code that is already implemented. Thus their solutions mechanically clash with the existing interfaces.

Good reference architecture, on the other hand, starts with solutions and research. Proofs of concept are usually a good starting point to generate templates because they are necessarily implementing something that we want to reach. If by some reason we cannot implement a solution to a problem, it means that our architecture is not fitted for our context.

I have also met really good Software Architects and a common pattern I have seen is that they always say “let us prove that this is possible, that we can implement it” on one way or another. Good project templates serve as reference architecture because you can see them deployed and working on a Software Platform, visit their repositories and understand how they integrate to the platform.

### Project Templates

Project templates are not a new concept but most probably they became more necessary with the advent of the microservices architecture. If you have a Digital Platform, good architecture mandates a series of cross-cutting concerns that conceptually can be grounded into templates that should require to do minimal customization to start the development of a new service.

I have seen many patterns for these but the most common is a single git repository in which architects and devs alike pour all the best practices they have learned for development along with sample integrations with technologies within the Digital Platform such as authentication or telemetry. These repositories usually are the product of spikes to know if certain technology can be a good fit for the projects or work that has been done previously.

Nonetheless, project templates are the lowest common denominator to use as Platform Accelerators because they require a lot of customizations to actually become an independent microservice. Cloning a project and do a lot of renaming is probably an error-prone task as the smart reader will notice.

### Project Generators

Once you have achieved enough maturity regarding project templates, the next logical step is to create tooling that uses these templates and produces ready-to-use projects.

The focus of this post is to talk about them in the context of Digital Platforms so tools like Micronaut or Gradle initializers are not going to be described because, as far as I know, they do not allow you to customize the projects they already produce with features specific to your context.

Tooling available to create project generators is varied. I have used mostly Yeoman and Atomist. But there is also Maven Archetypes and Micronaut `mn` utility, Gradle `init` subcommand, etc. Because the focus of this article goes along the lines of Digital Platforms, tools that do not provide a way to integrate platform-specific features are not discussed e.g. Micronaut `mn.`

#### Yeoman

Yeoman is a project scaffolding tool similar to Maven archetypes or Rust Cargo. In principle Yeoman is really easy to use as it works with templates and an “in memory” file system that allows you to stream files from a predefined location and apply transformations to them.

Whatever you can do with memory-fs editors you can do with all the files using Yeoman. I have also used sub-generators as feature toggles to allow generation of code with specific features on them.

The drawback of using templates is that you will not have a good feedback cycle unless you generate a project from scratch and then run the generated project and hopefully run a good test suite contained within the project. For example, if Yeoman generates a front end application you will want yo run `npm run build`or if you are generating a Gradle project then running `./gradlew build`. These will allow you to know if your code compiles and their tests are running fine with the set of features you want. All of this takes time so I would not recommend templating files at all.

What has worked best for me is to download a repository into the directory where Yeoman is expecting the template files to be and then do the replacing and renaming. This ensures that at least the starting point of your code generation is a project that hopefully is already in a good state (by having this project have a pipeline and a battery of tests that actually work).

The following problem here is making sure that the generated project is not in a bad state and soon enough you will have to have a pipeline that generates and discards projects after running tests on them.

Finally, the tools Yeoman gives you are very basic. String replacing, file renaming and so forth are the bare minimum for project generators and soon enough I had found a lot of complexity while trying to make more sophisticated things such as properly remove/add features to a project depending on the user needs. You could theoretically create projects that have only the features some devs will need but this becomes a complex problem due to the number of permutations that happens with these projects.

#### Atomist

Atomist approach to code generation takes the idea of independent seed projects that you take and apply code transformations to them. This is no templating mechanism so Atomist proposes using Microgrammars and AST transformations to automate the changes to the project.

While I agree that you could use other AST transformations using Yeoman directly using Vynil streams ASTs, I do think that the API Atomist provides, along Microgrammars are more simple and powerful to use as they provide really good abstractions over code projects and code transformations.

Using a Software Delivery Machine, you can use Git repositories as the starting point for a new project. By applying code transformations to the source code, you will produce a fresh project. The SDM will orchestrate the transformations and produce a new Git repository and also can push it to a service such as Github or Bitbucket ready to be used.

In a later post, I will discuss approaches to code project generators and probably code examples to create feature toggles using them.