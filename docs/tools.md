# Tools

## DoD/IC Ontology Working Group - Operationalizing Ontologies Community of Interest

**Contributors:** Paul Kogut, Don Pellegrino, Jonathan Vajda, John Beverley, Joe Blankenship, Eric Peterson, Tim Toohill, Jennifer DeCamp, Ali Hasanzedah, John Judkins, Amanda Mitchell

## Introduction

The goal of the Operationalizing Ontologies Community of Interest (OO-COI) is to provide guidance on how to apply ontologies in DoD/IC operational systems (e.g., C2, ISR, mission planning, equipment maintenance, logistics) and internal business systems. Current guidance is scattered across many sources and has significant gaps. The intended audience is both non-technical mission-focused personnel and very technical developers. Education of project managers, software architects, and junior software developers is a major barrier to fully leveraging the benefits of ontologies. The OO-COI will help DoD/IC personnel identify opportunities to insert ontologies into current and future systems.

This document will help DoD/IC software engineers get started in developing applications that leverage ontologies. See the Patterns document for help in identifying opportunities to insert ontologies into current and future systems.

> [!NOTE]
> This document assumes use of DoD/IC Foundry-compliant semantic infrastructure that includes OWL 2, RDF, and SPARQL (see Guidance for Ontology-based Systems Development).

## Essential Tool Concepts

### OWL Deductive Reasoning

Reasoning is used to answer queries and check the logical consistency of ontologies. OWL 2 profiles are designed to accommodate a variety of reasoning capabilities. The choice of the appropriate OWL 2 profile depends on the size of the data and the type of reasoning required for an application. These profiles trade off expressivity in exchange for performance or ability to implement using a particular technology (e.g., business rule engines vs. databases).

> [!NOTE]
> Note that satisfying a SPARQL query is a kind of inference and so the totality of inference capabilities is what the reasoner can do plus what SPARQL can do. 

There are four OWL 2 profiles:

* **OWL Full**
* **OWL EL**
* **OWL RL**
* **OWL QL**

OWL Full is the most expressive profile. However, OWL Full reasoning might run forever in some cases (it is undecidable). EL, RL, and QL leave out specific OWL expressions that impact reasoning performance and decidability.

For example, queries that involve `sameAs` expressions on individuals are notoriously computationally intensive.

* OWL EL is less expressive and suitable for fast reasoning on ontologies that obey its restrictions. EL is useful for checking/validating complex ontologies but is not as useful for querying with instance data.
* OWL RL is designed to be implementable using rule systems and is quite powerful. OWL RL is a good default profile for many applications.
* OWL QL is designed to be implemented in SQL and is useful for querying with large amounts of data.

It is not uncommon to reason using OWL Full on the ontology, augmenting the ontology with those inferences before loading the combination into a triple store, and then using a less powerful profile to deploy for querying instance data.

To select an appropriate profile, you can develop a set of “competency questions” that determine the kinds of inference that a specific application needs. Then map those competency questions to OWL expressions in profiles to select the appropriate profile.

> [!NOTE]
> The next version of this document will include a more complete explanation on checking the logical consistency of ontologies and advice on the specific reasoners that are available such as Pellet, Hermit, and ELK.

### Rules

The tightly integrated combination of ontologies and rules is a powerful artificial intelligence (AI) capability with wide applicability.

For example, ontologies and rules are being used by BMW for automated reasoning in autonomous cars[^1]. 

The Semantic Web Rule Language (SWRL)[^2] provides if-then rules on top of OWL[^3]. More human-readable forms of rules are also available[^4]. Rules can also be embedded in SPARQL construct statements.

### SHACL

The Shapes Constraint Language (SHACL)[^5][^6] is a way to check the quality of your RDF data. This is important for applications with large-scale or messy data.

### Labeled Property Graphs

Labeled Property Graphs[^7] (LPG) are schema-optional graph databases that were designed for highly efficient, scalable data queries. Though lacking support[^8] for semantic interoperability and automated reasoning, application of schema and top level ontology standards can facilitate this functionality. These factors make LPGs excellent choices for applications in which sub-graph access, inter- and intra-network alignment, real-time query, and flexible modeling are requirements.

However, LPGs are not as flexible as RDF in its modeling extensibility. Though LPG ecosystems are complementary to OWL ecosystems, attention to the manner in which LPGs are modeled to facilitate consistent ontologies must be a key locus for ontology engineers. OWL ontologies[^9] can be converted to LPG[^10] with some loss of semantics which may potentially impact your application. As a result, testing and validation of ontology models in LPGs must maintain a high level of scrutiny regardless of the level of automation applied to their generation or curation.

Query languages for LPGs such as Gremlin[^11] and openCypher[^12] optimize for graph traversal rather than OWL-like semantics and are not formal standards like SPARQL[^13]. Each query paradigm comes with compromises in syntactic semantic complexity, but is ultimately selected based on the requirements for which the LPG must provide the users within their communities of practice. Subsequently, users require direct logically generated answers (e.g., OWL semantic standards) as well as the ability to explore information in the graphs.

### Natural Language Processing

Natural Language Processing (NLP) is the handling of human language artifacts by a machine for the purpose of using those artifacts in text classification, speech recognition, understanding, generation of new text, and several other tasks.

The parsing of unstructured data including natural language documents and human-to-human or human-to-machine conversations into RDF which is semantically linked to ontologies is a major advantage of the OWL ecosystem. Processing natural language with high precision and recall is challenging.

A variety of NLP tools exist. All require significant machine learning training or knowledge engineering for most specialized DoD/IC domains. Large language models, such as ChatGPT, are NLP tools that generate new text artifacts based on next work prediction from a large foundation model of curated reference corporas.

### Relational Database to RDF Mapping Language

R2RML[^14] is a language for expressing mappings from relational databases to RDF datasets.

## List of Languages

There are many language standards that support ontology design pattern tasks or broader application of ontology products.

* OWL2
* SKOS
* DC
* CL
* OBO
* RDF
* CycL

## List of Tools and Frameworks

The tools below are roughly grouped by type (e.g., ontology development environment, knowledge graph, reasoning) but some tools cover multiple functions. Like in many software and AI technology areas, there is a continuous debate about the advantages and disadvantages of open-source software vs. commercial products. In the OWL ecosystem, commercial products are in general ahead of open-source frameworks especially in the category of knowledge graph and reasoning tools. Even the widely accepted and used Protégé is being left behind. The DoD/IC should carefully consider whether or not they should select a designated set of tools or build their own set of tools because commercial products are advancing rapidly. It is probably best to adhere to OWL, RDF, and SPARQL standards and swap in new tools as they become available.

### Catalogs

* Agent Tool (DOD/IC Ontology Foundry and Johns Hopkins Applied Physics Lab)
    * Agent Tool provides a way to search a curated library of ontologies.
    * It also provides tools for checking ontologies for compliance to documentation standards and eventually semantic consistency with reasoners.

### Ontology Development

* **Protégé**: A widely used open-source ontology development environment.[^15][^16]
* **WebProtege**: An open-source collaborative ontology development environment. A public version is hosted by Stanford.[^17] It can also be installed on premises.
* **Mobi**: A free collaborative ontology editor with many advanced features including support for SHACL.[^18] 
* **TopBraid Composer**: A mature commercial ontology development environment with many advanced features.[^19] 
* **ROBOT**: A Java-based collection of utility functions that can be used to develop and maintain ontologies such as extract, merge, filter, and logical validation. These utilities can be composed into a workflow.[^20] 
* **RDFLib**: A widely used Python utility package.[^21]
  * RDFLib can be used to ingest a variety of sources (e.g., SQL databases, MongoDB, CSV files, NLP parser output) into RDF for input into knowledge graphs. Among these capabilities, RDFLib can be used to create and modify ontology files in a programmatic way. For examples: with a spreadsheet, generate a new OWL file; with a CSV file of replacement IRIs, update old IRIs to new IRIs; perform a quality control check whether a definition fits the genus-species structure.

### Knowledge Graph and Reasoning

* **OWLReady2**: An open-source OWL framework. See the book `Ontologies with Python: Programming OWL 2.0 Ontologies with Python and Owlready2`. OWLReady2 uses an rdf/xml syntax and SWRL rules.[^22]
* **Karma**: An open-source ontology alignment tool, that integrates data from different sources into RDF.[^23] Karma is an information integration tool that enables users to quickly and easily integrate data from a variety of data sources including databases, spreadsheets, delimited text files, XML, JSON, KML and Web APIs. Users integrate information by modeling it according to an ontology of their choice using a graphical user interface that automates much of the process. Karma learns to recognize the mapping of data to ontology classes and then uses the ontology to propose a model that ties together these classes. Users then interact with the system to adjust the automatically generated model. During this process, users can transform the data as needed to normalize data expressed in different formats and to restructure it. Once the model is complete, users can published the integrated data as RDF or store it in a database.
* **Ontop**: Uses R2RML to virtually query relational databases. The data remains in the database and does not get converted into RDF.[^24]
Triple Stores for knowledge graphs are being scaled up to handle large amounts of data and do practical automated reasoning.[^25]
* **Stardog**: A mature commercial knowledge graph infrastructure including a scalable RDF triple store, a state-of-the-art OWL reasoner, and a virtual graph capability that allows access to data sources without ingesting them. Stardog has a user-friendly SPARQL-based rules syntax and also supports SWRL.[^26] Pystardog is a python wrapper for Stardog.[^27]
* **Cambridge Semantics Anzo**: A scalable knowledge graph platform with end-to-end pipeline support for structured and unstructured data. Anzo greatly facilitates adoption for novice users of knowledge graphs.[^28]
* **Oxford Semantic Technologies RDFox**: A scalable knowledge graph platform designed with an emphasis on efficient reasoning. RDFox enables intelligent information processing by representing and reasoning with domain knowledge in the form of rules and ontological axioms. RDFox is geared towards expert users.[^29]
* **Apache Jena**: An open-source Java framework for building semantic web applications.[^30] Jena includes a query engine for SPARQL called ARQ.
* **Amazon Neptune**: Supports both RDF and LPGs.[^31]
* **Ontotext GraphDB**[^32]
* **(ALI)**
* **Franz AllegroGraph**[^33]
* **PoolParty**[^34]
* **Neo4j**: The most widely used LPG tool.[^35] It can import RDF and some main OWL constructs.[^36]
* **ArcGIS Knowledge**: Tightly integrated with other esri geospatial tools.[^37]
* **TigerGraph**[^38]

### Natural Language Processing

* **spaCy and Prodigy**: Prodigy is used to label training data and spaCy learns to parse sentences based on that training data. These are widely used tools.[^39]
* **Lymba**: A commercial tool that uses hybrid machine learning and semantic knowledge. Lymba Jaguar uses NLP to extract candidate terms for ontologies.[^40]
* **Gamechanger**: Developed by DoD and has been tailored for some DoD domains. It currently does not output RDF/OWL.[^41]

### Text Editors

* **Microsoft Visual Studio Code**: A source code editor with syntax highlighting.[^42] Industry standard for coding and software development. Natively supports Git versioning and source control, command line terminal, syntax highlighting for common programming and markup languages, and extension support syntax highlighting for OWL-family languages and SPARQL.
* **Notepad++**: An open-source source code editor with syntax highlighting.[^43] Notepad++ is a source code editor. It features syntax highlighting, code folding and limited autocompletion for programming, scripting, and markup languages, but not intelligent code completion or syntax checking. Supports over 70 different programming and markup languages.

### Data Engineering

* **Apake NiFi**: An open-source data flow manager, juggling events and passing them to different services and microservices.[^44] NiFi was built to automate the flow of data between systems. While the term 'dataflow' is used in a variety of contexts, we use it here to mean the automated and managed flow of information between systems. This problem space has been around ever since enterprises had more than one system, where some of the systems created data and some of the systems consumed data. The problems and solution patterns that emerged have been discussed and articulated extensively. A comprehensive and readily consumed form is found in the Enterprise Integration Patterns.

### Data Architecture

* **Podman**: An open-source container and image manager.[^45] Podman (the POD MANager) is a tool for managing containers and images, volumes mounted into those containers, and pods made from groups of containers. Podman runs containers on Linux, but can also be used on Mac and Windows systems using a Podman-managed virtual machine. Podman is based on libpod, a library for container lifecycle management that is also contained in this repository. The libpod library provides APIs for managing containers, pods, container images, and volumes.
* **Kubernetes**: An open source system for automating deployment, scaling, and management of containerized applications.[^46] Kubernetes (also known as K8s) is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

## References

[Ontology Awesome List](https://github.com/ozekik/awesome-ontology)

[^1]: [Reasonable Vehicles Rule the Road](https://www.oxfordsemantic.tech/blog/reasonable-vehicles-rule-the-road)
[^2]: [SWRL Tutorial](https://www.michaeldebellis.com/post/swrl_tutorial)
[^3]: [OWLReady2 Rules](https://owlready2.readthedocs.io/en/v0.37/rule.html)
[^4]: [Stardog User-Defined Rules](https://docs.stardog.com/inference-engine/user-defined-rules)
[^5]: [SHACL](https://www.w3.org/TR/shacl/) 
[^6]: [TopQuadrant SHACL Tutorial](https://archive.topquadrant.com/technology/shacl/tutorial/) 
[^7]: [Labeled Property Graphs](https://doi.org/10.1145/3365109.3368782) 
[^8]: https://doi.org/10.1109/BigData52589.2021.9671547 
[^9]: [OWL ontologies](https://www.w3.org/OWL/)
[^10]: https://doi.org/10.3390/app11177782
[^11]: [Gremlin](https://tinkerpop.apache.org/gremlin.html) 
[^12]: [openCypher](https://opencypher.org/) 
[^13]: [SPARQL](https://www.w3.org/TR/sparql11-query/)
[^14]: [R2RML](https://www.w3.org/TR/r2rml/)
[^15]: [Protégé Pizza Tutorial](https://www.michaeldebellis.com/post/new-protege-pizza-tutorial)
[^16]: [Protégé Wiki](https://protegewiki.stanford.edu/wiki/Main_Page)
[^17]: [WebProtege](https://webprotege.stanford.edu/)
[^18]: [Mobi](https://mobi.inovexcorp.com/)
[^19]: [TopBraid Composer](https://www.topquadrant.com/products/topbraid-composer/)
[^20]: [ROBOT](http://robot.obolibrary.org/)
[^21]: [RDFLib](https://github.com/RDFLib/rdflib)
[^22]: [OWLReady2](https://github.com/pwin/owlready2)
[^23]: [Karma](https://github.com/usc-isi-i2/Web-Karma/releases)
[^24]: [Ontop](https://ontop-vkg.org/)
[^25]: [Large Triple Stores](https://www.w3.org/wiki/LargeTripleStores)
[^26]: [Stardog](https://www.stardog.com/learn-stardog/)
[^27]: [Pystardog](https://github.com/stardog-union/pystardog)
[^28]: [Cambridge Semantics Anzo](https://cambridgesemantics.com/)
[^29]: [Oxford Semantic Technologies](https://www.oxfordsemantic.tech/)
[^30]: [Apache Jena](https://jena.apache.org/getting_started/index.html)
[^31]: [Amazon Neptune](https://aws.amazon.com/neptune/)
[^32]: [Ontotext GraphDB](https://www.ontotext.com/products/graphdb/)
[^33]: [Franz AllegroGraph](https://allegrograph.com/)
[^34]: [PoolParty](https://www.poolparty.biz/)
[^35]: [Neo4j](https://neo4j.com/)
[^36]: [Neo4j Labs Neosemantics](https://neo4j.com/labs/neosemantics/4.0/)
[^37]: [ArcGIS Knowledge](https://enterprise.arcgis.com/en/knowledge/)
[^38]: [TigerGraph](https://www.tigergraph.com/)
[^39]: [spaCy](https://spacy.io/) and [Prodigy](https://prodi.gy/)
[^40]: [Lymba](https://www.lymba.com/)
[^41]: [Gamechanger](https://github.com/dod-advana/gamechanger)
[^42]: [VS Code](https://code.visualstudio.com/)
[^43]: [Notepad++](https://notepad-plus-plus.org/)
[^44]: [NiFi](https://nifi.apache.org/)
[^45]: [Podman on GitHub](https://github.com/containers/podman)
[^46]: [Kubernetes](https://kubernetes.io/)
