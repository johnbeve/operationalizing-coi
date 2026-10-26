# Appendix

## Terminology

Acronyms and terms used across the Patterns, Architectures, and Tools documents.

| Term | Meaning |
| --- | --- |
| API | Application Programming Interface. A defined way for software components to communicate. |
| BFO | Basic Formal Ontology. A top-level ontology (standardized as ISO/IEC 21838-2) that provides the most general categories, such as object, process, and quality. |
| C2 | Command and Control. |
| CCO | Common Core Ontologies. A suite of mid-level ontologies that extend BFO with terms common across many domains (e.g., agents, artifacts, information, events). |
| CDAO | DoD Chief Digital and Artificial Intelligence Office. |
| CL | Common Logic. An ISO standard (ISO/IEC 24707) family of first-order logic languages for exchanging knowledge. |
| Competency question | A question that an ontology or ontology-based system must be able to answer. Used to scope, design, and validate the ontology. |
| COTS / GOTS | Commercial off-the-shelf / Government off-the-shelf software. |
| CUI | Controlled Unclassified Information. |
| CycL | The knowledge representation language of the Cyc project. |
| DC | Dublin Core. A widely used vocabulary of metadata terms (e.g., title, creator, date). |
| DL | Description Logic. The family of formal logics underlying OWL 2 DL. |
| FOSS | Free and open-source software. |
| IC | Intelligence Community. |
| IRI | Internationalized Resource Identifier. The globally unique identifier for a resource (class, property, or individual) in RDF and OWL. |
| ISR | Intelligence, Surveillance, and Reconnaissance. |
| JSON-LD | JSON for Linked Data. A JSON-based serialization of RDF. |
| Knowledge graph | A graph of entities and the relationships between them, often structured by an ontology. |
| LLM | Large Language Model. |
| LPG | Labeled Property Graph. A graph data model in which nodes and edges carry labels and key-value properties (e.g., Neo4j). |
| MCP | Model Context Protocol. An open protocol for connecting AI applications to external tools and data sources. |
| NLP | Natural Language Processing. |
| OBO | Open Biological and Biomedical Ontologies. Both a community of ontologies (the OBO Foundry) and the OBO file format they historically used. |
| Ontology | A formal, machine-readable representation of the types of entities in a domain and the relationships between them. |
| OWL 2 | Web Ontology Language, version 2. The W3C standard language for authoring ontologies. |
| R2RML | RDB to RDF Mapping Language. A W3C standard for mapping relational databases to RDF. |
| RBAC | Role-Based Access Control. |
| RDF | Resource Description Framework. The W3C standard data model that represents information as subject-predicate-object triples. |
| Reasoner | Software that infers implicit facts from the axioms in an ontology and its data, and checks them for logical consistency (e.g., HermiT, ELK). |
| SHACL | Shapes Constraint Language. A W3C standard for validating RDF data against a set of conditions. |
| SKOS | Simple Knowledge Organization System. A W3C standard for representing thesauri, taxonomies, and controlled vocabularies. |
| SPARQL | SPARQL Protocol and RDF Query Language. The W3C standard query language for RDF. |
| SWRL | Semantic Web Rule Language. A language for writing if-then rules over OWL ontologies. |
| Triple store | A database designed to store and query RDF triples. |
| Virtual graph | A knowledge graph view over data that remains in its original source (e.g., a relational database), queried without converting it to RDF. |


## Training Materials

These materials will help the user with applying the operationalizing ontology patterns across varying levels of technical and academic acuity.

* __Beginners__ users have some domain expertise, but have little to no ontology application experience and may have less technical skills or exposure to ontology tools and architectures.
* __Intermediate__ users have a good amount of ontology application experience and can work with other on domain expertise (including their own) with some tools and architectures, but are not engineering new solutions.
* __Advanced__ users have a strong grasp of ontology tools and architectures, able to build new solutions for users at the intermediate and beginner levels.

### Beginners

* [Building Ontologies with Basic Formal Ontology Book](https://ontology.buffalo.edu/BOBFO/)
* [BFO 2020 Github Repository](https://github.com/BFO-ontology/BFO-2020)
* [Barry Smith on YouTube](https://www.youtube.com/@BarrySmithOntology)

### Intermediate

* [NCOR Applied Ontology Education](https://github.com/Applied-Ontology-Education)
* [Common Core Ontologies](https://github.com/CommonCoreOntology/CommonCoreOntologies)
* [John Beverley on YouTube](https://www.youtube.com/@johnbeve)

### Advanced

* These will be subject specific and may vary broadly from or overlap with Basic and Intermediate topic areas.

#### Reasoning

* [OWL 2 Web Ontology Language Primer](https://www.w3.org/TR/owl2-primer/): the W3C's introduction to OWL 2, including what can be inferred from each kind of axiom.
* [A Description Logic Primer](https://arxiv.org/abs/1201.4089) (Krötzsch, Simančík & Horrocks): a concise introduction to the description logics that underlie OWL 2 DL reasoning.
