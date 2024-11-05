# Patterns

## DoD/IC Ontology Working Group
### Operationalizing Ontologies Community of Interest

**Contributors:** Paul Kogut, Don Pellegrino, Jonathan Vaidja, John Beverley, Joe Blankenship, Eric Peterson, Tim Toohill, Jennifer DeCamp, Ali Hasanzedah, John Judkins, Amanda Mitchell

## Introduction
The goal of the Operationalizing Ontologies COI is to provide guidance on how to apply ontologies in DoD/IC operational systems (e.g., C2, ISR, mission planning, equipment maintenance, logistics) and internal business systems. Current guidance is scattered across many sources and has significant gaps. The intended audience is both non-technical mission-focused personnel and very technical developers. Education of project managers, software architects, and junior software developers is a major barrier to fully leveraging the benefits of ontologies. The Applications sub WG will help DoD/IC personnel identify opportunities to insert ontologies into current and future systems.

This document contains a list and description of common domain-independent ontology application patterns and associated appropriate architectures. We are using the term “application pattern” instead of “use case” because use case often refers to aspects of applications related to domain-specific ontologies (e.g., air defense, aircraft maintenance). Most of the patterns listed below are fairly general and not focused on specific missions or equipment.

This document assumes use of a semantic infrastructure that includes OWL 2, RDF, and SPARQL (see Guidance for Ontology-based Systems Development). Many but not all patterns will need some form of rules for implementation (e.g., Semantic Web Rule Language (SWRL)).

## Application Patterns
The patterns below fall into two main categories:
- Support for semantic interoperability across enterprises with heterogeneous data sources. This can range from using the ontology as a reference for terms in implementation code or databases to a baked-in OWL infrastructure where the machine enforces semantic interoperability.
- Support for automated reasoning and flexible queries with common sense and domain-specific knowledge. Automated reasoning involves inferring implicit information from explicit knowledge in the ontology and RDF data.

This is not meant to be a formal ontology of application patterns. The patterns are meant to illustrate potential applications. The patterns may overlap and we expect that a real-world system will often include multiple patterns. Generic architectures for ontology-based applications are shown in Appendix A.

_Note: Need to add more descriptions and references for most patterns below._

### Semantic interoperability to integrate heterogeneous data for conventional enterprise systems, AI applications, and data analytics applications (aka a data fabric).
The ontology serves as a lingua franca between heterogeneous sources. The focus is on command centers, backend computing, and cloud-based systems. This is where semantic interoperability challenges for DoD/IC are similar to those found in commercial industry.

OWL supports explicit mappings between existing ontologies via equivalentClass and equivalentProperty. This can be used to bridge between 2 domains (e.g., Army and Navy). See these books for a thorough discussion of semantic interoperability and ontology engineering: (Arp et al., 2015) and (Kendall and McGuinness, 2019).

### Battlefield semantic interoperability
Similar to the semantic interoperability pattern except messages are passed through communications networks (often with limited bandwidth) and the mobile platforms and equipment often have complex legacy message formats. The adoption of ontologies for battlefield interoperability has been slow. There are many competing initiatives and standards such as:
- STITCHES (Systems of Systems Technology Integration Tool Chain for Heterogeneous Electronic Systems) was developed by DARPA for MOSAIC warfare. STITCHES uses a chain of transformations rather than a common lingua franca. _Note: How ontologies fit with STITCHES is still an open question._
- UCI (Universal Command and Control Interface) is an XML schema for battle management. The most recent version has about 600 message types. Fields in messages are defined by informal annotations. _Note: We are not aware of any efforts to map UCI to formal ontologies._

### Knowledge Graph-based datastore
As an alternative to or replacement for a conventional relational database or NoSQL database. Knowledge graphs come in many forms with a range of built-in semantics from Labeled Property Graphs to OWL/RDF. This is more of an architecture pattern rather than an applications pattern, but it is definitely an important concept. See Developer Guidance document.

### Data catalogs
Search for sources of relevant structured data across an enterprise for the purpose of data analytics often for management purposes. The DoD Chief Data and AI Office (CDAO) has an active project in this area.

### Digital assistants and question answering systems
(e.g., Siri, Alexa, ChatGPT). The ontology provides semantic interoperability between front-end natural language processing of questions and commands and SPARQL queries submitted to backend knowledge graphs.

Recently, systems based on Large Language Models (LLM) such as ChatGPT have exploded in popularity (Karpathy, 2023). They can be used for general question answering and generation of natural language text paragraphs and reports. However, they often generate wrong answers (hallucinate) and are difficult to train to answer domain-specific questions relevant to DoD/IC. However, ontologies and LLMs are complementary technologies (Pan, 2023). Hybrid question-answering systems may solve some of the problems with hallucination and lack of DoD/IC domain knowledge.

### Labeling of machine learning training data
(e.g., images, video, signals) to find appropriate training data and understand the scope and coverage of an ML training dataset. These ontology-based labels should also be used to label the output of deep neural network inference to enable semantic interoperability with other AI and non-AI services (see semantic interoperability pattern).

### Deductive reasoning
Including common sense (e.g., geospatial and temporal) and domain-specific (e.g., military doctrine). The goal is to provide the human with inferred implicit knowledge to improve decision-making in situations where there are large amounts of complex data or short time windows to perform tasks. AI systems need more common sense (Allen, 2004; Marcus, 2019; Marcus, 2020; Speer, 2017; Zellers, 2018; Sap, 2019).

### Robustness checking and monitoring of the results of deep neural network inference
(e.g., when results of automatic target recognition on novel objects and occluded images may be wrong because they are not similar to data in the machine learning training data set).

### Explainable AI
Ontologies can provide the semantic infrastructure to generate logical or natural language explanations of the results of deductive reasoning to build trust for the end-user. For example, some OWL reasoners can generate a trace of the rules and axioms used to answer a SPARQL query. (_JENNIFER urges descriptions of “AI” terms should come from NIST glossary_)

### Service orchestration
Web services or microservices can be automatically composed and aggregated into a pipeline to achieve a task. Semantic Web Services were developed by the OWL research community but never fully standardized. An ontology is used to describe various aspects of a service to support search and composition. Various techniques such as AI planners or genetic algorithms can support reasoning for service composition.

### Monitoring and fault diagnosis
Monitoring the operational status of electrical and mechanical equipment and troubleshooting when a failure occurs.

### Monitoring and medical diagnosis
Monitoring of the physical and mental state of humans (e.g., warfighters and other critical personnel) and providing an intervention or augmentation (Zhu, 2017; Can, 2019; Bhattacharya, 2020).

### Semantic search of text documents
The goal is to increase recall and precision of search results by using the semantics in ontologies to overcome limitations of keyword search. Hybrid systems can try SPARQL queries first and if direct answers are not found then resort to returning relevant documents via traditional search or approximate vector techniques.

### Recommender systems
Proactively recommend relevant information (e.g., people who read X also found Y and Z useful).

### Personalization
To learn and apply personal preferences in an information system (highly related to recommender systems pattern).

### Process automation
Applications intended to reduce manpower and increase accuracy of results ranging from totally autonomous task performance to human-in-the-loop workflow assistants. Robotic Process Automation systems are moving towards Intelligent Process Automation systems with hopefully more semantics.

### Assessment automation
Similar to process automation pattern except more focused on formal checklists.

### Robotics and autonomous vehicles
Reason with background world knowledge to interpret natural language commands from humans and sensor input and then make decisions based on environmental and mission context.

### Neuro-symbolic reasoning
Embed existing knowledge from ontologies and rules into deep neural networks so that basic common knowledge does not have to be learned from large datasets. Applications of this pattern are in the research stage (Kautz, 2021; Pan, 2023).

## References
Allen, J. P., & DiBona, P. (2004, June). Plan Understanding: Inferring Implicit Dependencies from Explicit Elements in Multi-Agent Plan Representations. In IC-AI (pp. 379-385).

Arp, Smith, Spear, Building Ontologies with Basic Formal Ontology Robert Arp, MIT Press 2015

Bhattacharya, N., Rakshit, S., Gwizdka, J., & Kogut, P. (2020). Relevance Prediction from Eye-movements Using Semi-interpretable Convolutional Neural Networks. In 2020 Conference on Human Information Interaction and Retrieval (CHIIR ’20), March, 2020, Vancouver, BC

Can, Y. S., Chalabianloo, N., Ekiz, D., & Ersoy, C. (2019). Continuous stress detection using wearable sensors in real life: Algorithmic programming contest case study. Sensors, 19(8), 1849.

Kendall and McGuinness, Ontology Engineering, Morgan & Claypool Publishers 2019

Karpathy 2023  https://karpathy.ai/stateofgpt.pdf

Kautz 2021 “The Third AI Summer”  https://henrykautz.com/talks/index.html 

Marcus, G., & Davis, E. (2019). Rebooting AI: Building Artificial Intelligence We Can Trust. Pantheon.

Marcus, G. (2020). The next decade in AI: four steps towards robust artificial intelligence. arXiv preprint arXiv:2002.06177.

Pan, S., Luo, L., Wang, Y., Chen, C., Wang, J., & Wu, X. (2023). Unifying Large Language Models and Knowledge Graphs: A Roadmap. arXiv preprint arXiv:2306.08302.

Sap, M., Le Bras, R., Allaway, E., Bhagavatula, C., Lourie, N., Rashkin, H., ... & Choi, Y. (2019, July). Atomic: An atlas of machine commonsense for if-then reasoning. In Proceedings of the AAAI Conference on Artificial Intelligence (Vol. 33, pp. 3027-3035).

Speer, R., Chin, J., & Havasi, C. (2017, February). Conceptnet 5.5: An open multilingual graph of general knowledge. In Thirty-First AAAI Conference on Artificial Intelligence.

Zellers, R., Bisk, Y., Schwartz, R., & Choi, Y. (2018). Swag: A large-scale adversarial dataset for grounded commonsense inference. arXiv preprint arXiv:1808.05326.

Zhu, Y., Jankay, R. R., Pieratt, L. C., & Mehta, R. K. (2017, September). Wearable sensors and their metrics for measuring comprehensive occupational fatigue: a scoping review. In Proceedings of the Human Factors and Ergonomics Society Annual Meeting (Vol. 61, No. 1, pp. 1041-1045).
