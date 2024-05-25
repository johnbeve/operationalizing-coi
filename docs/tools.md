# Tools

## DoD/IC Ontology Working Group
### Operationalizing Ontologies Community of Interest

**Contributors:** Paul Kogut, Don Pellegrino, Jonathan Vaidja, John Beverley, Joe Blankenship, Eric Peterson, Tim Toohill, Jennifer DeCamp, Ali Hasanzedah, John Judkins, Amanda Mitchell

## Introduction
The goal of the Operationalizing Ontologies COI is to provide guidance on how to apply ontologies in DoD/IC operational systems (e.g., C2, ISR, mission planning, equipment maintenance, logistics) and internal business systems. Current guidance is scattered across many sources and has significant gaps. The intended audience is both non-technical mission-focused personnel and very technical developers. Education of project managers, software architects, and junior software developers is a major barrier to fully leveraging the benefits of ontologies. This document will help DoD/IC software engineers get started in developing applications that leverage ontologies. See the Ontology Applications Patterns document for help in identifying opportunities to insert ontologies into current and future systems.

This document provides advice on OWL ecosystem tools, architectures, and applied automated reasoning tools. The figure below shows typical generic components in an ontology-based architecture along with examples of tools and frameworks that can instantiate those components. The knowledge graph component is sometimes called an RDF triple store. The commercial world of ontology tools and applications is rapidly evolving (see [knowledgegraph.tech](https://www.knowledgegraph.tech/)).

![OWL Ecosystem](https://github.com/johnbeve/operationalizing-coi/blob/main/docs/assets/owl-ecosystem.png)

## Related Technologies
This section describes languages and tools that may be used in conjunction with OWL, RDF, and SPARQL to build an application.

### Integrating OWL, RDF, and SPARQL in a Modern Microservice Architecture
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

## OWL Deductive Reasoning (JOHN B & JON V)
Reasoning is used to answer SPARQL queries and check the logical consistency of ontologies. Note that satisfying a SPARQL query is a kind of inference and so the totality of inference capabilities is what the reasoner can do plus what SPARQL can do. OWL 2 profiles are designed to accommodate a variety of reasoning capabilities. The choice of the appropriate OWL 2 profile depends on the size of the data and the type of reasoning required for an application. Profiles trade off expressivity in exchange for performance or ability to implement using a particular technology (e.g., business rule engines vs. databases).

There are four OWL 2 profiles:
- **OWL Full**
- **OWL EL**
- **OWL RL**
- **OWL QL**

OWL Full is the most expressive profile. However, OWL Full reasoning might run forever in some cases (it is undecidable). EL, RL, and QL leave out specific OWL expressions that impact reasoning performance and decidability. For example, queries that involve sameAs expressions on individuals are notoriously computationally intensive. OWL EL is less expressive and suitable for fast reasoning on ontologies that obey its restrictions. EL is useful for checking/validating complex ontologies but is not as useful for querying with instance data. OWL RL is designed to be implementable using rule systems and is quite powerful. OWL RL is a good default profile for many applications. OWL QL is designed to be implemented in SQL and is useful for querying with large amounts of data. It is not uncommon to reason using OWL Full on the ontology, augmenting the ontology with those inferences before loading the combination into a triple store, and then using a less powerful profile to deploy for querying instance data.

To select an appropriate profile, you can develop a set of “competency questions” that determine the kinds of inference that a specific application needs. Then map those competency questions to OWL expressions in profiles to select the appropriate profile.

_Note: Do we need a tutorial on reasoning? Is there a good one out there that we can point to? This section also needs more explanation of checking the logical consistency of ontologies and advice on the specific reasoners that are available such as Pellet, Hermit, and ELK._

### Rules
The tightly integrated combination of ontologies and rules is a powerful AI capability with wide applicability. For example, ontologies and rules are being used by BMW for automated reasoning in autonomous cars ([Reasonable Vehicles Rule the Road](https://www.oxfordsemantic.tech/blog/reasonable-vehicles-rule-the-road)). The Semantic Web Rule Language (SWRL) provides if-then rules on top of OWL (see [SWRL Tutorial](https://www.michaeldebellis.com/post/swrl_tutorial) and [OWLReady2 Rules](https://owlready2.readthedocs.io/en/v0.37/rule.html)). More human-readable forms of rules are also available (see [Stardog User-Defined Rules](https://docs.stardog.com/inference-engine/user-defined-rules)). Rules can also be embedded in SPARQL construct statements.

### SHACL (JON V)
The Shapes Constraint Language (SHACL) is a way to check the quality of your RDF data (see [SHACL](https://www.w3.org/TR/shacl/) and [TopQuadrant SHACL Tutorial](https://archive.topquadrant.com/technology/shacl/tutorial/)). This is important for applications with large-scale or messy data.

_Note: Need more explanation of SHACL._

### Labeled Property Graphs (JOE B)
Labeled Property Graphs (LPG) are a form of graph database that was designed for highly efficient queries and visualizations of data (see [RDF Triple Store vs. Labeled Property Graph](https://neo4j.com/blog/rdf-triple-store-vs-labeled-property-graph-difference/)) and not semantic interoperability and automated reasoning. The debate about LPG vs. RDF continues but tools are evolving to handle both simultaneously. OWL ontologies can be automatically converted to LPG with some loss of semantics which may or may not impact your application. Query languages for LPGs such as Gremlin and openCypher are more focused on graph traversal rather than OWL-like semantics and they are not formal standards like SPARQL. LPG ecosystems like neo4j are actually complementary to OWL ecosystems. A user wants direct logically generated answers (OWL) as well as the ability to explore information in graphs (LPG).

### Natural Language Processing
The parsing of unstructured data including natural language documents and human-to-human or human-to-machine conversations into RDF which is semantically linked to ontologies is a major advantage of the OWL ecosystem. Processing natural language with high precision and recall is challenging. A variety of NLP tools exist. All require significant machine learning training or knowledge engineering for most specialized DoD/IC domains.

_Note: Need to explain the relation to ChatGPT and Large Language Models._

### Relational Database to RDF Mapping Language
R2RML is a language for expressing mappings from relational databases to RDF datasets. See [R2RML](https://www.w3.org/TR/r2rml/).

## List of Languages
Items such as SKOS, DC.

## List of Tools and Frameworks
The tools below are roughly grouped by type (e.g., ontology development environment, knowledge graph, reasoning) but some tools cover multiple functions. Like in many software and AI technology areas, there is a continuous debate about the advantages and disadvantages of open-source software vs. commercial products. In the OWL ecosystem, commercial products are in general ahead of open-source frameworks especially in the category of knowledge graph and reasoning tools. Even the widely accepted and used Protégé is being left behind. The DoD/IC should carefully consider whether or not they should select a designated set of tools or build their own set of tools because commercial products are advancing rapidly. It is probably best to adhere to OWL, RDF, and SPARQL standards and swap in new tools as they become available.

### Agent Tool (DOD/IC Ontology Foundry and Johns Hopkins Applied Physics Lab)
Agent Tool provides a way to search a curated library of ontologies. It also provides tools for checking ontologies for compliance to documentation standards and eventually semantic consistency with reasoners.

### Ontology Development Environments
- **Protégé**: A widely used open-source ontology development environment. For a recent tutorial see [Protégé Pizza Tutorial](https://www.michaeldebellis.com/post/new-protege-pizza-tutorial). For installation instructions see [Protégé Wiki](https://protegewiki.stanford.edu/wiki/Main_Page).
- **WebProtege**: An open-source collaborative ontology development environment. A public version is hosted by Stanford. See: [WebProtege](https://webprotege.stanford.edu/). It can also be installed on premises.
- **Mobi**: A free collaborative ontology editor with many advanced features including support for SHACL. See: [Mobi](https://mobi.inovexcorp.com/).
- **TopBraid Composer**: A mature commercial ontology development environment with many advanced features. See: [TopBraid Composer](https://www.topquadrant.com/products/topbraid-composer/).
- **ROBOT**: A Java-based collection of utility functions that can be used to develop and maintain ontologies such as extract, merge, filter, and logical validation. These utilities can be composed into a workflow. See: [ROBOT](http://robot.obolibrary.org/).

### Knowledge Graphs and Reasoning Tools
Triple Stores for knowledge graphs are being scaled up to handle large amounts of data and do practical automated reasoning. See [Large Triple Stores](https://www.w3.org/wiki/LargeTripleStores).
- **Stardog**: A mature commercial knowledge graph infrastructure including a scalable RDF triple store, a state-of-the-art OWL reasoner, and a virtual graph capability that allows access to data sources without ingesting them. Stardog has a user-friendly SPARQL-based rules syntax and also supports SWRL. For tutorial and documentation see: [Stardog](https://www.stardog.com/learn-stardog/). Pystardog is a python wrapper for Stardog. See: [Pystardog](https://github.com/stardog-union/pystardog).
- **Cambridge Semantics Anzo**: A scalable knowledge graph platform with end-to-end pipeline support for structured and unstructured data. Anzo greatly facilitates adoption for novice users of knowledge graphs. See: [Cambridge Semantics Anzo](https://cambridgesemantics.com/).
- **Oxford Semantic Technologies RDFox**: A scalable knowledge graph platform designed with an emphasis on efficient reasoning. RDFox enables intelligent information processing by representing and reasoning with domain knowledge in the form of rules and ontological axioms. RDFox is geared towards expert users. See: [Oxford Semantic Technologies](https://www.oxfordsemantic.tech/).
- **OWLReady2**: An open-source OWL framework. See the book “Ontologies with Python: Programming OWL 2.0 Ontologies with Python and Owlready2”. OWLReady2 uses an rdf/xml syntax and SWRL rules. See: [OWLReady2](https://github.com/pwin/owlready2).
- **Apache Jena**: An open-source Java framework for building semantic web applications. See: [Apache Jena](https://jena.apache.org/getting_started/index.html). Jena includes a query engine for SPARQL called ARQ.
- **RDFLib**: A widely used Python utility package. See: [RDFLib](https://github.com/RDFLib/rdflib). RDFLib can be used to ingest a variety of sources (e.g., SQL databases, MongoDB, CSV files, NLP parser output) into RDF for input into knowledge graphs.
- **Ontop**: Uses R2RML to virtually query relational databases. The data remains in the database and does not get converted into RDF. See: [Ontop](https://ontop-vkg.org/).
- **Amazon Neptune**: Supports both RDF and LPGs. See: [Amazon Neptune](https://aws.amazon.com/neptune/).
- **Ontotext GraphDB**: See: [Ontotext GraphDB](https://www.ontotext.com/products/graphdb/). **(ALI)**
- **Franz AllegroGraph**: See: [Franz AllegroGraph](https://allegrograph.com/).
- **PoolParty**: See: [PoolParty](https://www.poolparty.biz/).

### NLP Tools
- **spaCy and Prodigy**: Prodigy is used to label training data and spaCy learns to parse sentences based on that training data. These are widely used tools. See: [spaCy](https://spacy.io/) and [Prodigy](https://prodi.gy/).
- **Lymba**: A commercial tool that uses hybrid machine learning and semantic knowledge. Lymba Jaguar uses NLP to extract candidate terms for ontologies. See: [Lymba](https://www.lymba.com/).
- **Gamechanger**: Developed by DoD and has been tailored for some DoD domains. It currently does not output RDF/OWL. See: [Gamechanger](https://github.com/dod-advana/gamechanger).

### Other Knowledge Graph Tools
- **Neo4j**: The most widely used LPG tool. See: [Neo4j](https://neo4j.com/). It can import RDF and some main OWL constructs. See: [Neo4j Labs Neosemantics](https://neo4j.com/labs/neosemantics/4.0/).
- **ArcGIS Knowledge**: Tightly integrated with other esri geospatial tools. See: [ArcGIS Knowledge](https://enterprise.arcgis.com/en/knowledge/).
- **TigerGraph**: See: [TigerGraph](https://www.tigergraph.com/).
