# Architectures

## DoD/IC Ontology Working Group - Operationalizing Ontologies Community of Interest

**Contributors:** Paul Kogut, Don Pellegrino, Jonathan Vajda, John Beverley, Joe Blankenship, Eric Peterson, Tim Toohill, Jennifer DeCamp, Ali Hasanzedah, John Judkins, Amanda Mitchell

## Introduction

The goal of the Operationalizing Ontologies Community of Interest (OO-COI) is to provide guidance on how to apply ontologies in DoD/IC operational systems (e.g., C2, ISR, mission planning, equipment maintenance, logistics) and internal business systems. Current guidance is scattered across many sources and has significant gaps. The intended audience is both non-technical mission-focused personnel and very technical developers. Education of project managers, software architects, and junior software developers is a major barrier to fully leveraging the benefits of ontologies. The OO-COI will help DoD/IC personnel identify opportunities to insert ontologies into current and future systems.

This document provides advice on OWL ecosystem tools, architectures, and applied automated reasoning tools. The figure below shows typical generic components in an ontology-based architecture along with examples of tools and frameworks that can instantiate those components. The knowledge graph component is sometimes called an RDF triple store. The commercial world of ontology tools and applications is rapidly evolving (see [knowledgegraph.tech](https://www.knowledgegraph.tech/)).

![OWL Ecosystem](https://github.com/johnbeve/operationalizing-coi/blob/main/docs/assets/owl-ecosystem.png)

> [!NOTE]
> This document assumes use of DoD/IC Foundry-compliant semantic infrastructure that includes OWL 2, RDF, and SPARQL (see Guidance for Ontology-based Systems Development).

This section describes languages and tools that may be used in conjunction with OWL, RDF, and SPARQL to build an application.

## Integrating OWL, RDF, and SPARQL in a Modern Microservice Architecture

Microservices architectures are the latest attempt to build flexible systems and reusable code. There is no formal widely accepted definition of microservices architectures but they generally have these characteristics:

- Loosely coupled and fine-grained services with minimized dependencies
- Services have well-defined “public” APIs
- The architecture is designed to accommodate services implemented in multiple programming languages and services that use different data stores
- Emphasis on independent deployment with containers
- Associated with cloud architectures and DevOps processes
- Microservices can be combined into composite services

The goals of microservice architectures and OWL ecosystems are not fundamentally incompatible. Interoperability is central to both. They diverge in their implementations of semantics. Technology often used in microservices architectures includes:
- **JSON**: Used for serializing and transmitting structured data between microservices. JSON is primarily syntax. JSON schema adds some semantics similar to XML schema.
- **JSON LD**: An extension of JSON to add semantics similar to RDF. This is a promising bridge between microservices and OWL ecosystems.
- **REST**: Widely used service-oriented architecture protocol that usually transmits data as JSON or XML.
- **OpenAPI**: Defines REST APIs and is a standard programming language-agnostic interface description for HTTP APIs, allowing both humans and computers to discover and understand the capabilities of a service without requiring access to source code.
- **gRPC**: A more recent service-oriented architecture protocol that transmits data as serialized binary. Uses protocol buffers to define contracts with datatypes.
- **Docker**: Used to define containers for microservices.
- **Kubernetes**: Used to execute and monitor containers such as Docker. Helm charts allow you to configure Kubernetes.
- **ActiveMQ**: Supports both point-to-point and publish/subscribe messaging. In microservices architectures, publish/subscribe messaging is often used for asynchronous communication. Producer services define topics and consumer services listen to topics.

The microservice architecture technologies described above create a major barrier to the adoption of OWL, RDF, and SPARQL-based architectures that support formal semantics and automated reasoning. It is difficult to explain why the OWL ecosystem should be used instead of JSON. If you have the luxury of building a set of microservices from scratch, then an OWL ecosystem like that shown in the diagram above is highly recommended. The major challenge comes when there are existing services and applications that are not ontology-based. In this case, you need to resort to custom translators.

_Note: This is a complex subject and there is no widely accepted solution yet. The W3C is working on this topic (see: [W3C JSON-LD Best Practices](https://w3c.github.io/json-ld-bp/))._

## Generic Architectures for Ontology Applications (ERIC P)

The diagram below shows a generic OWL application architecture. Applications like those listed in the sections above can query a knowledge graph. Preexisting services or systems A and B can interoperate via a shared ontology that contains mappings between classes and properties.

![Architecture 1](https://github.com/johnbeve/operationalizing-coi/blob/main/docs/assets/generic-arch-1.png)

The diagram below shows a generic OWL backend architecture. Structured and unstructured text data can be ingested into the knowledge graph to support queries of heterogeneous sources.

![Architecture 2](https://github.com/johnbeve/operationalizing-coi/blob/main/docs/assets/generic-arch-2.png)