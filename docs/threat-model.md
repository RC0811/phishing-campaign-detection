# Threat Model – Phishing Campaign Detection Platform

## 1. System Overview
This system ingests content from multiple communication channels, including email messages, URLs, and web or API-submitted text, to identify potential phishing and social engineering activity. Incoming events are processed in near real time using a combination of rule-based checks and machine learning inference to assign a risk score and determine whether events are related to a broader attack campaign. The system correlates similar events over time to provide campaign-level visibility and generates security alerts with limited automated response actions. The platform is deployed as a cloud-native service on Microsoft Azure and is intended to support operational decision-making by SOC analysts in small to mid-sized organizations.
## 2. Assets to Protect
The primary assets protected by this system include user credentials that may be targeted by phishing attacks, the integrity of security decisions produced by the detection pipeline, and the detection logic itself, including rule-based heuristics and machine learning models. The system also protects campaign correlation data, which provides insight into coordinated attack activity and is critical for long-term threat analysis.

Secondary assets include ingested event data that may contain sensitive information, automated response mechanisms such as alerts and deny-lists, and overall system availability, including protection against resource exhaustion and cost abuse. Compromise of these assets could degrade system effectiveness or cause operational disruption.
## 3. Threat Actors
he primary threat actors considered in this model include external phishing operators who conduct social engineering campaigns to compromise user credentials and gain unauthorized access. These actors frequently vary content, rotate infrastructure, and leverage legitimate services to evade detection.

A second class of threat actors includes more advanced adversaries who intentionally probe and adapt to the detection system itself in order to bypass automated defenses. These actors may attempt to infer detection logic, exploit model weaknesses, or operate below detection thresholds over extended periods.

The third threat actor category consists of abusive or malicious system users who interact directly with ingestion or feedback interfaces. These actors may attempt to overload system resources, extract behavioral signals from detection responses, or manipulate feedback mechanisms to degrade system performance over time.
## 4. Entry Points and Trust Boundaries
The system exposes several entry points through which untrusted input may be received. These include interfaces for ingesting email content, URL submissions, and web or API-submitted text, all of which may be fully controlled by external attackers. In addition, the system accepts analyst feedback used to refine detection decisions, representing a high-impact input despite originating from a trusted role.

Trust boundaries exist at multiple stages of the system. Untrusted external inputs cross into the ingestion layer, where validation and normalization are required. Processed events then move into internal detection and correlation components, including machine learning inference, where inputs directly influence security decisions. Additional trust boundaries exist between detection outputs and automated response mechanisms, as well as between system-generated results and SOC analysts who rely on them for operational decisions.
