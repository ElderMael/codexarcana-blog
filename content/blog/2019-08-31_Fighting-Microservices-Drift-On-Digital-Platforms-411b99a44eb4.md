---
title: Fighting Microservices Drift On Digital Platforms
description: >-
  Previously in my post about Digital Platform Accelerators, I wrote about
  Distributed Refactoring Tools. In this post, I will try to…
date: '2019-08-31T16:16:11.458Z'
categories: []
keywords: []
slug: /@eldermael/fighting-microservices-drift-on-digital-platforms-411b99a44eb4
---

Previously in my post about [Digital Platform Accelerators](https://medium.com/@eldermael/digital-platform-accelerators-a897ec4b92f4?source=post_page---------------------------), I wrote about Distributed Refactoring Tools. In this post, I will try to describe the different tools I have used and the circumstances that lead me to use them. Also, why they are necessary.

I have worked on four microservice projects on different roles. From front-end and backend developer, tester, infrastructure developer, and a mix of all of them. While I worked on three different companies during those projects, I almost always found the same problems appearing.

The need to share code between services using platform libraries and the consequent maintenance that comes with them. The need to create policy through pipelines that evolve constantly and end up breaking project builds due to backward-incompatible changes. And finally, the need to update configurations for both pipelines and microlibs on several projects at a time.

In hindsight, all these problems mostly come from the same source: **drift**. Be it _configuration drift_ due to a myriad of properties files or configuration sources; dependency hell due to _library version drift;_ or _delivery drift_ caused by feature parity between projects and the pipelines required to deliver them.

![Driftwood, Wikimedia Commons.](img/0__aAeyMEubOi__AHcDF.jpg)
Driftwood, Wikimedia Commons.

### Why Does This Kind Of Drift Happen?

It’s because _you share code and settings_. Configuration drift happens when you have different settings or initialization data for your services or infrastructure. Dependency drift evolves to dependency hell when you have different versions of the same library and you share those versions on other software projects. Finally, delivery drift happens when your services cannot be delivered with the same pipeline definition over time.

The organic nature of software is what is causing drift. At some point, we have created strategies for conveying meaning on change e.g. versioning and more specifically semantic versioning. With these versions, the goal is to keep up to date with the latest release because it should be the most stable or has the latest features that help us evolve our platform.

The problem with semantic versioning is very misleading regarding two things: it’s not always the most stable and in most programming languages there is no way to enforce it. Even Joe Armstrong, of Erlang fame, tried to find ways to enforce that even a function was exactly the same as other function to enforce compatibility.

The latest release of a library is not always the most stable due to the nature of modifying software itself. Regressions happen, not breaking compatibility with previous releases is a goal but there are no guarantees.

What I think is that semantic version, even if well-intentioned, is not sufficient if you want to avoid drift on your dependencies or configuration. The smart reader has probably also thought about dependency locking. Some tools have already integrated this feature so that every time you build a software project it will always resolve the same dependencies. The problem with version locking is that it poses the problem of maintenance.

Version locking and the organic nature of software conflict with each other. If you lock dependencies, sooner or later you need to upgrade them or they will become obsolete. It’s on your best interest to not be out of date with security patches and bug fixes.

### Distributed Refactoring As Means To Ease Drift

Unless you are on a monorepo (which has different challenges, out of the scope of this post), there are many constraints to evolve your software and keep up to date in a Microservices architecture.

The first problem with Microservices is that, unlike the monolith, you need to have platform libraries. The share-nothing approach could be useful but leads to a lot of duplicated efforts and even more drift because everyone will be tempted to solve the same problems with different strategies.

Platform libraries are implementations of cross-cutting concerns at a platform level. With a monolith, AOP used to be the way to achieve this, but you cannot intercept microservice calls without adding more overhead between services. Examples of this are authentication implementations, logging, monitoring, telemetry, etc. Even the pipeline definitions of build servers such as Jenkins are a way of policy enforcing and they require updates.

Now that you have implemented cross-cutting concerns using those libraries, keeping them up to date will be the next challenge. This is where distributed refactoring comes into play.

If you are into a monorepo, refactoring can be a single commit and it’s atomic. Updating libraries in different repositories will not be atomic and it will be difficult to do by hand if you have more than a few microservices to update. Even if updating different repositories is not atomic, automating these updates as much as possible will save a lot of developer hours.

I remember working on a single pipeline to deploy only a certain type of microservices. Every time I had to add a feature, it required modifying at least a dozen of services of that type. That could take anything from a couple of hours to an entire day depending on the definition and the size of the change. Even with shared pipeline libraries, updating the versions used is still a task that requires effort per microservice.

### The Tools I Have Used To Execute Distributed Refactoring

#### Atomist

I have used Atomist at very early stages in my second microservices project. At that time I worked as a tester and we needed to use clients for a huge amount of SOAP services that provided auto-generated code.

Unfortunately, while we could generate code from those services because I was working as a tester, I knew that the service contract was going to change eventually and I did not want to create builders by hand for the myriad of objects that represented the response and request for those services.

Then I found Atomist and I found that I could create software that transforms software, I created a small program that added the required annotations to the generated code.

While this approach helped me a lot, on the way I discovered many other features that Atomist has that have helped me resolve all the problems that I have faced always during the development of microservices.

Atomist fingerprints allow you to keep track of the different versions of the platform libraries being used and with this drive updates. Configuration drift can also be tracked with Atomist. But Atomist goes beyond just tracking, you can create Code Transformations to keep projects from drifting if required with pull requests that developers can accept when ready (or just apply them if you feel empowered to do the change yourself).

Generating pull requests to update libraries using microgrammars to look for specific parts of Gradle build files or NPM package.json files is possible and is very simple to do.

Delivery drift can also be tackled by having Atomist fix/add step definitions and Jenkins pipeline versions to keep projects up to date with the latest policy in your platform.

[**What’s Lurking in your Repositories? | Atomist Blog**  
_The monolith is crumbling. Most organizations are moving from a small number of large applications to a large number of…_blog.atomist.com](https://blog.atomist.com/whats-lurking/ "https://blog.atomist.com/whats-lurking/")[](https://blog.atomist.com/whats-lurking/)

Finally, I have been experimenting on creating backward compatibility with project kickstarters by annotating new platform features and make Atomist copy such features from seed/reference architecture projects.

This is important because project kickstarters and reference architecture start to drift the moment that you used them to start a new microservice. If users want to use new platform features, in most of the projects we have to do this manually with migration guides and manual steps. If you can automate adding new features, for example, the use of a secret registry such as Hashicorp Vault, you could save a lot of developer hours invested into integrating that feature from reference architecture services.

[**ElderMael/zwitch-sdm**  
_An Atomist software delivery machine (SDM) that clones projects and deletes/adds features to them based on parameters…_github.com](https://github.com/ElderMael/zwitch-sdm "https://github.com/ElderMael/zwitch-sdm")[](https://github.com/ElderMael/zwitch-sdm)

#### Snyk

[**Open Source Security Platform | Snyk**  
_Enabling more than 300,000 developers to automatically find and fix open source vulnerabilities. Giving developers a…_snyk.io](https://snyk.io/ "https://snyk.io/")[](https://snyk.io/)

I have been in only one project where they used Snyk and it solves the problem of dependency version drift but with an approach focused on security. I really do not have much experience using the tool but I can vouch that it helped many other developers to keep dependencies up to date when critical security issues arrive.

Just recently we have had a huge amount of pipelines failing due to security scans made by OWASP and keeping the relevant libraries can consume a lot of time. While most of the time we need to ignore the problem because even the newest version does not resolve it, Snyk is capable of fixing them automatically with patches later on.

#### rewrite

[**Netflix-Skunkworks/rewrite**  
_The Rewrite project is a refactoring tool for Java source code. It contains a custom Abstract Syntax Tree (AST)…_github.com](https://github.com/Netflix-Skunkworks/rewrite "https://github.com/Netflix-Skunkworks/rewrite")[](https://github.com/Netflix-Skunkworks/rewrite)

I became aware of rewrite only a few days ago and it looks very powerful. But it only works on Java projects. Its API looks fantastic for distributed refactoring and I have seen presentations were it could refactor all the Guava references of a method on GitHub!

I am researching this project for future use as one of my current project goals is to provide compatibility with other projects thus I can see the potential of rewrite to refactor calls to microlibraries we use to provide platform features.

Jon Schneider uses rewrite to refactor some Guava calls on all of GitHub!

### Conclusion

Fighting microservices drift is a daunting task and while I have seen and implemented various approaches to this and it is still very difficult. I believe that keeping team independence is great, automated refactoring possibly could be better.

I remember in the first project I had to go and review all the front-end code of various codebases and create comments for developers to update their dependencies to introduce some features dictated by the platform. My surprise is that while some teams fixed the issue right away, others did not. In this case, I lacked the authority to enforce or apply the changes myself so that went on for a while until things started to fail.

In further projects, I had more power to do this but I still find that going to each repository and apply the fixes by hand is very error-prone and this is not the ideal scenario because drift happens in many places at a time and all of a sudden. That moment was when I started to look for tools that allowed me to refactor code automatically or allow me to speed the process.

My point is that even if you could keep things up to date for a while yourself, the scale of a microservice architecture will reach such a mass that doing things automatically is a better alternative than putting the effort to do it and feel the pain.