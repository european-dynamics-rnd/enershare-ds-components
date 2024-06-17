![Enershare ](images/logo_Enershare.png)
# Enershare (MVP2 readme)
ENERSHARE scope and objectives are considered to cover three core cornerstones. Trust and sovereignty of data, interoperability of data and participants, and the business logic/applications consist the set of these three concepts that ENERSHARE aims to focus on. Besides ENERSHARE is closely related on and influenced by the IDS reference architecture for International Data Spaces which introduces a benchmark for developing data-driven products, ecosystems, and services, providing a standardized framework for implementation and development. A data space consists of a network of parties and components. In the International Data Spaces Reference Architecture Model (IDS-RAM) this network is formed by connectors. In other words, each component or service in a data space is represented by a connector. An IDS connector allows and enables the exchange of data within a data space. It provides a number of core functions that are extended with business logic inside a data app. Among the Connector Core Service(s) are the means for Authentication, Contract Negotiation and Trusted Data Exchange. 

This documentation refers in the particular components of MVP2.0. The MVP2.0 is comprised of the following elements:
- [The TNO Security Gateway (TSG) Connector](#the-tsg-connector)
- [Metadata Broker](#metadata-broker)
- [Identity Provider (CA + DAPS)](#identity-provider(ca--daps))
- [Vocabulary Hub & Wizard for generation of Open APIs](#vocabulary-hub--wizard-for-generation-of-open-apis)
- [OpenAPI Interfaces](#openapi-interfaces)
- [Transformation Service](#transformation-service)
- [Compliance Service](#compliance-service)
- [Mashup Editor](#mashup-editor)
- [Semantic Models](#semantic-models)
- [Marketplace](#marketplace)
- [Clearing House](#clearing-house)
- [AppStore](#appstore)
- [Blockchain & Notarisation Services](#blockchain--notarisation-services)\

A set of available complementary components will provided based on the FIWARE True Connector:
- The True Connector
- Usage Control & Rules enforcement implementation in TRUE connector
- [FIWARE Context Broker](#)

# TSG connector and side components 
TEXT & FIGURES
## The TNO Security Gateway (TSG) Connector
The basic MVP2 implementation of the IDSA Connector is the TNO Security Gateway (TSG) Core Container. The TSG container operates as a base for data space components (since participation in a Data Space as a stakeholder is possible only through a connector) and can be easily integrated with services and data apps. These data apps perform the business logic for both data consumers and providers, in the same way that is required in ENERSHARE.

**Description and Purpose**

The TSG Connector performs seamless collaboration and data sharing, supporting the participants to exploit the maximum potential of their data components and assets and evolve their practices. Additionally, based on the TSG concept simultaneously with the IDSA architecture, the TSG connector ensures the establishment of very specific rules and principles customized and aligned according to the project’s objectives. TSG Connector adheres to an IDSA-based HTTP Multipart communication protocol, automating message flows and being easily deployable.

**Development Progress**

MVP2 updated the TSG Connector and its related components functionality. Currently TSA connector is being updated to function under the new Data Space protocol. The TSG Connector is developed in Kotlin and built within Docker images. 

Already, a set of 15 connectors have been deployed within Enershare data space. 

**Technical functional and structural details**

Detailed technical information about the TSG Connector can be found in the following links: 

+ TNO Security Gateway Architecture & Documentation : **https://tno-tsg.gitlab.io/**
+ TSG Core Container : **https://gitlab.com/tno-tsg/core-container**
+ TSG Connector Helm Chart : **https://gitlab.com/tno-tsg/helm-charts/connector**
+ ENERSHARE Connectors : **https://daps.enershare.dataspac.es/#connectors**
+ IDS Connector : **https://docs.internationaldataspaces.org/ids-knowledgebase/v/ids-ram-4/layers-of-the-reference-architecture-model/3-layers-of-the-reference-architecture-model/3_5_0_system_layer/3_5_2_ids_connector**

The usage control functionality that is provided by TSG Connector and the individual components that perform it are presented in **section 5.2.2 in ENERSHARE deliverable D4.2 - "Enershare Trust and sovereignty building blocks (Beta version)"**.

The technical description of the communication and data exchange between a data provider’s TSG connector and a data consumer’s TSG connector (Policy negotiation) is presented in detail in **section 5.3.4 in the ENERSHARE deliverable D4.2**. The involved sub-components and the steps that are performed in order to communicate two TSG connectors are presented in a sequence diagram in the aforementioned section.


## Metadata Broker
The Metadata Broker is a core component of the Data Space as it is an IDS Connector which contains an endpoint for the registration, publication, maintenance, and query of connector self-descriptions. As such it is part of the ENERSHARE Data Space. Every connector participating in the project has its own “functionality catalogue” that contains its resource self-descriptions, according to the IDSA reference architecture. An IDSA connector can provide various resources, so the specific catalogue may include multiple self-descriptions. For a data consumer to locate specific resources across different connectors, it needs to query multiple catalogues, find the desired resources and then integrate the results.

**Description and Purpose**

The Metadata Broker operates like a centralized catalogue of resource self-descriptions within the ENERSHARE Data Space. Specifically, it provides a central access point to resource self-descriptions where data providers can register their services and themselves in a way that they are discoverable by Data consumers.

A Self-Description encapsulates information about IDS Connector itself and its capabilities and characteristics. This Self-Description contains information about the offered interfaces, the owner of the component and the metadata of the data offered by the component. A Self-Description is provided by the operator of the Connector. The Self-Description in total can be seen as metadata. 

The process that is followed to take advantage of the Metadata Broker is step-wise. 
1.As the first step, the data provider registers, publishes, and updates self-descriptions in the Metadata Broker. 
2.Following the publication, these self-descriptions are discovered by data consumers who make queries to the Metadata Broker. The self-descriptions contain the appropriate information for the Consumer to find the best matching and connect to the connector of the provider to consume the data.

---------------FUIGURE--------------

**Development Progress**

The TSG Metadata Broker is considered to be the best choice for the ENERSHARE Metadata Broker as one of individual components that allow a participant to be part of an IDS data space. The TSG Metadata Broker does not participate in the actual data exchange although is implemented as an IDSA Connector. The TSG Metadata Broker implements a Fuseki triple store backend to enable the SPARQL query functionality.


**Technical functional and structural details**

The Metadata Broker is a combination of a TSG Core Container and a Broker Data App. The Core Container serves as the hub of the IDS ecosystem and facilitates IDS messaging, message routing, artifact handling, container orchestration, policy enforcement, and embedded workflow management. The Broker Data App carries out the business logic for managing self-descriptions.

More information about the Metadata Broker processes and functionality can be found in the below links:

+ IDS Metadata Broker from IDSA RAM: **https://docs.internationaldataspaces.org/ids-ram-4/layers-of-the-reference-architecture-model/3-layers-of-the-reference-architecture-model/3_5_0_system_layer/3_5_4_metadata_broker https://gitlab.com/tno-tsg/broker/data-app/-/tree/master**
+ Gaia-X federated catalogue : **https://docs.gaia-x.eu/technical-committee/architecture-document/latest/federation_service/#federated-catalogue**

More information about the functionality of the Metadata Broker and his role in the overall architecture of ENERSHARE can be found in the **section 5.4 of the ENERSHARE deliverable D5.1 - “ ENERSHARE Data Value Stack (Alpha version)”**.

More information about the interfaces (description, “provided to”, End-point, protocol used and allowed methods) and the data exchange with other components are described in the **section 6.4 in the ENERSHARE deliverable D5.2 “ENERSHARE Data Value Stack (Beta version)”**.


## Identity Provider (CA + DAPS)
The ENERSHARE project follows the data space principles as they are described in OPENDEI initiatives. One of the technical building blocks for OPENDEI is the one which guarantees Trust among its users. Identity Management is extremely important for ensuring trust within a data space ecosystem. Specifically, Identity management enables authentication, identification and authorization among the participants of the data space.

**Description and Purpose**

ENERSHARE implements the Identity Provider component in order to handle the Identity management within the digital environment. Identity Provider is introduced within the IDSA Reference Architecture as one of its core components, which is responsible to perform the identity and access management. Specifically, the Identity Provider is an Intermediary that provides functionalities to create, manage, maintain and validate identity data of and for the participants. Additionally, the Identity Provider is composed of three sub-components, namely, the Certificate Authorities (CAS), the Dynamic Attribute Provisioning Service (DAPS) and the Participant Information Service (ParIS).






## Vocabulary Hub & Wizard for generation of Open APIs
text
## FIWARE Context Broker
text
## OpenAPI Interfaces
text
## Transformation Service
text
## Compliance Service
text
## Mashup Editor
text
## Semantic Models
text
## Marketplace
text
## Clearing House
text
## AppStore
text
## Blockchain & Notarisation Services


# True connector and side components
**test**
