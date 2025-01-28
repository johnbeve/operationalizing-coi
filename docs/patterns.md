# Patterns

## DoD/IC Ontology Working Group - Operationalizing Ontologies Community of Interest

**Contributors:** Paul Kogut, Don Pellegrino, Jonathan Vajda, John Beverley, Joe Blankenship, Eric Peterson, Tim Toohill, Jennifer DeCamp, Ali Hasanzedah, John Judkins, Amanda Mitchell

## Introduction

The goal of the Operationalizing Ontologies Community of Interest (OO-COI) is to provide guidance on how to apply ontologies in DoD/IC operational systems (e.g., C2, ISR, mission planning, equipment maintenance, logistics) and internal business systems. Current guidance is scattered across many sources and has significant gaps. The intended audience is both non-technical mission-focused personnel and very technical developers. Education of project managers, software architects, and junior software developers is a major barrier to fully leveraging the benefits of ontologies. The OO-COI will help DoD/IC personnel identify opportunities to insert ontologies into current and future systems.

This document contains a list of common domain-independent ontology application patterns and associated appropriate architectures. We are using the term “application pattern” instead of “use case” because use case often refers to aspects of applications related to domain-specific ontologies (e.g., air defense, aircraft maintenance, etc.). Most of the patterns listed below are fairly general and not focused on specific missions or equipment.

```{note}
This document assumes use of DoD/IC Foundry-compliant semantic infrastructure that includes OWL 2, RDF, and SPARQL (see Guidance for Ontology-based Systems Development). Many, but not all, patterns will need some form of rules for implementation (e.g., Semantic Web Rule Language (SWRL)).
```

## Application Patterns

The patterns below fall into two main categories:

* Support for semantic interoperability across enterprises with heterogeneous data sources.
  * This can range from using the ontology as a reference for terms in implementation code or databases to a baked-in OWL infrastructure where the machine enforces semantic interoperability.
* Support for automated reasoning and flexible queries with common sense and domain-specific knowledge.
  * Automated reasoning involves inferring implicit information from explicit knowledge in the ontology and RDF data.

This is not meant to be a formal ontology of application patterns: the patterns are meant to illustrate potential applications. The patterns may overlap and we expect that a real-world systems will often include multiple patterns. Generic architectures for ontology-based applications are shown in the architecture document.

```{note}
The patterns are templated into the following baseline fields:

* [competency questions](https://arxiv.org/pdf/2412.13688) which help scope, validate, establish, relate, or contextualize the pattern.
* key terms associated with the pattern.
* descriptions of the pattern.
* use cases in which the pattern has or can be applied including relevant rules.
```

### Data Fabric

* Competency questions
  * How is data connected?
  * What systems allow connection of data assets?
* Terms
  * data, metadata, cloud compute
* Description
  * Semantic interoperability to integrate heterogeneous data for conventional enterprise systems, AI applications, and data analytics applications (aka a data fabric).
* Use cases
  * The ontology serves as a lingua franca between heterogeneous sources. The focus is on command centers, backend computing, and cloud-based systems. This is where semantic interoperability challenges for DoD/IC are similar to those found in commercial industry.
  * OWL supports explicit mappings between existing ontologies via equivalentClass and equivalentProperty. This can be used to bridge between 2 domains (e.g., Army and Navy). See these books for a thorough discussion of semantic interoperability and ontology engineering.[^2][^5]

### Battlefield semantic interoperability

* Competency questions
  * What communication systems need to exchange information?
  * What kind of information must be transferred between communication systems?
  * Who is operating the communication systems?
  * Where are the communication systems located?
* Terms
  * battlefield, communications, interoperability
* Description
  * Similar to the semantic interoperability pattern except messages are passed through communications networks (often with limited bandwidth) and the mobile platforms and equipment often have complex legacy message formats. The adoption of ontologies for battlefield interoperability has been slow.
* Use cases
  * STITCHES (Systems of Systems Technology Integration Tool Chain for Heterogeneous Electronic Systems) was developed by DARPA for MOSAIC warfare. STITCHES uses a chain of transformations rather than a common lingua franca.
    * _Note:_ How ontologies fit with STITCHES is still an open question.
  * UCI (Universal Command and Control Interface) is an XML schema for battle management. The most recent version has about 600 message types. Fields in messages are defined by informal annotations.
    * _Note:_ We are not aware of any efforts to map UCI to formal ontologies.

### Knowledge Graph-based datastore

* Competency questions
  * What thing or collection of things requires a dyadic data model?
  * Is there triple store or dyadic data pattern?
  * Is the the query type a traversal?
  * Is connection between entities the primary goal of analysis?
* Terms
  * knowledge graph, relationships, dyad, triple, property, RDF
* Description
  * As an alternative to or replacement for a conventional relational database or NoSQL database. Knowledge graphs come in many forms with a range of built-in semantics from Labeled Property Graphs to OWL/RDF. This is more of an architecture pattern rather than an applications pattern, but it is definitely an important concept.
* Use cases
  * Exploration of social networks
  * Examination of communications networks

### Data catalogs

* Competency questions
  * What data assets do I have?
  * Where are my data stored?
  * Who has access to what data assets?
  * When was the data loaded, accessed, or depricated?
* Terms
  * data, catalog, metadata, security, user, mart
* Description
  * Search for sources of relevant structured data across an enterprise for the purpose of data analytics often for management purposes.
* Use cases
  * DoD Chief Data and AI Office (CDAO) projects

### Digital assistants and question answering systems

* Competency questions
  * What is the domain of assistance?
  * Who answers these types of questions?
  * What skills are needed to answer questions?
  * What constraints do you have on questions?
* Terms
  * answering system, digital assistant, agent, LLM
* Description
  * Recently, systems based on Large Language Models (LLM) such as ChatGPT have exploded in popularity.[^6] They can be used for general question answering and generation of natural language text paragraphs and reports. However, they often generate wrong answers (hallucinate) and are difficult to train to answer domain-specific questions relevant to DoD/IC. However, ontologies and LLMs are complementary technologies.[^10] Hybrid question-answering systems may solve some of the problems with hallucination and lack of DoD/IC domain knowledge.
* Use cases
  * Siri, Alexa, ChatGPT
  * The ontology provides semantic interoperability between front-end natural language processing of questions and commands and SPARQL queries submitted to backend knowledge graphs.

### Labeling of machine learning training data

* Competency questions
  * What type of data is being labeled?
  * What skills are needed to assess training data?
  * Where is the training data located?
  * How is the data being modeled?
* Terms
  * training data, machine learning, deep learning, classification
* Description
  * To find appropriate training data and understand the scope and coverage of an ML training dataset. These ontology-based labels should also be used to label the output of deep neural network inference to enable semantic interoperability with other AI and non-AI services (see semantic interoperability pattern.
* Use cases
  * Image classification
  * Video classification
  * Signals classification

### Deductive reasoning

* Competency questions
  * What is being reasoned on?
  * What are the limits upon which the topic is being reasoned?
  * Who is involved in the reasoning process?
  * How is reasoning being performed?
* Terms
  * reasoning, deduction, inference, decision-making, data, logic
* Description
  * To provide the human with inferred implicit knowledge to improve decision-making in situations where there are large amounts of complex data or short time windows to perform tasks. AI systems need more common sense.[^1][^8][^9][^11][^12][^13]
* Use cases
  * Common sense (e.g., geospatial and temporal) 
  * Domain-specific (e.g., military doctrine)

### Robustness checking and monitoring of the results of deep neural network inference

* Competency questions
  * What is robustness?
  * How is checking of robustness performed?
  * What are the constraints of the neural network?
  * What is being monitored?
* Terms
  * neural network, data, monitoring, testing
* Description
  * Use of ontology to enhance results of automatic target recognition on novel objects and occluded images as they may be wrong because they are not similar to data in the machine learning training data set.
* Use cases
  * 

### Explainable AI

* Competency questions
  * What about the AI needs to be explained?
  * How is explaination affecting the AI?
  * What will explaination of the AI do?
* Terms
  * artificial intelligence, oversight, algorithms
* Description
  * Ontologies can provide the semantic infrastructure to generate logical or natural language explanations of the results of deductive reasoning to build trust for the end-user.
* Use cases
  * OWL reasoners can generate a trace of the rules and axioms used to answer a SPARQL query. (_JENNIFER urges descriptions of “AI” terms should come from NIST glossary_)

### Service orchestration

* Competency questions
  * What services need orchestration?
  * What things will be orchestrated?
  * Where will this orchestration occur?
* Terms
  * services, pipelines, API, architecture, information technology
* Description
  * Web services or microservices can be automatically composed and aggregated into a pipeline to achieve a task. Semantic Web Services were developed by the OWL research community but never fully standardized. An ontology is used to describe various aspects of a service to support search and composition. Various techniques such as AI planners or genetic algorithms can support reasoning for service composition.
* Use cases
  * Resolving task orchestration across multiple 

### Monitoring and fault diagnosis

* Competency questions
  * What systems are being monitored?
  * What faults do these systems incur?
  * How are faults identified?
  * How is monitoring performed?
* Terms
  * monitoring, faults, errors, diagnosis, troubleshooting, electrical, mechanical
* Description
  * Monitoring the operational status of electrical and mechanical equipment and troubleshooting when a failure occurs.
* Use cases
  * Automated and semi-automated system diagnostics of military platforms

### Monitoring and medical diagnosis

* Competency questions
  * What mental states are being monitored?
  * What physical states are being monitored?
  * What diagnosis are required for a physical or mental state?
  * Where is monitoring or diagnosis required?
  * When is monitoring or diagnosis performed?
* Terms
  * medical, psychological, warfighter, health, monitoring, diagnosis
* Description
  * Monitoring of the physical and mental state of humans (e.g., warfighters and other critical personnel) and providing an intervention or augmentation.[^3][^4][^14]
* Use cases
  * Identify PTSD in warfighters
  * Rapidly identify disease vectors within warfighter forces
  * Anticipate treatment geographically or temporally for varying distribution of warfighting forces

### Semantic search of text documents

* Competency questions
  * What topics or materials need to be searched?
  * Is there a priority in search?
  * How will text documents be accessed for search?
  * Is there something in the text of consistent interest?
* Terms
  * search, semantic, text, semantic, NLP, SPARQL
* Description
  * The goal is to increase recall and precision of search results by using the semantics in ontologies to overcome limitations of keyword search. Hybrid systems can try SPARQL queries first and if direct answers are not found then resort to returning relevant documents via traditional search or approximate vector techniques.
* Use cases
  * Wolfram Alpha search models
  * Enforce better GenAI prompt responses

### Recommender systems

* Competency questions
  * What topics are within the domain of recommendation?
  * What is being recommended?
  * How is a recommendation assessed?
  * Are there any limitations on inputs?
* Terms
  * recommendation, semantic, artificial intelligence, LLM, GenAI
* Description
  * Proactively recommend relevant information (e.g., people who read X also found Y and Z useful).
* Use cases
  * A topic specific chat Interface
  * A knowledge graph interpretation layer for user responses

### Personalization

* Competency questions
  * What are the users environmental preferences?
  * What environment is being personalized?
  * How can personalization be performed?
  * Can personalization be automated?
* Terms
  * personalization, semantic, artificial intelligence, LLM, GenAI
* Description
  * To learn and apply personal preferences in an information system (highly related to recommender systems pattern).
* Use cases
  * Learning from user interactions to optimize their working environment.
  * Learning from groups of users to improve system performance.

### Process automation

* Competency questions
  * What processes are being automated?
  * How is the process performed without automation?
  * When is the process performed?
  * What ways is automation possible with portions of the process?
* Terms
  * process, automation, workflow
* Description
  * Applications intended to reduce manpower and increase accuracy of results ranging from totally autonomous task performance to human-in-the-loop workflow assistants. 
* Use cases
  * Robotic Process Automation systems are moving towards Intelligent Process Automation systems with hopefully more semantics.

### Assessment automation

* Competency questions
  * What is being assessed?
  * How is the assessment performed?
  * What skills are needed to make and assessment?
* Terms
  * assessment, automation, reasoning, checklists
* Description
  * Similar to process automation pattern except more focused on formal checklists.
* Use cases
  * Automated testing of technical systems
  * Improving human-in-the-loop assessment tasks

### Robotics and autonomous vehicles

* Competency questions
  * What systems are used with autonomous vehicles?
  * What vehicles are autonomous?
  * What is the purpose of robotic or autonomous system use?
  * How are systems being automated?
  * When are these systems operational?
  * Where are these systems operational?
  * How is testing or simulation performed?
* Terms
  * robots, automation, vehicles, reasoning, GenAI, sensors, decision-making
* Description
  * Reason with background world knowledge to interpret natural language commands from humans and sensor input and then make decisions based on environmental and mission context.
* Use cases
  * Coordination of autonomous sytems with different communication protocols.
  * Multi-Agent, multi-modal autonomous system coordination

### Neuro-symbolic reasoning

* Competency questions
  * What representations of knowledge are present in the model?
  * What is the expectation for reasoning in this system?
  * How are symbolic elements trained in this model?
  * Where is the model being consumed by the user?
  * How is the user applying the model?
* Terms
  * neuro-symbolic, reasoning, deep learning, GenAI
* Description
  * Embed existing knowledge from ontologies and rules into deep neural networks so that basic common knowledge does not have to be learned from large datasets. Applications of this pattern are in the research stage.[^7][^10]
* Use cases
  * Resolving data dimensionality post-modeling within disparate data systems.

## References

[^1]: Allen, J. P., & DiBona, P. (2004, June). Plan Understanding: Inferring Implicit Dependencies from Explicit Elements in Multi-Agent Plan Representations. In IC-AI (pp. 379-385).
[^2]: Arp, Smith, Spear, Building Ontologies with Basic Formal Ontology Robert Arp, MIT Press 2015
[^3]: Bhattacharya, N., Rakshit, S., Gwizdka, J., & Kogut, P. (2020). Relevance Prediction from Eye-movements Using Semi-interpretable Convolutional Neural Networks. In 2020 Conference on Human Information Interaction and Retrieval (CHIIR ’20), March, 2020, Vancouver, BC
[^4]: Can, Y. S., Chalabianloo, N., Ekiz, D., & Ersoy, C. (2019). Continuous stress detection using wearable sensors in real life: Algorithmic programming contest case study. Sensors, 19(8), 1849.
[^5]: Kendall and McGuinness, Ontology Engineering, Morgan & Claypool Publishers 2019
[^6]: Karpathy 2023  https://karpathy.ai/stateofgpt.pdf
[^7]: Kautz 2021 “The Third AI Summer”  https://henrykautz.com/talks/index.html 
[^8]: Marcus, G., & Davis, E. (2019). Rebooting AI: Building Artificial Intelligence We Can Trust. Pantheon.
[^9]: Marcus, G. (2020). The next decade in AI: four steps towards robust artificial intelligence. arXiv preprint arXiv:2002.06177.
[^10]: Pan, S., Luo, L., Wang, Y., Chen, C., Wang, J., & Wu, X. (2023). Unifying Large Language Models and Knowledge Graphs: A Roadmap. arXiv preprint arXiv:2306.08302.
[^11]: Sap, M., Le Bras, R., Allaway, E., Bhagavatula, C., Lourie, N., Rashkin, H., ... & Choi, Y. (2019, July). Atomic: An atlas of machine commonsense for if-then reasoning. In Proceedings of the AAAI Conference on Artificial Intelligence (Vol. 33, pp. 3027-3035).
[^12]: Speer, R., Chin, J., & Havasi, C. (2017, February). Conceptnet 5.5: An open multilingual graph of general knowledge. In Thirty-First AAAI Conference on Artificial Intelligence.
[^13]: Zellers, R., Bisk, Y., Schwartz, R., & Choi, Y. (2018). Swag: A large-scale adversarial dataset for grounded commonsense inference. arXiv preprint arXiv:1808.05326.
[^14]: Zhu, Y., Jankay, R. R., Pieratt, L. C., & Mehta, R. K. (2017, September). Wearable sensors and their metrics for measuring comprehensive occupational fatigue: a scoping review. In Proceedings of the Human Factors and Ergonomics Society Annual Meeting (Vol. 61, No. 1, pp. 1041-1045).
