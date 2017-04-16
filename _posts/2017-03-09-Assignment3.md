---
layout: post
title: "Two Phase Commit Explained"
categories: journal
tags: [documentation,sample]
---
As a part of Transaction Management in Microservices, we were interested to venture into the topic of Two Phase Commit. I worked along with Thanmai and Supreeth.

## Architecture:
Consider the same architecture as that of the Event-driven approach. We have an Order Service and a Customer Service with their respective databases. But instead of the Message Broker to communicate the events between the two services, we will talk about the Two-phase commit approach.

***

## Mechanism:
![two-phase-commit](http://www.yusufaytas.com/wp-content/uploads/2012/10/2PhaseCommit.png)

***

## Problem Statement:
In microservices architecture, each microservice has its own private datastore. Different microservices might use different SQL and NoSQL databases. While this database architecture has significant benefits, it creates some distributed data management challenges. The challenge of decentralized data management is how to implement business transactions that maintain eventual consistency.

***

## Possible Solutions:

Method | Source
------- | -------
Event-driven Architecture | [EDA](https://en.wikipedia.org/wiki/Event-driven_architecture)
Two-phase Commit Protocol | [2PC Protocol](https://en.wikipedia.org/wiki/Two-phase_commit_protocol)

***

## Solution Evaluation:
Any transaction made has to go through a transaction manager. This manager ensures that a transaction occurs across all the services (resources). As the name suggests, there are two phases in this mechanism - Commit Request Phase and Commit Phase.

1. Commit request phase (also known as voting phase): The manager sends a _query to commit_ message to all the services. The manager then waits for all the services to vote yes or no. Each of the services will perform the transaction up to the point where they would have to commit. The services reply with _yes_ or an agreement if all they are prepared or _no_ if even if one of the services is not prepared.

2. Commit phase (also knows as completion phase): There can be two conditions here. Either the manager received _yes_ from all the services or at least one of the services voted _no_. 

  * Manager received _yes_ from all services: The manager sends a commit message to all the services asking them to commit the transaction. After the commit, the services send an acknowledgement to the manager after which the transaction is complete.

  * Manager received _no_ from one or more of the services: The manager sends a rollback message to all the services asking them to rollback to the state before the actions from the previous phase. After the rollback, the services send an acknowledgement to the manager after which the transaction is undone.

***

## Conclusion:

### Advantages:
- In an environment which has many databases that get affected. It is good to treat them as transactions. Global transactions span on one or more transactional resources, and enlist them all in a single transaction. 
- Prepare phase can be considered as a dry-run phase to check if the commit is allowed by all the components involved in the system.

### Disadvantages:
- The transaction manager is a single point of failure. If it fails, then the services will never be able to resolve their transactions.
- This protocol is a blocking protocol. The manager will block till it receives the messages from the services which would imply that the locks and resources held by it will not be released till it receives a reply.
- If any of the services vetoes the commit, then all the services are asked to perform a rollback on their databases. This ensures consistency among partitions. But being a blocking protocol, this mechanism does not ensure good availability. 

### CAP Theorem:
We know that web services cannot ensure - _consistency_, _availability_ and _partition tolerance_. They can, at most, support only two out of the three. ACID, as we know, provides consistency for partitioned databases. If we have to achieve availability instead, we can think of BASE (basically available, soft state, eventually consistent). This basically argues that it is better to have availability along with eventual consistency rather than compromising on availability on the whole. As previously discussed, we can implement an _event driven architecture_ to fulfill this purpose.

***

## Implementations and Examples:
- Atomikos:  [Link](https://www.atomikos.com)
- Bitronix:  [Link](https://github.com/bitronix/btm)
- JTA Standalone Transaction Manager: [Link](http://simplejta.sourceforge.net)

***

## Associated Github issues:
- [2 Phase Commit Implementation using Microservice data management #2](https://github.com/airavata-courses/spring17-microservice-data-management/issues/2)

***

## Other References:
- [Configuring Spring and JTA without full java IDE](https://spring.io/blog/2011/08/15/configuring-spring-and-jta-without-full-java-ee/)
- [Base: An Acid Alternative](http://queue.acm.org/detail.cfm?id=1394128)
- [Transaction Managers](http://dorel.vaida.co/2006/10/open-source-jta-transaction-managers.html)