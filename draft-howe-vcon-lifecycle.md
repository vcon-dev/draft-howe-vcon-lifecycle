---
title: "vCon Lifecycle Management using Transparency Services"
abbrev: "vCon Lifecycle"
category: std

docname: draft-howe-vcon-lifecycle-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date: 2026-02-25
consensus: true
v: 3
area: "Applications and Real-Time"
workgroup: "Virtualized Conversations"
keyword:
 - conversation
 - vcon
 - CDR
 - call detail record
 - call meta data
 - call recording
 - email thread
 - text conversation
 - video recording
 - video conference
 - conference recording
 - SCITT
 - transparency
venue:
  group: "Virtualized Conversations"
  type: "Working Group"
  mail: "vcon@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/vcon/"
  github: "howethomas/vcon-howe-scitt-lifecycle"
  latest: "https://howethomas.github.io/vcon-howe-scitt-lifecycle/draft-howe-vcon-lifecycle.html"

author:
 -
    fullname: Thomas McCarthy-Howe
    organization: VCONIC
    email: ghostofbasho@gmail.com
 -
    fullname: S. Lasker
    organization: independent
 -
    fullname: Diana James
    organization: Marashlian & Donahue, PLLC


normative:
  RFC2119:
  RFC8174:

  I-D.draft-ietf-vcon-vcon-core:
    target: https://datatracker.ietf.org/doc/draft-ietf-vcon-vcon-core/
    title: "The JSON format for vCon - Conversation Data Container"
    author:
      -
        ins: D. G Petrie
        name: Daniel G Petrie
        org: SIPez LLC
    date: January 2026
    seriesinfo:
      Internet-Draft: draft-ietf-vcon-vcon-core-02

  I-D.draft-ietf-scitt-architecture:
    target: https://datatracker.ietf.org/doc/draft-ietf-scitt-architecture/
    title: "An Architecture for Trustworthy and Transparent Digital Supply Chains"
    seriesinfo:
      Internet-Draft: draft-ietf-scitt-architecture

informative:
  CCPA:
    target: https://oag.ca.gov/privacy/ccpa
    title: "California Consumer Privacy Act"
    author:
      org: State of California
    date: 2018

  GDPR:
    target: https://gdpr.eu/
    title: "General Data Protection Regulation"
    author:
      org: European Union
    date: 2018

  I-D.draft-james-privacy-primer-vcon:
    target: https://datatracker.ietf.org/doc/draft-james-privacy-primer-vcon/
    title: "Privacy Primer for Virtual Conversations (vCons)"
    seriesinfo:
      Internet-Draft: draft-james-privacy-primer-vcon

  I-D.draft-howe-vcon-lawful-basis:
    target: https://datatracker.ietf.org/doc/draft-howe-vcon-lawful-basis/
    title: "vCon Lawful Basis"
    author:
      -
        ins: T. McCarthy-Howe
        name: Thomas McCarthy-Howe
        org: VCONIC
    seriesinfo:
      Internet-Draft: draft-howe-vcon-lawful-basis

  I-D.draft-howe-vcon-wtf-extension:
    target: https://datatracker.ietf.org/doc/draft-howe-vcon-wtf-extension/
    title: "vCon World Transcription Format Extension"
    author:
      -
        ins: T. McCarthy-Howe
        name: Thomas McCarthy-Howe
        org: VCONIC
    seriesinfo:
      Internet-Draft: draft-howe-vcon-wtf-extension

--- abstract

This document proposes using transparency systems such as SCITT (Supply Chain, Integrity, Transparency, and Trust) to manage the lifecycle of Virtual Conversations (vCons), which are standardized containers for conversational data like call recordings, transcripts, and chat logs.
While vCons enable capturing and sharing conversation details for AI analysis and business purposes, they lack mechanisms for proving compliance with privacy regulations and consent management.
Transparency systems such as SCITT address this by providing an immutable, append-only transparency logs that records key lifecycle events—from vCon creation and consent management to call recording, as well as data processing and deletion—enabling entities to demonstrate regulatory compliance and maintain trust across distributed systems.
The framework specifically addresses consent management challenges under regulations like GDPR and CCPA, where consent can be revoked at any time, requiring coordinated deletion across all parties that have received the vCon.
By combining vCons with transparency systems such as SCITT, organizations can build scalable, transparent governance systems that protect personal data rights while enabling responsible use of conversational data for AI and business applications.

--- middle

# Introduction

   Virtual Conversations (vCons) [I-D.draft-ietf-vcon-vcon-core] are powerful means of
   capturing and collaborating on the details of human conversations,
   built to travel.  They feed AI systems, enable entities to respond
   more accurately to customer needs, and manage the health of their
   business more effectively.  The vCon working group focuses on
   passing conversational data, such as data commonly generated and
   collected in business and security environments, from chat logs to
   transcripts to recordings.

   Most systems provide a way to store such information, but there are
   few standards or interoperability within the storage or transmission
   mechanisms.  vCon is a framework for capturing and collaborating on
   the details of a Virtual Conversation, feeding AI systems, and
   enabling entities to respond to customer needs more accurately and
   manage their business's health more effectively.

   The two opposing forces influencing such information passing are
   trying to enforce personal data and communications privacy and providing the ability and
   interest to use conversations in various ways, e.g., AI analysis.

   Although vCons are tools that enable actors to do the right thing,
   they are not tools that enable actors in a distributed system to
   prove it. However, when combined with transparency services like SCITT
   [I-D.draft-ietf-scitt-architecture], proof becomes practical. Transparency services like SCITT allow Relying Parties
   to obtain information pertinent to the lifecycle of a vCon in a
   "transparent" way. These services achieve this by having producers publish
   information in a Transparency Service, where Relying Parties can
   check the information.

These relying parties can then use this information to make decisions based on the current state and context of the vCon to account for changes in consent, updates in the accuracy of the content, or amendments of the information it might contain. Transparency services such as SCITT, the Supply Chain, Integrity, Transparency, and Trust protocol, enable clients to register statements about events, physical or virtual, such as when things are created or used. These statements are immutable and are useful to support auditing, governance, and coordination between various distributed systems.

When using vCons to define a conversation, and transparency services such as SCITT to record the
events that occur to them, more scalable and transparent systems of
governance and provenance can be constructed to support privacy
efforts.  It is expected that there are many situations where this
governance across security boundaries is common and desired by all
parties.  One real-world example of this is management of consent as
it applies to the use of conversations for different purposes, such as machine learning.  Using
conversations as inputs to machine learning has great benefit to both
customers and businesses, yet only responsibly within the defense of
personal data rights and compliance with personal data and communications privacy laws, united together
by consent. Although consent to a call recording or personal data collection and processing is not always required under the applicable laws, seeking consent is often the best practice, given the Privacy by Design principles, multijurisdictional business operations, and the ever-changing privacy laws. Please see the [I-D.draft-james-privacy-primer-vcon] for more information on consent and other data subject protection concepts.

In all of these cases, the ability to define and express the processing of conversations depends on the ability to authoritatively define the lifecycle of a vCon:

* who originated the vCon in the first place to establish provenance
* how it was analyzed and amended, to accurately respond to right-to-know requests
* the authenticity both of the original document for downstream workflow
* and authenticity of the redactions that come from the original, in service of data minimization efforts
* the various expressions of digital rights
* the sharing or deletion in response to the same digital rights

For this document and for purposes of illustration, consent will be used as an example. Proper consent management is fundamental to the responsible protection of data and the ability to leverage that data. Consent granted by the data subject of a vCon also needs to be stored and passed, exactly like the other information contained in a vCon. Unlike the rest of the information contained, the gathered consent is expressly not immutable. Consent, when gathered for a purpose, can also be revoked by the data subject at any time and surely after a vCon has been shared for analysis.

Multiple regulations, including the US-born California Consumer Protection Act (CCPA) [CCPA] and the EU-born General Data Protection Regulation (GDPR) [GDPR], outline requirements for entities to use and dispose of PII information responsibly upon request. Consent, although illustrative, is not the only example of mutability in the lifecycle of a vCon. Verification of parties, improvements in the analysis, and additions of contextual attachments result in updates to a vCon after data is shared, begging for a mechanism to track and govern such changes.

To honor the working group's charter to pass conversational data safely between consenting parties, this draft provides an overview of the requirements, a workflow and an example consent structure for using transparency services such as SCITT to manage the vCon lifecycle at scale, providing end-to-end, interoperable services and tooling. The workflow enables entities in the workflow to collaborate on a vCon while assuring all entities in the workflow adhere to relevant PII regulations using a transparency service ledger such as a SCITT Ledger. Actual implementations of these workflows are left to implementers and applications; this draft provides an authoritative list of the entries that should appear on the transparency service ledger to enable them.

## Acts of Trust and Transparency

Throughout this workflow, no single entity can prove that other entities performed the required actions. However, by auditing the transparency service ledgers of all involved parties, entities can prove they acted on the acknowledged consent and intent of the Data Subject, holding other entities accountable for performing required operations. In short, this audit can help to prove that "the good guys did the right thing", to measure the compliance of those outside this architecture who may have chosen different methods of compliance assurance.

## Standards-Based Interoperability

Virtual conversations benefit a wide range of industries and business scenarios. Their value lies in enabling cross-conversation collaboration. A standards-based approach lets both collaborators and competitors integrate readily with transcription [I-D.draft-howe-vcon-wtf-extension], consent management, and CRM systems.

Packaging conversations and associated metadata in the vCon format standardizes what is exchanged. Because vCons can contain PII and digital fingerprints, implementers must understand and comply with applicable PII regulations. A common standard provides stability for information management across the lifecycle.

Recording which vCon elements were sent to which parties establishes accountability for what was sent, what was received, and when the exchanges occurred.

## What Differentiates Transparency Services from a Database

The information written to transparency services such as SCITT could be compared to information in a standard database. What makes transparency services such as SCITT different:

* **Immutable and Append-Only nature**: Once written, data cannot be modified or deleted
* **Cryptographic security**: Through pre-signed statements, making transparency services such as SCITT a notary that cannot alter contents
* **Independent verifiability**: Parties can verify data without trusting the service provider
* **Separation**: Between the immutable, append-only ledger and the evidentiary metadata store (which can be deleted/redacted for PII governance)
* **Standardized communication**: And enforcement of regulations and compliance

# Conventions and Definitions

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
   "OPTIONAL" in this document are to be interpreted as described in BCP
   14 [RFC2119] [RFC8174] when, and only when, they appear in all
   capitals, as shown here.

The following terms, derived from [CCPA], [GDPR] and [I-D.draft-james-privacy-primer-vcon], are used throughout the document. For comprehensive privacy definitions and context, see [I-D.draft-james-privacy-primer-vcon].

**Conserver**: A vCon workflow engine that routes vCons for processing and enhancements; retrieves from and saves to a vCon Registry; does not persist vCons itself.

**Data Controller**: The entity that determines the purposes and means of processing and bears primary responsibility under privacy laws; typically enters into data processing agreements with Data Processors.

**Data Originator**: The entity that records and initiates the vCon, identifies parties and media, and has access to conversation content. Examples include phone numbers with audio recordings for phone calls, or emails with audio/video for internet-based calls (e.g., Microsoft Teams, Zoom, Google Meet).

**Data Processor**: An entity that processes personal data on behalf of the Data Controller (e.g., third-party providers). May subcontract; must operate within the controller's instructions. A Conserver may invoke processors for transcription, sentiment, fraud detection, or messaging.

**Data Subject**: The individual(s) whose personal information is processed (also called the "consumer" in many privacy laws).

**Entity**: A company, group, or individual that may share, alter, or use a vCon (e.g., Data Originator, Data Controller, Data Processor).

**Party**: A participant in a vCon, as identified in the vCon draft.

**Personal Data**: Information relating to an identified or identifiable Data Subject (e.g., name, identification number, location, online identifier, or factors tied to identity).

**Processing**: Any operation performed on personal data (e.g., collection, storage, use, disclosure, deletion).

**Transparency Service**: An append-only ledger (such as SCITT) that provides integrity protection for vCons and establishes state at a point in time for governance and regulatory conformance.

**vCon Registry**: A storage service capable of storing vCons, rich metadata, and large attachments (audio/video).

# vCon Lifecycle

## Example Use Case: Consent Management

The example use case, consent management, has the following requirements, all considered necessary to fulfill the proper sharing of personal information responsibly:

* As an individual, I wish to express my data subject rights to express my consent for various purposes, and to withdraw the same.
* As a member of an organization, I want to operationally assure that the processing of personal data is within the consent I gained from the data subject, and to safely record those activities to provide to both data subjects and governance bodies.
* As a regulator, I wish to have a measurement system to support compliance, bias and regulatory enforcement of policy.
* As a technologist, I wish to maintain the integrity of conversational pipelines, maintaining the trust both stakeholders and data subjects have in the trust and transparency of the process.

## vCon Lifecycle Scope

### Creation, Distribution and Deletion

The vCon lifecycle comprises a series of phases from creation through distribution to deletion. Tracking these phases enables fundamental privacy rights, such as the right to know how your data was processed, and secures AI supply chains by establishing provenance and guaranteeing integrity.

The phases of a vCon's life include:

~~~
+----------------+     +----------------+     +----------------+
| 1. vConCreated |---->| 2. Recording   |---->| 3. vConSent    |
|                |     |    Added       |     |                |
+----------------+     +----------------+     +----------------+
                                                      |
                                                      v
+----------------+     +----------------+     +----------------+
| 6. vConSentTo  |<----| 5. vConEnhanced|<----| 4. vConReceived|
|    Processors  |     |                |     |                |
+----------------+     +----------------+     +----------------+
        |
        v
+----------------+     +----------------+
| 7. Data        |---->| 8. vConDeletion|
|    Processing  |     |                |
+----------------+     +----------------+
~~~

1. **vConCreated**: The call completes, and a vCon is created with call metadata stored in the vCon Registry.
2. **RecordingAdded**: The actual recording is saved and added to the attachments section of the vCon.
3. **vConSent**: The Data Originator sends the vCon to the Data Controller with integrity protection using a transparency service such as SCITT. Unredacted vCons containing sensitive information MUST be encrypted during transmission to protect personally identifiable information, as outlined in [I-D.draft-james-privacy-primer-vcon] Section 3.
4. **vConReceived**: The Data Controller receives the vCon and records this in the Transparency Service.
5. **vConEnhanced**: The Data Controller adds transcription and license information and identifies themselves.
6. **vConSentToProcessors**: The Data Controller sends the vCon to relevant Data Processors. Encryption of vCons in transit is REQUIRED for protection of sensitive personal data.
7. **Data Processing**: Value-added services are performed on the vCon data.
8. **vConDeletion**: The vCon is deleted when no longer needed, when consent is revoked, or when it expires.

### Digital Rights Management

Interwoven with the vCon lifecycle is consent management.  A modern
consent model is envisioned: consent is gathered by the Data
Controller (or the Data Originator acting as a data processor on behalf of the Data Controller) for particular purposes (such as training or sharing) and
can be withdrawn by the Data Subject on demand.  This withdrawal may
result in revoking the vCon or modifying it to remove non-consenting
portions.


~~~
+------------------+     +------------------+     +------------------+
| 1. ConsentTo     |---->| 2. ConsentFor    |---->| 3. Consent       |
|    Record        |     |    Purpose       |     |    Recorded      |
+------------------+     +------------------+     +------------------+
                                                         |
                                                         v
+------------------+     +------------------+     +------------------+
| 6. RevokeRequest |<----| 5. ConsentReview |<----| 4. ConsentReceipt|
|    Processing    |     |    Revocation    |     |    Sent          |
+------------------+     +------------------+     +------------------+
~~~

Lifecycle events in Digital Rights Management include:

1. **ConsentToRecord**: Consent is requested from the Data Subject to record the conversation.
2. **ConsentForPurpose**: Confirmation of consent for specific purposes (e.g., "sales followup") is obtained.
3. **ConsentRecorded**: The Data Controller records where consent was confirmed in the transcript or recording.
4. **ConsentReceipt Sent**: Notification is sent to Data Subject(s) with a link to review consent details.
5. **ConsentReview/Revocation**: Data Subject can review or choose to revoke consent at any time.
6. **RevokeRequestProcessing**: If consent is revoked, the request is processed and communicated to all parties.

#### Multi-purpose Consent

Consent is often layered, with the Data Subject providing separate, independent consent for different purposes. For example, a Data Subject may consent to recording for "quality assurance" but not for "training AI models", or vice versa. The Data Subject can withdraw consent for specific purposes while maintaining consent for others.

~~~
Purpose 1: Quality Assurance
+------------------+     +------------------+
| Consent Granted  |---->| Consent Active   |
+------------------+     +------------------+
                              |
                              | Revoke for QA only
                              v
                         +------------------+
                         | Consent Revoked  |
                         | (QA only)        |
                         +------------------+

Purpose 2: AI Training (Independent)
+------------------+     +------------------+
| Consent Granted  |---->| Consent Active   |
+------------------+     +------------------+
                              |
                              | (Still active even if QA revoked)
                              v
                         +------------------+
                         | Consent Active   |
                         | (Training OK)    |
                         +------------------+
~~~

Multi-purpose consent management includes the following additional considerations:

1. **Purpose-Specific Consent**: Each purpose (e.g., "quality assurance", "training", "analytics") MUST have independent consent records that can be revoked individually.
2. **Partial Revocation**: When a Data Subject revokes consent for one purpose, it does not affect consent for other purposes.
3. **Consent Granularity**: Data Processors MUST track which purposes retain active consent and refuse processing for purposes where consent has been revoked.
4. **Audit Trail**: Each purpose-specific consent grant, review, and revocation MUST be recorded separately in the Transparency Service to enable compliance verification.

For more information on consent management and data subject rights, refer to [I-D.draft-james-privacy-primer-vcon].

### Amendment of Existing vCons

Under normal circumstances, vCons may be amended. For example, at creation time, parties to a vCon may be verified through methods such as OAuth. However, if account credentials are later found to be compromised, the verification status may need revision. Party verification issues often trigger "Rights to Correct" requests and are fundamental to responsible data rights management. Other enhancements and modifications may occur for security reasons, future processing needs, or in response to regulatory changes.

~~~
+----------------+     +----------------+     +----------------+
| 1. DialogAdded |---->| 2. vConProcessed|---->| 3. Data       |
|                |     |                |     |    Redaction   |
+----------------+     +----------------+     +----------------+
~~~

Events that may be recorded on the distributed ledger include:

1. **DialogAdded**: A dialog is saved and added to the vCon.
2. **vConProcessed**: The Data Controller processes the vCon.
3. **Data Redaction**: Data Processors delete the data or redact the Data Subject.

### Breach Response and Notification

A data breach occurs when personal data is accessed, disclosed, or lost in an unauthorized manner. Upon discovery of a breach, entities must follow a coordinated response process to notify affected Data Subjects and regulators in accordance with applicable privacy laws. The breach response lifecycle ensures timely detection, investigation, notification, and remediation.

~~~
+----------------+     +----------------+     +----------------+
| 1. Breach      |---->| 2. Breach      |---->| 3. Subject     |
|    Detected    |     |    Investigation|     |    Notified    |
+----------------+     +----------------+     +----------------+
                                                      |
                                                      v
+----------------+     +----------------+     +----------------+
| 6. Remediation |<----| 5. Regulator   |<----| 4. Regulator   |
|    Completed   |     |    Notified    |     |    Notification|
+----------------+     +----------------+     +----------------+
~~~

Breach Response Lifecycle events include:

1. **vcon_breach_detected**: A data breach affecting one or more vCons is discovered. The entity discovering the breach records the detection timestamp and initial scope assessment.
2. **vcon_breach_investigated**: The breach is investigated to determine scope, affected Data Subjects, and cause. Investigation details are recorded on the Transparency Service.
3. **vcon_subject_notified**: Data Subject(s) are notified of the breach as required by applicable law (typically within 72 hours of discovery for GDPR).
4. **vcon_regulator_notified**: Regulatory authorities are notified of the breach if required by applicable law.
5. **vcon_remediated**: Remediation actions are completed, which may include deletion of compromised vCons, revocation of affected consent records, or other corrective measures.

All breach response events MUST be recorded in the Transparency Service to establish a complete audit trail demonstrating compliance with breach notification requirements, as outlined in [I-D.draft-james-privacy-primer-vcon].

### AI Training and Processing

Artificial Intelligence applications increasingly utilize vCons for training machine learning models and performing inference on conversational data. This processing must be subject to rigorous consent verification, data governance, and human oversight as outlined in privacy regulations such as the EU AI Act. The AI processing lifecycle ensures that all training data and inferences are authorized, tracked, and auditable.

~~~
+----------------+     +----------------+     +----------------+
| 1. Training    |---->| 2. Training    |---->| 3. Training    |
|    Data        |     |    Initiated   |     |    Completed   |
|    Prepared    |     |                |     |                |
+----------------+     +----------------+     +----------------+
                                                      |
                                                      v
+----------------+     +----------------+     +----------------+
| 6. Inference   |<----| 5. Model       |<----| 4. Model       |
|    Performed   |     |    Deployed    |     |    Validated   |
+----------------+     +----------------+     +----------------+
~~~

AI Training and Processing Lifecycle events include:

1. **vcon_training_prepared**: vCons are prepared for use in AI model training. This includes verification that consent for "training" or "AI processing" purposes is present in all selected vCons, application of data minimization principles, and creation of training datasets. The preparation event records which vCons were included, what consent purposes were verified, and any redactions or anonymization applied.
2. **vcon_model_training_initiated**: AI model training begins using prepared vCons. The event records the model type, purpose (e.g., sentiment analysis, transcription improvement), training parameters, and reference to the training dataset prepared in the previous step.
3. **vcon_model_training_completed**: AI model training completes. The event records model version, accuracy metrics, training duration, and any data quality issues encountered.
4. **vcon_model_validated**: The trained model is validated against test datasets and quality thresholds. Human review and approval of model behavior is documented, particularly for high-risk use cases.
5. **vcon_model_deployed**: The validated model is deployed to production. The event records deployment timestamp, version, and applicable constraints (e.g., acceptable use cases, geographic restrictions).
6. **vcon_inference_performed**: The deployed model performs inference on a vCon. Inference events record the model version used, input vCon identifier, inference results, confidence scores, and whether the results were acted upon or stored.

All AI processing events MUST be recorded in the Transparency Service with particular attention to documenting consent verification, data governance practices, human oversight, and compliance with the EU AI Act or other applicable AI regulations, as discussed in [I-D.draft-james-privacy-primer-vcon] Section 2.5.

# Detailed Use Case

## vCon Create, Consent and Share

~~~
    +-------------------+                      +-------------------+
    |  Data Originator  |                      |  Data Controller  |
    +---------+---------+                      +---------+---------+
              |                                          |
              | 1. Call Initiation                       |
              |-------->                                 |
              |                                          |
              | 2. Consent to Record                     |
              |-------->                                 |
              |                                          |
              | 3. Consent to Share                      |
              |-------->                                 |
              |                                          |
              | 4. vCon Created                          |
              |                                          |
              | 5. Recording Added                       |
              |                                          |
              | 6. vCon Sent                             |
              |----------------------------------------->|
              |                                          |
              |                                          | 7. vCon Received
              |                                          |
              |                                          | 8. vCon Enhanced
              |                                          |
              |                                          | 9. vCon Sent
              |                                          |-------->
              |                                          |
              |                                          |
    +---------v---------+                      +---------v---------+
    |  Data Originator  |                      |  Data Controller  |
    +-------------------+                      +-------------------+
                                                        |
                                                        v
                                               +-------------------+
                                               |  Data Processor   |
                                               +---------+---------+
                                                         |
                                                         | 10. vCon Received
                                                         |
                                                         | 11. Consent Recorded
                                                         |
                                                         | 12. vCon Enhanced
                                                         |
                                                         | 13. Consent Receipt
                                                         |    Sent
                                                         |
                                                         | 14. Consent Review
                                                         |
                                                         | 15. Value-Add
                                                         |    Services
                                                         |
                                               +---------v---------+
                                               |  Data Processor   |
                                               +-------------------+

### Data Originator

1. **Initiating Call**: An initiating caller contacts a Data Subject to provide a service.
2. **Consent to Record**: The initiating caller requests consent to record the call for training purposes.
3. **Consent to Share**: The call completes, confirming consent for
the recording to be used for "sales followup", noting that the
Data Subject can review and revoke consent later. Depending on the types of personal data communicated on the call and the purpose of its processing, the consent request language may need to include additional information.
4. **vCon Created**: The call completes, the vCon is created, and call metadata is recorded in the vCon Registry.
5. **Recording Added**: The recording is saved to the vCon Registry, adding it to the vCon's attachments section.
6. **vCon Sent**: The Data Originator completes their responsibilities and sends the vCon to the Data Controller.

### Data Controller

1. **vCon Received**: The vCon is received from the Data Originator, and a vcon_received operation is recorded in the Transparency Service.
2. **vCon Enhanced with License and Data Controller**: The Data Controller adds transcription, specifies the intended license, and identifies themselves as the Data Controller on the vCon.
3. **vCon Sent**: The Data Controller sends the vCon to the Data Processor(s).

When sending vCons to Data Processors, the Data Controller is responsible for ensuring that all recipients operate under data processing agreements that align with the Data Controller's obligations under applicable privacy laws. If a Data Processor subcontracts with other processors, the Data Controller remains accountable for those subcontractors' compliance with data protection requirements. All Data Processors in the chain must record their receipt and processing of the vCon on the Transparency Service, creating a verifiable chain of custody and responsibility. For more information on processor responsibilities and chains of responsibility, refer to [I-D.draft-james-privacy-primer-vcon].

### Data Processor(s)

1. **vCon Received**: The Data Processor validates the vCon's transparency service receipt from the Data Controller.
2. **Consent Recorded**: The Data Processor records consent confirmation in the Transparency Service.
3. **vCon Enhanced**: Sentiment analysis and other enhancements are processed through the Data Processor's Conserver workflows.
4. **Consent Receipt Sent**: The Data Processor sends notification to the Data Subject(s) with a link to review consent details.
5. **Consent Review**: The Data Subject(s) can review vCon information at any time and revoke consent if desired.
6. **Data Processor Value-Add**: The Data Processor performs value-added services for the Data Subject(s).

## Revocation and the Right to Be Forgotten

At any point, a Data Subject can request revocation or the right to be forgotten, requiring all vCon possessors to act accordingly. vCons must be tracked for where they were sent and who to contact when a Data Subject makes such requests. The Transparency Service maintains metadata about ingested vCons, ensuring integrity and inclusion protection.

~~~
    +-------------------+                      +-------------------+
    |   Data Subject    |                      |  Data Controller  |
    +---------+---------+                      +---------+---------+
              |                                          |
              | 1. Revoke Consent                        |
              |-------->                                 |
              |                                          |
              | 2. Revoke Request Sent                   |
              |----------------------------------------->|
              |                                          |
              |                                          | 3. Act on Revocation
              |                                          |
              |                                          | 4. Send Request to
              |                                          |    All Processors
              |                                          |-------->
              |                                          |
    +---------v---------+                      +---------v---------+
    |   Data Subject    |                      |  Data Controller  |
    +-------------------+                      +-------------------+
                                                        |
                                                        v
                                               +-------------------+
                                               |  Data Processor   |
                                               +---------+---------+
                                                         |
                                                         | 5. Deletion of Data
                                                         |
                                               +---------v---------+
                                               |  Data Processor   |
                                               +-------------------+
~~~

### Data Subject

1. **Revoke Consent**: The Data Subject revokes consent by some manner: i.e. clicks a link included in all communications between the Data Processor and the Data Subject(s), through an external system or in conversation with the data controller.
2. **Revoke Request Sent**: If the vcon_consent_revoked operation was handled by the Data Processor, they MUST contact the Data Controller to communicate the Data Subject's intent.

### Data Controller Revocation

1. **Act on Consent Revocation Request**: The Data Controller receives the vCon Consent Revocation Request and records it on their Transparency Service.
2. **Send Revocation Request to Data Controllers**: If the vCon was sent to other Data Processors, they must communicate the revocation request to any Data Processor that hasn't yet acknowledged it.

### Data Processor Revocation

1. **Deletion of Data**: Any Data Processor that hasn't yet acted on the request must acknowledge it.


## Breach Response Workflow

A breach response workflow demonstrates how entities coordinate to detect, investigate, notify, and remediate data breaches affecting vCons. This workflow illustrates the critical role of the Transparency Service in establishing an audit trail of breach-related actions.

~~~
    +-------------------+                      +-------------------+
    |  Data Subject     |                      |  Data Controller  |
    +---------+---------+                      +---------+---------+
              |                                          |
              | 1. Breach Discovered                     |
              |-------->                                 |
              |                                          |
              |                                          | 2. Investigate
              |                                          |
              |                                          | 3. Record on
              |                                          |    Transparency Service
              |                                          |
              | 4. Notification Sent                     |
              |<----------------------------------------|
              |                                          |
              |                                          | 5. Notify Regulators
              |                                          |
    +---------v---------+                      +---------v---------+
    |  Data Subject     |                      |  Data Controller  |
    +-------------------+                      +-------------------+
                                                        |
                                                        v
                                               +-------------------+
                                               |  Regulatory Body  |
                                               +---------+---------+
                                                         |
                                                         | 6. Confirm Receipt
                                                         |
                                               +---------v---------+
                                               |  Regulatory Body  |
                                               +-------------------+
~~~

### Breach Discovery and Investigation

1. **Breach Discovered**: A breach is discovered through monitoring systems, security alerts, or report from a Data Subject. The discovering entity records the breach detection on the Transparency Service with timestamp, initial scope, and affected data categories.

2. **Investigation Initiation**: The Data Controller initiates a formal investigation to determine the scope of the breach, which vCons are affected, which Data Subjects are impacted, and the cause of the breach.

3. **Scope Documentation**: Investigation findings are recorded on the Transparency Service, including list of affected vCons, count of impacted Data Subjects, data categories involved, and preliminary cause assessment.

### Notification Process

1. **Data Subject Notification**: Within required timeframes (72 hours for GDPR), Data Subjects are notified of the breach. Notification includes description of the breach, data affected, recommended protective actions, and contact information for questions.

2. **Regulatory Notification**: Depending on breach scope and jurisdiction, regulatory authorities are notified. Event is recorded on Transparency Service showing regulatory body, notification timestamp, and compliance with applicable timelines.

3. **Processor Notification**: If vCons were shared with Data Processors, each Processor is notified and must acknowledge receipt and initiate their own breach response procedures.

### Remediation

1. **Remediation Actions**: Remediation may include deletion of compromised vCons, revocation of consent records, password resets, notification of related parties, or other corrective measures. Each action is recorded on the Transparency Service.

2. **Audit Trail Completion**: All breach-related events form a complete, immutable audit trail on the Transparency Service demonstrating compliance with regulatory requirements and proving that the good actors took appropriate action.

## AI Training and Processing Workflow

An AI training and processing workflow demonstrates how organizations prepare vCons for machine learning, execute training with proper consent verification and governance, deploy models safely, and audit inference results.

~~~
    +-------------------+                      +-------------------+
    |  Data Controller  |                      |  AI Operations    |
    +---------+---------+                      +---------+---------+
              |                                          |
              | 1. Training Data Selection                |
              |-------->                                 |
              |                                          |
              | 2. Consent Verification                  |
              |-------->                                 |
              |                                          |
              |                                          | 3. Data Redaction
              |                                          |    (if needed)
              |                                          |
              |                                          | 4. Training Dataset
              |                                          |    Created
              |                                          |
              |                                          | 5. Model Training
              |                                          |    Initiated
              |                                          |
              |                                          | 6. Training
              |                                          |    Completed
              |                                          |
              | 7. Model Review & Approval               |
              |<----------------------------------------|
              |                                          |
              | 8. Deployment Approval                   |
              |-------->                                 |
              |                                          |
    +---------v---------+                      +---------v---------+
    |  Data Controller  |                      |  AI Operations    |
    +-------------------+                      +-------------------+
                                                        |
                                                        v
                                               +-------------------+
                                               |  Production       |
                                               |  Inference        |
                                               +-------------------+
~~~

### Training Data Preparation

1. **Dataset Selection**: The Data Controller selects vCons for use in training based on business requirements (e.g., sentiment analysis, transcription accuracy improvement).

2. **Consent Verification**: For each selected vCon, the Data Controller verifies that consent for "training" or "AI processing" purposes is active and has not been revoked. Revocation of consent for this specific purpose excludes the vCon from the training dataset.

3. **Data Preparation**: Data minimization principles are applied. vCons are redacted to remove unnecessary PII, transcriptions are normalized, and metadata is prepared. All preparation steps are recorded on the Transparency Service.

4. **Dataset Creation**: A training dataset is created with records of which vCons were included, what consent purposes were verified, and what redactions or anonymization was applied.

### Model Training and Validation

1. **Training Initiated**: AI model training begins using the prepared dataset. The event records model type, intended purpose, training parameters, and reference to the dataset.

2. **Training Completed**: Training finishes. The event records model version, performance metrics, training duration, and any data quality observations.

3. **Model Review**: Human reviewers assess model performance, fairness, and bias. For high-risk use cases (as defined in privacy regulations), comprehensive human review is required.

4. **Model Validation**: The model is validated against held-out test data and quality thresholds. Validation results, including accuracy, precision, recall, and fairness metrics, are recorded on the Transparency Service.

### Deployment and Inference

1. **Deployment Approval**: After successful validation and human review, deployment is approved by the Data Controller.

2. **Model Deployed**: The model is deployed to production with constraints documented (acceptable use cases, geographic restrictions, refresh schedules).

3. **Inference Performed**: When new vCons are processed by the deployed model, inference events are recorded on the Transparency Service, including model version, confidence scores, and whether results were used for business decisions.

4. **Consent Monitoring**: Throughout inference, the system continues to check whether the vCon's consent status permits AI processing. If consent is revoked, future inferences on that vCon MUST cease.

5. **Audit Trail**: All training, validation, and inference events create an immutable audit trail demonstrating compliance with data governance, consent verification, and human oversight requirements as required by the EU AI Act and similar regulations.

# vCon Lifecycle Events

The following events outline important "moments that matter" in a vCon's lifecycle. These events are not intended to be stored within the vCon itself, but rather as operations stored on transparency services such as SCITT to provide context for the vCon's intent at specific points in time:

* **vcon_created**: The initial vCon document as first recorded. The vCon may start with a basic structure defining minimal metadata, as recordings or attachments may be added asynchronously upon encoding completion.

* **vcon_enhanced**: The vCon has been amended or appended. While vCons are considered immutable, information may be amended or appended—previous values exist in the vCon Registry but may be superseded. Amendments may include transcription corrections or consent changes.

* **vcon_sent**: The vCon was sent to an external party. This operation seals the vCon's integrity, recording what was sent, to whom, and when in the Transparency Service. A transparency service receipt from the receiving service confirms possession.

* **vcon_received**: The vCon was received from an external entity. This documents possession at a specific time, sealing content integrity and returning a transparency service receipt to the sender.

* **vcon_consent_accepted**: One or more parties have consented to the vCon being recorded and shared for its intended purpose. Consent may not be established during initial vCon creation, as the Data Controller, not the Data Originator (infrastructure provider), is responsible for managing Data Subject consent.

* **vcon_consent_revoked**: One or more parties have revoked consent for one or more purposes. Depending on region, license, and regulatory requirements, one revocation may or may not require all Data Processors to act. For multi-purpose consent, individual purpose-specific consent can be revoked while maintaining consent for other purposes.

* **vcon_party_redacted**: A party to the vCon has been redacted. This differs from consent revocation, as the vCon may remain viable if a party's information can be redacted while maintaining integrity and usefulness.

* **vcon_deleted**: The vCon has been deleted due to an implicit act such as revocation or no longer being needed. When a Data Controller deletes a vCon, they must inform all recipients to either delete it or assume Data Controller responsibilities.

* **vcon_expired**: The vCon has expired due to license terms or compliance requirements. This triggers deletion and notification to all shared entities.

* **vcon_rcvr_purged**: When a vCon is sent from a Data Controller, the receiving Entity may maintain it indefinitely, for a set period, or delete it upon operation completion. If the Entity no longer needs to maintain the vCon, they can delete it and notify the sender.

* **vcon_breach_detected**: A data breach affecting one or more vCons is discovered and reported to the Transparency Service. The event records the detection timestamp, initial scope assessment, affected data categories, and the entity that discovered the breach.

* **vcon_breach_investigated**: Investigation of the breach is conducted to determine full scope, which vCons are affected, which Data Subjects are impacted, and root cause. Investigation findings are recorded on the Transparency Service with complete details of the breach impact.

* **vcon_subject_notified**: Data Subjects affected by a breach are notified in accordance with applicable law (e.g., within 72 hours of discovery for GDPR). The event records notification timestamp, notification method, content delivered, and confirmation of receipt where applicable.

* **vcon_regulator_notified**: Regulatory authorities are notified of the breach as required by applicable law. The event records the regulatory body notified, notification timestamp, and compliance with applicable notification timelines.

* **vcon_remediated**: Remediation actions for a breach are completed. These may include deletion of compromised vCons, revocation of affected consent records, password resets, or other corrective measures. The event records remediation actions taken and completion timestamp.

* **vcon_training_prepared**: vCons are prepared for use in artificial intelligence training. The event records consent verification for "training" or "AI processing" purposes, data minimization and redaction steps applied, and creation of the training dataset with reference to included vCons.

* **vcon_model_training_initiated**: AI model training begins using prepared vCons. The event records model type, intended purpose, training parameters, algorithm, and reference to the training dataset.

* **vcon_model_training_completed**: AI model training finishes successfully. The event records model version, performance metrics (accuracy, loss, etc.), training duration, and any data quality or ethical concerns encountered.

* **vcon_model_validated**: The trained model is validated against held-out test data and quality thresholds. For high-risk AI use cases, human review and approval are documented. The event records validation results, fairness metrics, bias assessments, and human review outcomes.

* **vcon_model_deployed**: The validated model is deployed to production. The event records deployment timestamp, model version, deployment environment, applicable constraints (acceptable use cases, geographic restrictions), and human approval.

* **vcon_inference_performed**: The deployed model performs inference on a vCon, generating analysis or predictions. The event records model version used, input vCon identifier, inference results, confidence scores, and whether the inference was acted upon or stored.

# Security Considerations

The security of the vCon lifecycle depends heavily on the integrity and availability of the Transparency Service. Entities MUST ensure that their transparency service implementations (such as SCITT) are properly secured and that access controls are in place to prevent unauthorized modifications.

The handling of personally identifiable information (PII) throughout the vCon lifecycle requires careful consideration of privacy regulations and data protection requirements. Entities MUST implement appropriate technical and organizational measures to protect PII and ensure compliance with applicable regulations.

## Breach Detection and Response Security

Organizations utilizing vCons MUST implement robust monitoring systems to detect unauthorized access, disclosure, or loss of vCons. Upon detection of a suspected breach, entities MUST:

* Record the breach detection immediately on the Transparency Service to establish an immutable audit trail.
* Conduct a prompt investigation to determine scope, affected Data Subjects, and root cause.
* Notify affected Data Subjects within applicable legal timelines (e.g., 72 hours for GDPR).
* Notify regulatory authorities as required by applicable law.
* Document all breach response actions on the Transparency Service to demonstrate compliance.

Complete breach response procedures and regulatory requirements are detailed in [I-D.draft-james-privacy-primer-vcon] Section 2.2.2.

## Artificial Intelligence Security Considerations

When utilizing vCons for AI training or inference, organizations MUST implement additional security and governance measures:

* **Consent Verification**: Before using vCons for training datasets, systems MUST verify that active consent for "training" or "AI processing" purposes exists and has not been revoked. Verification results MUST be recorded on the Transparency Service.

* **Data Minimization**: Training datasets MUST apply strict data minimization principles, removing or redacting unnecessary PII. All redactions and anonymization steps MUST be documented.

* **Model Governance**: All AI models MUST undergo human review, fairness assessment, and bias evaluation before deployment. For high-risk use cases, comprehensive human oversight is required as outlined in the EU AI Act and similar regulations.

* **Inference Monitoring**: After deployment, inference events MUST be recorded on the Transparency Service with model version, confidence scores, and whether results influenced business decisions. If consent is revoked after training, the system MUST cease performing inferences on affected vCons.

* **Audit Trail**: Complete AI processing workflows (preparation, training, validation, deployment, inference) MUST be recorded on the Transparency Service to enable compliance audits and investigations.

For detailed information on AI governance, risk mitigation, and compliance with emerging AI regulations, see [I-D.draft-james-privacy-primer-vcon] Section 2.5.

# Privacy Considerations

This document describes a framework for managing vCons that contain personally identifiable information. Implementers MUST ensure compliance with applicable privacy regulations, including but not limited to GDPR [GDPR] and CCPA [CCPA].

The framework provides mechanisms for consent management and data subject rights, but implementers are responsible for ensuring that their implementations properly respect and enforce these rights.

## Multi-purpose Consent Management

The framework supports multi-purpose consent, where Data Subjects provide separate, independent consent for different processing purposes. Implementers MUST:

* Track consent on a per-purpose basis, enabling independent grant and revocation of consent for different purposes (e.g., "quality assurance", "AI training", "analytics").
* Ensure that revocation of consent for one purpose does not affect consent for other purposes.
* Provide Data Subjects with granular control over their consent, allowing them to opt-in or opt-out of specific purposes independently.
* Record each purpose-specific consent grant, review, and revocation separately on the Transparency Service for compliance verification.
* Refuse processing for any purpose where active consent has not been obtained or has been revoked.

For comprehensive information on consent as a fundamental privacy right, see [I-D.draft-james-privacy-primer-vcon] Section 2.2.2.

## Artificial Intelligence and Privacy

When vCons are used in AI applications, privacy considerations are amplified due to the sensitive nature of conversational data and the potential for algorithmic bias or discriminatory outcomes.

* **Data Governance**: AI training datasets MUST be subject to rigorous data governance practices, including verification of lawful basis [I-D.draft-howe-vcon-lawful-basis], consent verification, and documentation of data sources and usage.

* **Bias and Fairness**: AI models trained on vCon data MUST be evaluated for bias and fairness impacts across demographic groups to prevent discriminatory outcomes. Human review and fairness testing are essential before deployment.

* **Transparency**: Organizations MUST be transparent with Data Subjects about the use of their conversational data in AI systems, including what inferences are being performed and how results may influence business decisions.

* **Human Oversight**: Particularly for high-risk AI use cases, human oversight of model training, validation, and inference is required to ensure that the system operates as intended and does not produce harmful outcomes.

* **Compliance with AI Regulations**: Organizations must comply with emerging AI regulations such as the EU AI Act, which establishes risk-based requirements for AI use cases. See [I-D.draft-james-privacy-primer-vcon] Section 2.5 for detailed discussion of AI-specific privacy and governance considerations.

* **Audit and Accountability**: All AI processing steps must be recorded on the Transparency Service to enable compliance audits and to demonstrate accountability to regulators and affected Data Subjects.

# IANA Considerations

This document has no IANA actions.

{backmatter}

# Acknowledgments

* Thank you to Allistair Woodman for connecting the first dots between VCon and SCITT
* Thank you to Jeff Pulver and Cody Launius for their collaboration and support

