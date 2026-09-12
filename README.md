# Operational Contract

> **DevOps should not have to reverse-engineer the operational requirements of an application.**

An Operational Contract is a simple, structured document that describes the information Development, DevOps, and SRE teams need to deploy, operate, monitor, troubleshoot, and maintain an application in production.

This project provides a practical template and a simple example to help teams document operational requirements close to the application’s source code.

The goal is not to introduce another complex process or replace Platform Engineering. It is to reduce operational ambiguity, improve collaboration between teams, and create a foundation for safer and more predictable production operations.

## Why This Project Exists

Imagine a new Microservice is ready to be deployed.

The development team hands the Repository to the DevOps team and says:

> **"The service is ready to deploy."**

You open the Repository.

There is a README.

It is actually a good README.

It explains what the Application does, how to run it locally, how to install dependencies, how to run tests, and maybe even how to build the Docker image.

Everything looks fine.

**Until you actually have to deploy it to Production.**

Then the questions start:

* Which port does the service listen on?
* What are the Health Check and Readiness Check endpoints?
* How long does the Application usually take to start?
* Which Environment Variables are required?
* Which configurations are Secrets?
* What services does it depend on?
* Which dependencies are required for the service to start?
* What happens if one of those dependencies becomes unavailable?
* Can the service safely run with multiple replicas?
* How much CPU and Memory does it need?
* Does it support Graceful Shutdown?
* Does it run Database Migrations?
* Is it safe to Rollback?
* Which Metrics should be monitored?
* Where should we start when there is an Incident?

A simple Deployment can quickly turn into a back-and-forth process:

```text
DevOps: Which port does this service use?
Developer: 8080.

DevOps: Is Redis required?
Developer: No, it's only used for cache.

DevOps: What happens if Kafka is unavailable?
Developer: It should retry.

DevOps: How many replicas can we run?
Developer: I think it's fine.

DevOps: Does it run migrations on startup?
        Is rollback safe?
Developer: Let me check...
```

What should have been a normal Deployment becomes a series of messages, Tickets, meetings, and sometimes multiple Deployments and fixes.

---

## The Problem Isn't the README

In many cases, **the README isn't actually bad.**

It was simply written for a different audience.

A Developer usually wants to know:

> **"How do I run and develop this Application?"**

But the DevOps/SRE team has a different question:

> **"How do I safely run and maintain this Application in Production?"**

These questions are related, but they are not the same.

Kubernetes can deploy a Container, but it doesn't know whether the Application can safely scale.

We can define a Readiness Probe, but Kubernetes doesn't know when that endpoint actually means the Application is ready.

We can configure Kubernetes to restart a Container, but it doesn't know whether restarting the Application during a Database Migration is safe.

That information has to come from somewhere.

When it isn't documented, it usually comes through **back-and-forth communication between teams.**

---

## The Problem Gets Bigger as the Number of Services Grows

For one Microservice, these conversations may not seem like a big deal.

But when you have dozens or hundreds of Microservices and multiple Development teams, these small questions become a **constant operational cost**.

Every missing piece of information becomes another question.

Every question creates a dependency on someone who knows the answer.

And if that person is not available, the Deployment may stop.

Over time, operational knowledge moves away from the Repository and ends up in:

**messages, Tickets, meetings, and people's heads.**

This project is an attempt to reduce that friction.

---

## The Idea: Operational Contract

If another team is responsible for Deploying and Maintaining your Application, they should be able to answer the main operational questions **before the Deployment starts.**

That led to a simple idea:

> **Every Application should have clear operational requirements alongside its development documentation.**

This project calls that an **Operational Contract**.

An Operational Contract is a structured way to document the information the team responsible for Production needs to:

* Deploy
* Operate
* Monitor
* Troubleshoot
* Maintain

the service.

The goal is not to add another layer of bureaucracy.

The goal is to take information that may currently live in a Developer's head, messages, or Tickets and keep it, as much as possible, **close to the Application and inside the Repository.**

---

## Why Keep It Close to the Application?

Applications change, and their operational requirements can change with them.

For example, imagine Redis is initially used only as an optional Cache.

A few months later, it becomes a required dependency for the Application to start.

If this change is only documented in someone's memory or in a separate Wiki, it is easy for the documentation and the actual behavior of the Application to drift apart.

But if the Operational Contract lives in the Repository, the Application change and the documentation change can happen in the same Pull Request.

This makes operational documentation part of the Application's change lifecycle, just like Code.

---

## Does This Mean the README Has to Become Huge?

No.

The goal is **not** to turn the README into a 30-page document.

Not every service needs every section.

A simple internal service may only need a small part of the Template, while a Critical Production service may need much more detail.

The Template should therefore be **customized based on the service's complexity, architecture, and criticality.**

The goal is not to document everything.

The goal is to make sure that **important information required to run the service in Production is not something people have to guess.**

---

## What Does the Template Cover?

The Operational Contract Template covers the main operational areas of a Microservice:

1. **Service Overview**
2. **Build & Runtime**
3. **Ports & Protocols**
4. **Ingress / External Access**
5. **Dependencies**
6. **Configuration & Environment Variables**
7. **ConfigMaps & Volumes**
8. **Secrets Management**
9. **Testing**
10. **Observability**
11. **Resource Requirements & Scaling**
12. **Scheduling**
13. **Security & Compliance**
14. **Deployment Notes**
15. **Incident Response Notes**
16. **Contact & On-Call**
17. **Additional Notes**

Not every service needs every section.

Use what is relevant and remove what isn't.

---

## This Doesn't Replace Platform Engineering

**The Operational Contract is not the final solution.**

In a mature organization, many of these problems should be solved through **Platform Engineering and a Self-Service Platform**.

A Platform can provide standard ways to:

* Deploy services
* Configure Observability
* Manage Secrets
* Scale workloads
* Apply Security Policies
* Provide operational tooling

But not every organization has such a Platform today.

Until we get there, we still need to Deploy and Operate Applications.

The Operational Contract is therefore a **small step toward reducing operational friction and unnecessary back-and-forth while moving toward a real Platform.**

---

## Files

This repository intentionally keeps things simple:

```text
.
├── README.md
├── operational-contract-template.md
└── platform-engineering.yml
```

### `operational-contract-template.md`

The actual template that can be copied into an Application Repository and customized based on its operational requirements.


### `platform-engineering.yml`

A short discussion about how the Operational Contract relates to Platform Engineering and how this idea could evolve toward more automated and self-service workflows.

---

## How to Use

Use the template as a starting point for defining your application's operational requirements.

Remove sections that are not relevant and fill in the information another team would need to safely deploy and operate the application.

The template is intentionally opinionated but **not a universal standard**. Adapt it to your organization's:

* Architecture
* Infrastructure
* Tooling
* Security requirements
* Deployment process
* Service criticality


---

## The Goal

The goal is simple:

> **Before someone deploys your Application, they should know what they need to know to operate it safely.**

Less guessing.

Less back-and-forth.

Less operational knowledge trapped in people's heads.

More information close to the Application.

---

## Contributing

This is a starting point, not a finished standard.

If you have experienced similar problems in a DevOps, SRE, or Platform Engineering team, contributions and feedback are welcome.

Ideas, improvements, missing operational requirements, and real-world use cases are especially valuable.

---

