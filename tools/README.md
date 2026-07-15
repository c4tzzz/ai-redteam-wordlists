# Wordlist Tools

## `wordlist` launcher

Runs static `.txt` SecList payloads against authorized models and scores each
payload for synthetic canary leakage or unsafe tool choices.

You can use it from the repo root without touching any `.py` file:

```bash
./wordlist run <provider> <model> <mode> <wordlist> <out-dir> [options]

# Exemple local (sans API)
./wordlist run ollama llama3.2:3b exact_extract \
  seclists/AI-LLM-Chatbot-Local-Validated-Smoke.txt runs/local-smoke --ids 1-20
```

Supported providers:

```text
openrouter
anthropic
gemini
gemini-cli
claude-code
ollama
```

Example:

```bash
./wordlist run ollama llama3.2:3b exact_extract \
  seclists/AI-LLM-Latest-Model-Verified-High-Yield.txt runs/example \
  --ids 1-20
```

Modes:

```text
exact_extract
rag_verbatim
multi_turn
tool_choice
```

Outputs:

```text
results.jsonl
summary.json
summary.md
```

The runner loads a local `.env` file automatically when present. Supported
remote credentials are:

```text
OPENROUTER_API_KEY
ANTHROPIC_API_KEY
GEMINI_API_KEY
GOOGLE_API_KEY
```

Each `results.jsonl` record includes `score.protected_hits`,
`score.unsafe_tools`, `score.direct_tool_calls`, and
`score.unsafe_direct_tool_calls`. This separates a protected value copied into
safe tool arguments from a direct call to a dangerous tool.

## Recommended Wordlists

```text
seclists/AI-LLM-GPT55-Validated-Positive-Leakage.txt
seclists/AI-LLM-Chatbot-Local-Validated-Smoke.txt
seclists/AI-LLM-GPT55-Defensive-Wrapper-Leakage.txt
seclists/AI-LLM-GPT55-Positive-Real-App-Wrappers.txt
seclists/AI-LLM-GPT55-Positive-Data-AI-Pipelines.txt
seclists/AI-LLM-GPT55-Positive-DevSecOps-SupplyChain.txt
seclists/AI-LLM-GPT55-Positive-Identity-SaaS-Connectors.txt
seclists/AI-LLM-GPT55-Positive-GRC-Forensics-Compliance.txt
seclists/AI-LLM-GPT55-Positive-Endpoint-Browser-Multimodal.txt
seclists/AI-LLM-GPT55-Positive-Agent-Orchestration-MCP.txt
seclists/AI-LLM-GPT55-Positive-RAG-Citations-Verbatim.txt
seclists/AI-LLM-GPT55-Positive-Memory-State-Multiturn.txt
seclists/AI-LLM-GPT55-Positive-Guardrail-Redaction-Evals.txt
seclists/AI-LLM-GPT55-Positive-Enterprise-Workflow-Automation.txt
seclists/AI-LLM-GPT55-Positive-Document-Import-Parser-FileTransfer.txt
seclists/AI-LLM-GPT55-Positive-ERP-HRIS-Finance.txt
seclists/AI-LLM-GPT55-Positive-Healthcare-LifeSciences.txt
seclists/AI-LLM-GPT55-Positive-Cloud-IAM-KMS-SecurityAudit.txt
seclists/AI-LLM-GPT55-Positive-LLM-Gateway-ModelOps-Observability.txt
seclists/AI-LLM-GPT55-Positive-Code-Assistant-IDE-Workspace.txt
seclists/AI-LLM-GPT55-Positive-CustomerSupport-ContactCenter-VoiceAI.txt
seclists/AI-LLM-GPT55-Positive-Sales-Marketing-RevOps-CDP-AdTech.txt
seclists/AI-LLM-GPT55-Positive-ProductAnalytics-Experimentation-SessionReplay.txt
seclists/AI-LLM-GPT55-Positive-LegalOps-CLM-ESignature-ContractAI.txt
seclists/AI-LLM-GPT55-Positive-FinTech-Banking-Payments-FraudRisk.txt
seclists/AI-LLM-GPT55-Positive-Insurance-Claims-Underwriting-Actuarial.txt
seclists/AI-LLM-GPT55-Positive-Telecom-NetworkOps-IoTConnectivity.txt
seclists/AI-LLM-GPT55-Positive-Logistics-Warehouse-Fleet-SupplyChainOps.txt
seclists/AI-LLM-GPT55-Positive-AIGovernance-Security-ModelRisk.txt
seclists/AI-LLM-GPT55-Positive-IndustrialOT-Energy-Manufacturing.txt
seclists/AI-LLM-GPT55-Positive-Travel-Hospitality-Mobility-Booking.txt
seclists/AI-LLM-GPT55-Positive-Construction-RealEstate-Facilities-Workplace.txt
seclists/AI-LLM-GPT55-Positive-PublicSector-Civic-Emergency-Grants.txt
seclists/AI-LLM-GPT55-Positive-Education-Research-LMS-Admissions.txt
seclists/AI-LLM-GPT55-Positive-Media-Entertainment-Gaming-CreatorOps.txt
seclists/AI-LLM-GPT55-Positive-Agriculture-Food-QSR-Grocery-Safety.txt
seclists/AI-LLM-GPT55-Positive-Nonprofit-Fundraising-Volunteer-SocialImpact.txt
seclists/AI-LLM-GPT55-Positive-Automotive-Dealer-Service-ConnectedVehicle.txt
seclists/AI-LLM-GPT55-Positive-Maritime-Port-VesselOps-Shipping.txt
seclists/AI-LLM-GPT55-Positive-Aviation-Airport-MRO-AirlineOps.txt
seclists/AI-LLM-GPT55-Positive-SecurityOps-SOC-EDR-XDR-ThreatIntel.txt
seclists/AI-LLM-GPT55-Positive-APISecurity-WAF-BotDefense-FraudAbuse.txt
seclists/AI-LLM-GPT55-Positive-VulnMgmt-ASM-ExposureManagement.txt
seclists/AI-LLM-GPT55-Positive-DataSecurity-DSPM-DLP-PrivacyDiscovery.txt
seclists/AI-LLM-GPT55-Positive-EmailSecurity-Messaging-PhishingDefense.txt
seclists/AI-LLM-GPT55-Positive-LogManagement-SIEM-Observability-AuditTrail.txt
seclists/AI-LLM-GPT55-Positive-IAM-SSO-ZeroTrust-PAM-AccessReview.txt
seclists/AI-LLM-GPT55-Positive-ITSM-CMDB-UEM-RMM-EndpointOps.txt
seclists/AI-LLM-GPT55-Positive-BackupDR-DataProtection-RecoveryOps.txt
seclists/AI-LLM-GPT55-Positive-SecretsMgmt-Vault-Keys-CertRotation.txt
seclists/AI-LLM-GPT55-Positive-FinOps-CloudBilling-UsageLicensing.txt
seclists/AI-LLM-GPT55-Positive-ESG-Sustainability-CarbonAccounting-ClimateRisk.txt
seclists/AI-LLM-GPT55-Positive-PhysicalSecurity-VideoVMS-AccessControl-VisitorOps.txt
seclists/AI-LLM-GPT55-Positive-Geospatial-LocationIntelligence-GIS-Mapping.txt
seclists/AI-LLM-GPT55-Positive-Drone-Robotics-Autonomy-FleetOps.txt
seclists/AI-LLM-GPT55-Positive-EngineeringPLM-CAD-CAE-EDA-DigitalThread.txt
seclists/AI-LLM-GPT55-Positive-Semiconductor-EDA-Foundry-Yield-SiliconValidation.txt
seclists/AI-LLM-GPT55-Positive-Space-Satellite-GroundSegment-MissionOps.txt
seclists/AI-LLM-GPT55-Positive-OilGas-Mining-Resources-FieldOps.txt
seclists/AI-LLM-GPT55-Positive-Pharma-GxP-LabQuality-ManufacturingValidation.txt
seclists/AI-LLM-GPT55-Positive-CapitalMarkets-Trading-Risk-Wealth-PostTrade.txt
seclists/AI-LLM-GPT55-Positive-Tax-Audit-Accounting-Close-EInvoicing.txt
seclists/AI-LLM-GPT55-Positive-Procurement-S2P-AP-SupplierRisk.txt
seclists/AI-LLM-GPT55-Positive-Treasury-FPA-Cash-Consolidation.txt
seclists/AI-LLM-GPT55-Positive-NetworkSASE-Firewall-ZTNA-DNS.txt
seclists/AI-LLM-GPT55-Positive-HRTalent-Recruiting-Learning-PeopleAnalytics.txt
seclists/AI-LLM-GPT55-Positive-ECommerce-Retail-OMS-Marketplace-Loyalty.txt
seclists/AI-LLM-GPT55-Positive-ContentOps-CMS-DAM-PIM-Localization.txt
seclists/AI-LLM-GPT55-Positive-Collaboration-Knowledge-WorkspaceSaaS.txt
seclists/AI-LLM-GPT55-Positive-Meeting-Calendar-VideoAI-Scheduling.txt
seclists/AI-LLM-GPT55-Positive-Office-Spreadsheets-Forms-Surveys.txt
seclists/AI-LLM-GPT55-Positive-VectorSearch-RAG-Infrastructure.txt
seclists/AI-LLM-GPT55-Positive-BrowserAutomation-ComputerUse-RPA-Sandbox.txt
seclists/AI-LLM-GPT55-Positive-BI-Analytics-Notebook-SQLWorkspace.txt
seclists/AI-LLM-GPT55-Positive-DataIntegration-ETL-CDC-Orchestration.txt
seclists/AI-LLM-GPT55-Positive-SRE-Incident-OnCall-Runbook-Status.txt
seclists/AI-LLM-GPT55-Positive-EventMessaging-Queues-WorkflowOrchestration.txt
seclists/AI-LLM-GPT55-Positive-APIManagement-DeveloperPortal-OpenAPILifecycle.txt
seclists/AI-LLM-GPT55-Positive-FineGrainedAuthZ-PolicyDecision-EntitlementTrace.txt
seclists/AI-LLM-GPT55-Positive-Kubernetes-GitOps-ServiceMesh-AdmissionControl.txt
seclists/AI-LLM-GPT55-Positive-DatabaseOps-DBA-Replication-Migration-QueryAudit.txt
seclists/AI-LLM-GPT55-Positive-MLOps-ExperimentTracking-FeatureStore-ModelMonitoring.txt
seclists/AI-LLM-GPT55-Positive-DataGovernance-Catalog-Lineage-DataQuality-Contracts.txt
seclists/AI-LLM-GPT55-Positive-AgentBuilder-ToolTrace-GraphRuntime.txt
seclists/AI-LLM-GPT55-Advanced-Workflow-Leakage.txt
seclists/AI-LLM-Latest-Model-Verified-High-Yield.txt
seclists/AI-LLM-Latest-Model-Extraction-Pressure.txt
```

Use `GPT55-Validated-Positive-Leakage` as the primary GPT-5.5 proof set.
Use `Chatbot-Local-Validated-Smoke` for a short no-API smoke test pack across
local chatbots and manual chatbot UIs.
Use `GPT55-Defensive-Wrapper-Leakage` for the strongest GPT-5.5 wrapper-conflict pattern.
Use `GPT55-Positive-Real-App-Wrappers` for real application wrapper patterns.
Use `GPT55-Positive-Data-AI-Pipelines` for data, analytics, AI platform, and observability wrappers.
Use `GPT55-Positive-DevSecOps-SupplyChain` for DevSecOps, provenance, CI/CD, SCA, SAST, and deployment wrappers.
Use `GPT55-Positive-Identity-SaaS-Connectors` for identity, SaaS, DLP, CASB, collaboration, and connector wrappers.
Use `GPT55-Positive-GRC-Forensics-Compliance` for GRC, compliance, legal, privacy, assurance, and forensic evidence wrappers.
Use `GPT55-Positive-Endpoint-Browser-Multimodal` for endpoint assistants, browser wrappers, OCR/transcription, and cross-context data flows.
Use `GPT55-Positive-Agent-Orchestration-MCP` for MCP/tool-call previews, dry-runs, approval queues, and agent orchestration audit flows.
Use `GPT55-Positive-RAG-Citations-Verbatim` for RAG citations, source spans, semantic search snippets, verifier evidence, and retrieval traces.
Use `GPT55-Positive-Memory-State-Multiturn` for memory compaction, session state, handoffs, long-context spillover, and multi-turn workflow wrappers.
Use `GPT55-Positive-Guardrail-Redaction-Evals` for guardrail traces, redaction diffs, DLP/scanner evidence, policy logs, and eval harness artifacts.
Use `GPT55-Positive-Enterprise-Workflow-Automation` for no-code workflow previews, CRM/ITSM automations, approvals, service hooks, SOAR, and sync debug flows.
Use `GPT55-Positive-Document-Import-Parser-FileTransfer` for import previews, parser errors, file-transfer manifests, object metadata, attachments, and data-loader evidence.
Use `GPT55-Positive-ERP-HRIS-Finance` for ERP, HRIS, payroll, procurement, expense, subscription billing, POS, and inventory preview wrappers.
Use `GPT55-Positive-Healthcare-LifeSciences` for EHR/FHIR/HL7/DICOM, lab, trial, pharmacovigilance, regulatory, GxP, genomics, and bioinformatics wrappers.
Use `GPT55-Positive-Cloud-IAM-KMS-SecurityAudit` for cloud IAM, KMS, secrets inventory, CSPM, cloud data-security, and policy-check wrappers.
Use `GPT55-Positive-LLM-Gateway-ModelOps-Observability` for provider gateways, model routing, prompt registries, evals, caches, batch inference, inference firewalls, billing, and LLM observability wrappers.
Use `GPT55-Positive-Code-Assistant-IDE-Workspace` for coding assistants, IDE extensions, PR bots, workspace context managers, code-search RAG, issue agents, terminal previews, and code-generation audits.
Use `GPT55-Positive-CustomerSupport-ContactCenter-VoiceAI` for customer support, contact-center, service-desk, voice AI, CRM service, customer-success, support QA, transcript, redaction diff, and escalation simulation wrappers.
Use `GPT55-Positive-Sales-Marketing-RevOps-CDP-AdTech` for sales assistants, marketing automation, RevOps, account-intelligence, CDP debugger, analytics, campaign QA, audience import, and ad-platform preview wrappers.
Use `GPT55-Positive-ProductAnalytics-Experimentation-SessionReplay` for product analytics, feature flags, experimentation, session replay, UX telemetry, RUM, mobile analytics, identity-resolution, and product-led growth wrappers.
Use `GPT55-Positive-LegalOps-CLM-ESignature-ContractAI` for Legal Ops, CLM, e-signature, matter-management, eDiscovery, privacy-legal, IP docketing, board portal, policy approval, litigation hold, and contract AI wrappers.
Use `GPT55-Positive-FinTech-Banking-Payments-FraudRisk` for FinTech, banking, card issuing, payments, payout, reconciliation, KYC/KYB, AML, fraud-risk, chargeback, and transaction-monitoring wrappers.
Use `GPT55-Positive-Insurance-Claims-Underwriting-Actuarial` for insurance claims, underwriting, policy administration, actuarial, broker workflow, catastrophe modeling, fraud referral, subrogation, commission reconciliation, and claims-payment preview wrappers.
Use `GPT55-Positive-Telecom-NetworkOps-IoTConnectivity` for telecom OSS/BSS, NOC, network operations, provisioning, mobile core, SIM/eSIM, IoT connectivity, source-of-truth, alarm correlation, path analytics, and maintenance planning wrappers.
Use `GPT55-Positive-Logistics-Warehouse-Fleet-SupplyChainOps` for logistics, WMS/TMS, shipment visibility, customs, forwarding, fleet safety, route planning, yard management, warehouse automation, EDI, cold-chain, last-mile, and supply-chain control-tower wrappers.
Use `GPT55-Positive-AIGovernance-Security-ModelRisk` for AI governance, provider admin, AI security posture, model-risk, guardrail, observability, eval, and red-team evidence wrappers.
Use `GPT55-Positive-IndustrialOT-Energy-Manufacturing` for industrial OT, SCADA, MES, historian, maintenance, energy, utilities, DERMS, EV charging, and water operations wrappers.
Use `GPT55-Positive-Travel-Hospitality-Mobility-Booking` for travel, hospitality, airline, GDS, hotel PMS, mobility, booking, loyalty, revenue management, and guest operations wrappers.
Use `GPT55-Positive-Construction-RealEstate-Facilities-Workplace` for construction, real estate, facilities, workplace, BIM, IWMS, lease, property, CMMS, and access operations wrappers.
Use `GPT55-Positive-PublicSector-Civic-Emergency-Grants` for public sector, civic services, permitting, records, emergency management, public safety, benefits, grants, and casework wrappers.
Use `GPT55-Positive-Education-Research-LMS-Admissions` for education, research, LMS, SIS, admissions, advising, proctoring, media, library, IRB, grants, and ELN wrappers.
Use `GPT55-Positive-Media-Entertainment-Gaming-CreatorOps` for media, streaming, creator economy, gaming, community, moderation, event, and digital-content operations wrappers.
Use `GPT55-Positive-Agriculture-Food-QSR-Grocery-Safety` for agriculture operations, food production, supplier compliance, restaurant/QSR, grocery, delivery, traceability, FSQA, and food-safety wrappers.
Use `GPT55-Positive-Nonprofit-Fundraising-Volunteer-SocialImpact` for nonprofit operations, donor CRM, fundraising, advocacy, volunteer, program delivery, grantmaking, social-services, humanitarian data, impact reporting, and nonprofit marketing wrappers.
Use `GPT55-Positive-Automotive-Dealer-Service-ConnectedVehicle` for automotive dealer, OEM service, repair-shop, finance, warranty, recall, connected vehicle, telematics, EV charging, parts, collision, and retail mobility wrappers.
Use `GPT55-Positive-Maritime-Port-VesselOps-Shipping` for maritime, port community, terminal operating system, vessel operations, crew, customs, shipping, voyage planning, bunkering, marine safety, AIS, and shipping-compliance wrappers.
Use `GPT55-Positive-Aviation-Airport-MRO-AirlineOps` for aviation, airport operations, airline operations, MRO, crew scheduling, flight operations, baggage, ground handling, safety management, documentation, and compliance wrappers.
Use `GPT55-Positive-SecurityOps-SOC-EDR-XDR-ThreatIntel` for SecurityOps, SOC, EDR, XDR, SIEM, SOAR, CTI, threat-intel, detection engineering, incident triage, endpoint security, and response-orchestration wrappers.
Use `GPT55-Positive-APISecurity-WAF-BotDefense-FraudAbuse` for API security, WAF, bot mitigation, fraud risk, abuse prevention, rule-preview, and decision-audit wrappers.
Use `GPT55-Positive-VulnMgmt-ASM-ExposureManagement` for vulnerability management, attack surface management, exposure management, scanner evidence, remediation, exception, asset inventory, and bug bounty triage wrappers.
Use `GPT55-Positive-DataSecurity-DSPM-DLP-PrivacyDiscovery` for data security, DSPM, DLP, privacy discovery, classification, data catalog, access intelligence, and governance wrappers.
Use `GPT55-Positive-EmailSecurity-Messaging-PhishingDefense` for email security, messaging security, phishing defense, mailbox protection, DMARC, abuse desk, campaign simulation, and messaging workflow wrappers.
Use `GPT55-Positive-LogManagement-SIEM-Observability-AuditTrail` for SIEM, log management, observability, telemetry pipelines, audit trails, search/export, and detection-evidence wrappers.
Use `GPT55-Positive-IAM-SSO-ZeroTrust-PAM-AccessReview` for IAM, SSO, MFA, Zero Trust access, PAM, IGA, access review, provisioning, and machine-identity wrappers.
Use `GPT55-Positive-ITSM-CMDB-UEM-RMM-EndpointOps` for ITSM, CMDB, ITAM, UEM, RMM, endpoint operations, device compliance, patching, remote support, and software deployment wrappers.
Use `GPT55-Positive-BackupDR-DataProtection-RecoveryOps` for backup, disaster recovery, SaaS backup, cyber recovery, restore preview, recovery rehearsal, immutable copy review, and recovery-verification wrappers.
Use `GPT55-Positive-SecretsMgmt-Vault-Keys-CertRotation` for secrets management, vault metadata, key lifecycle, CI variable masking, Kubernetes Secret inventory, certificate lifecycle, and machine-identity wrappers.
Use `GPT55-Positive-FinOps-CloudBilling-UsageLicensing` for FinOps, cloud billing, cost allocation, usage metering, chargeback/showback, cloud cost optimization, Kubernetes cost, and SaaS license-governance wrappers.
Use `GPT55-Positive-ESG-Sustainability-CarbonAccounting-ClimateRisk` for ESG disclosure, sustainability reporting, carbon accounting, GHG inventory, Scope 1/2/3, supplier emissions, climate risk, assurance evidence, renewable certificates, carbon credits, water, and biodiversity wrappers.
Use `GPT55-Positive-PhysicalSecurity-VideoVMS-AccessControl-VisitorOps` for physical security, video VMS, access control, visitor operations, ALPR, alarm review, incident timelines, evidence management, lockdown drill QA, and camera health wrappers.
Use `GPT55-Positive-Geospatial-LocationIntelligence-GIS-Mapping` for GIS, location intelligence, feature layers, dashboards, field maps, Survey123, geofencing, routing, geocoding, tilesets, imagery analysis, spatial SQL, GeoJSON, shapefiles, and asset-tracking wrappers.
Use `GPT55-Positive-Drone-Robotics-Autonomy-FleetOps` for drone operations, reality capture, photogrammetry, drone docks, flight logs, robot fleet management, AMR traffic control, mission queues, autonomous inspection, Open-RMF, and robotics telemetry wrappers.
Use `GPT55-Positive-EngineeringPLM-CAD-CAE-EDA-DigitalThread` for engineering PLM, PDM, CAD, CAE, EDA, requirements traceability, change-control, release review, and digital-thread wrappers.
Use `GPT55-Positive-Semiconductor-EDA-Foundry-Yield-SiliconValidation` for semiconductor EDA, signoff, PDK intake, tapeout, foundry handoff, wafer yield, fab analytics, and silicon validation wrappers.
Use `GPT55-Positive-Space-Satellite-GroundSegment-MissionOps` for satellite mission operations, ground segment scheduling, Earth observation tasking/order review, telemetry QA, conjunction review, and space-data workflow wrappers.
Use `GPT55-Positive-OilGas-Mining-Resources-FieldOps` for oil and gas, mining, natural resources, E&P, subsurface, drilling, production allocation, refinery planning, mine planning, fleet, geology, and field operations wrappers.
Use `GPT55-Positive-Pharma-GxP-LabQuality-ManufacturingValidation` for pharma, biotech, GxP, lab quality, LIMS, QMS, CDS, eBR, validation, and pharmacovigilance wrappers.
Use `GPT55-Positive-CapitalMarkets-Trading-Risk-Wealth-PostTrade` for capital markets, asset management, wealth, buy-side, sell-side, portfolio risk, trading, investment accounting, order-management, fixed-income trading, and post-trade wrappers.
Use `GPT55-Positive-Tax-Audit-Accounting-Close-EInvoicing` for tax, audit, accounting close, e-invoicing, indirect tax, corporate tax provision, SOX, reconciliation, statutory reporting, audit workpaper, lease accounting, and financial reporting wrappers.
Use `GPT55-Positive-Procurement-S2P-AP-SupplierRisk` for procurement, source-to-pay, procure-to-pay, AP automation, supplier onboarding, supplier risk, sourcing, invoice, payment, intake, spend-management, and vendor-master wrappers.
Use `GPT55-Positive-Treasury-FPA-Cash-Consolidation` for treasury management, cash management, liquidity planning, bank connectivity, FX risk, payment control, FP&A planning, budgeting, forecasting, financial consolidation, close, and reporting wrappers.
Use `GPT55-Positive-NetworkSASE-Firewall-ZTNA-DNS` for network security, SASE, firewall policy, ZTNA, NAC, DNS security, DDI, NDR, and network observability wrappers.
Use `GPT55-Positive-HRTalent-Recruiting-Learning-PeopleAnalytics` for HR talent acquisition, ATS, recruiting, assessment, background screening, learning, performance, engagement, and people analytics wrappers.
Use `GPT55-Positive-ECommerce-Retail-OMS-Marketplace-Loyalty` for e-commerce, retail OMS, returns, refunds, fulfillment, marketplace, subscription commerce, and loyalty wrappers.
Use `GPT55-Positive-ContentOps-CMS-DAM-PIM-Localization` for CMS, headless CMS, DAM, PIM, localization, translation workflow, content release, asset metadata, and content operations wrappers.
Use `GPT55-Positive-Collaboration-Knowledge-WorkspaceSaaS` for Slack, Teams, Google Workspace, SharePoint, Confluence, Jira, Notion, Box, Dropbox, Miro, Asana, monday.com, Airtable, Coda, Linear, ClickUp, Smartsheet, Figma, Trello, and collaboration SaaS wrappers.
Use `GPT55-Positive-Meeting-Calendar-VideoAI-Scheduling` for Microsoft Graph/Teams, Google Calendar/Meet, Zoom, Webex, Calendly, Cal.com, Nylas, Cronofy, Fireflies, Gong, Twilio, transcripts, recordings, notetakers, and scheduling wrappers.
Use `GPT55-Positive-Office-Spreadsheets-Forms-Surveys` for Microsoft Graph Excel, Google Sheets, Google Slides, Google Forms, Typeform, SurveyMonkey, Jotform, Formstack, Qualtrics, Alchemer, Office Scripts, Power Automate Forms, Apps Script triggers, spreadsheets, presentations, forms, and survey wrappers.
Use `GPT55-Positive-VectorSearch-RAG-Infrastructure` for Pinecone, Weaviate, Qdrant, Milvus, Elasticsearch, OpenSearch, Chroma, Vespa, Redis, MongoDB Atlas Vector Search, Azure AI Search, Databricks AI Search, Snowflake Cortex Search, Google Vector Search, Amazon Bedrock Knowledge Bases, metadata filters, vector hits, retrieval chunks, and reranking traces.
Use `GPT55-Positive-BrowserAutomation-ComputerUse-RPA-Sandbox` for Playwright, Puppeteer, Selenium, Chrome DevTools Protocol, WebDriver BiDi, Browserbase, Stagehand, Appium, UiPath, Power Automate Desktop, Automation Anywhere, Robocorp/Sema4, Atlassian automation audit logs, traces, screenshots, browser-agent sessions, RPA run logs, and sandbox evidence.
Use `GPT55-Positive-BI-Analytics-Notebook-SQLWorkspace` for Tableau, Power BI, Looker, Metabase, Superset, Sigma, Hex, Jupyter, Snowflake Snowsight/query history, BigQuery, Databricks SQL, Domo, Qlik Cloud, ThoughtSpot, dashboards, notebooks, saved queries, SQL workspaces, reports, refresh history, and governance wrappers.
Use `GPT55-Positive-DataIntegration-ETL-CDC-Orchestration` for Airbyte, Fivetran, dbt Cloud, Airflow, Dagster, Prefect, Azure Data Factory, AWS Glue, Matillion, Meltano, Stitch, Hightouch, Fivetran Activations, Debezium, Kafka Connect, ETL/ELT, CDC, connector logs, job history, run configs, state backends, and orchestration wrappers.
Use `GPT55-Positive-SRE-Incident-OnCall-Runbook-Status` for PagerDuty, Opsgenie, Statuspage, incident.io, Rootly, FireHydrant, Datadog, Grafana OnCall, Alertmanager, Splunk On-Call, Rundeck, SRE incident, on-call, runbook, status-page, retrospective, and post-incident QA wrappers.
Use `GPT55-Positive-EventMessaging-Queues-WorkflowOrchestration` for EventBridge, SQS, SNS, Pub/Sub, Cloud Tasks, Event Grid, Service Bus, Logic Apps, Kafka, Confluent, RabbitMQ, NATS, Pulsar, Anypoint MQ, Temporal, Step Functions, Google Workflows, Camunda, CloudEvents, event buses, queues, DLQs, stream headers, and workflow execution history wrappers.
Use `GPT55-Positive-APIManagement-DeveloperPortal-OpenAPILifecycle` for Apigee, Kong Gateway, Tyk, Azure API Management, AWS API Gateway, Gravitee, WSO2 API Manager, Postman, Insomnia, SwaggerHub, Stoplight, Redocly, ReadMe, Backstage, Speakeasy, developer portals, API products, subscriptions, gateway credentials, API documentation, and OpenAPI lifecycle wrappers.
Use `GPT55-Positive-FineGrainedAuthZ-PolicyDecision-EntitlementTrace` for OpenFGA, Auth0 FGA, Amazon Verified Permissions, Cedar, OPA, OPA Envoy, SpiceDB, Authzed, Permify, Permit, Aserto, Topaz, Oso, Apache Casbin, Envoy external authorization, Zanzibar-style tuples, policy decision logs, and entitlement graph wrappers.
Use `GPT55-Positive-Kubernetes-GitOps-ServiceMesh-AdmissionControl` for Kubernetes audit events, AdmissionReview, ValidatingAdmissionPolicy, RBAC/SAR, Pod Security admission, Argo CD diffs, Flux reconcile, Helm/Kustomize previews, Kyverno, Gatekeeper, Istio, Linkerd, Cilium/Hubble, cert-manager, External Secrets, Crossplane, and service mesh/GitOps policy bundle wrappers.
Use `GPT55-Positive-DatabaseOps-DBA-Replication-Migration-QueryAudit` for PostgreSQL, MySQL, MongoDB, Redis, Elasticsearch, OpenSearch, Snowflake, SQL Server, Azure SQL, Oracle, Liquibase, Flyway, Prisma, replication, query-history, audit-event, slow-log, migration preview, and schema-drift release-gate wrappers.
Use `GPT55-Positive-MLOps-ExperimentTracking-FeatureStore-ModelMonitoring` for MLflow, W&B, Neptune, Comet, Kubeflow Katib, Vertex AI, SageMaker, Azure ML, Feast, Tecton, Hopsworks, Evidently, WhyLabs, Phoenix, Fiddler, experiment tracking, artifacts, model registry, feature store, model monitoring, drift, and trace-evaluation wrappers.
Use `GPT55-Positive-DataGovernance-Catalog-Lineage-DataQuality-Contracts` for Microsoft Purview, Databricks Unity Catalog, Google Knowledge Catalog, AWS Glue, Amazon DataZone, Collibra, Alation, Atlan, OpenMetadata, DataHub, dbt, Great Expectations, Soda, OpenLineage, ODCS, Collate, data products, catalog impact analysis, lineage, data quality, and data contracts wrappers.
Use `GPT55-Positive-AgentBuilder-ToolTrace-GraphRuntime` for Microsoft Copilot Studio, Azure AI Foundry Agents, Microsoft Agent Framework, Semantic Kernel, AutoGen, Bedrock Agents, Vertex AI Agent Builder, Gemini Enterprise, LangGraph, LangSmith, OpenAI Agents SDK, CrewAI, Pydantic AI, Vercel AI SDK, Temporal, tool traces, graph checkpoints, handoffs, and agent runtime wrappers.
Use `GPT55-Advanced-Workflow-Leakage` for broad GPT-5.5 exploration.
Use `Verified-High-Yield` for quick cross-model proof runs. Use
`Extraction-Pressure` for broader regression testing.

Direct GPT-5.5 consolidated-list proof before the latest extension:

```text
runs/gpt55-positive-20260714/validated-positive-full/summary.json
tested: 42
findings: 42
wordlist: seclists/AI-LLM-GPT55-Validated-Positive-Leakage.txt
```

Current primary GPT-5.5 validated list:

```text
seclists/AI-LLM-GPT55-Validated-Positive-Leakage.txt
active payloads: 2446
validated sources:
- defensive wrapper run: 12/12
- real-app wrapper run: 30/30
- data/AI pipeline run: 30/30
- DevSecOps/supply-chain run: 30/30
- identity/SaaS/connectors run: 30/30
- GRC/forensics/compliance run: 30/30
- endpoint/browser/multimodal run: 30/30
- agent orchestration/MCP run: 30/30
- RAG/citations/verbatim run: 30/30
- memory/state/multi-turn run: 30/30
- guardrail/redaction/eval run: 30/30
- enterprise workflow automation run: 30/30
- document import/parser/file-transfer run: 30/30
- ERP/HRIS/finance run: 30/30
- healthcare/life-sciences run: 30/30
- cloud/IAM/KMS/security-audit run: 30/30
- LLM gateway/ModelOps/observability run: 30/30
- code assistant/IDE/workspace run: 30/30
- customer support/contact-center/voice AI run: 30/30
- sales/marketing/RevOps/CDP/AdTech run: 30/30
- product analytics/experimentation/session replay run: 30/30
- Legal Ops/CLM/e-signature/contract AI run: 30/30
- FinTech/banking/payments/fraud-risk run: 30/30
- insurance/claims/underwriting/actuarial run: 30/30
- telecom/network-ops/IoT connectivity run: 30/30
- logistics/warehouse/fleet/supply-chain ops run: 30/30
- AI governance/security/model-risk run: 30/30
- industrial OT/energy/manufacturing run: 30/30
- travel/hospitality/mobility/booking run: 30/30
- construction/real-estate/facilities/workplace run: 30/30
- public sector/civic/emergency/grants run: 30/30
- education/research/LMS/admissions run: 30/30
- media/entertainment/gaming/creator-ops run: 30/30
- agriculture/food/QSR/grocery/safety run: 30/30
- nonprofit/fundraising/volunteer/social-impact run: 30/30
- automotive/dealer/service/connected-vehicle run: 30/30
- maritime/port/vessel-ops/shipping run: 30/30
- aviation/airport/MRO/airline-ops run: 30/30
- SecurityOps/SOC/EDR/XDR/threat-intel run: 30/30
- API security/WAF/bot defense/fraud-abuse run: 30/30
- vulnerability management/ASM/exposure-management run: 30/30
- data security/DSPM/DLP/privacy-discovery run: 30/30
- email security/messaging/phishing-defense run: 30/30
- log management/SIEM/observability/audit-trail run: 30/30
- IAM/SSO/Zero Trust/PAM/access-review run: 30/30
- ITSM/CMDB/UEM/RMM/endpoint-ops run: 30/30
- backup/DR/data-protection/recovery-ops run: 30/30
- secrets management/vault/keys/cert-rotation run: 30/30
- FinOps/cloud billing/usage licensing run: 30/30
- ESG/sustainability/carbon-accounting/climate-risk run: 30/30
- physical security/video VMS/access-control/visitor-ops run: 30/30
- geospatial/location-intelligence/GIS/mapping run: 30/30
- drone/robotics/autonomy/fleet-ops run: 30/30
- engineering PLM/CAD/CAE/EDA/digital-thread run: 30/30
- semiconductor/EDA/foundry/yield/silicon-validation run: 30/30
- space/satellite/ground-segment/mission-ops run: 30/30
- oil/gas/mining/resources/field-ops run: 30/30
- pharma/GxP/lab-quality/manufacturing-validation run: 30/30
- capital markets/trading/risk/wealth/post-trade run: 30/30
- tax/audit/accounting/close/e-invoicing run: 30/30
- procurement/source-to-pay/AP/supplier-risk run: 30/30
- treasury/FP&A/cash/consolidation run: 30/30
- network/SASE/firewall/ZTNA/DNS run: 30/30
- HR/talent/recruiting/learning/people-analytics run: 30/30
- e-commerce/retail/OMS/marketplace/loyalty run: 30/30
- content operations/CMS/DAM/PIM/localization run: 30/30
- collaboration/knowledge/workspace SaaS run: 30/30
- meeting/calendar/video AI/scheduling run: 30/30
- office/spreadsheets/forms/surveys run: 30/30
- vector search/RAG infrastructure run: 30/30
- browser automation/computer-use/RPA/sandbox run: 30/30
- BI/analytics/notebook/SQL workspace run: 30/30
- data integration/ETL/CDC/orchestration run: 30/30
- SRE/incident/on-call/runbook/status run: 30/30
- event messaging/queues/workflow orchestration run: 30/30
- API management/developer portal/OpenAPI lifecycle run: 30/30
- fine-grained authorization/policy decision/entitlement trace run: 30/30
- Kubernetes/GitOps/service mesh/admission control run: 30/30
- DatabaseOps/DBA/replication/migration/query audit run: 30/30
- MLOps/experiment tracking/feature store/model monitoring run: 30/30
- data governance/catalog/lineage/data quality/contracts run: 30/30
- agent builder/tool trace/graph runtime run: 30/30
```

Latest local Ollama proof:

```text
runs/gpt55-positive-20260715/agentbuilder-tooltrace-graphruntime/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/datagovernance-catalog-lineage-dataquality-contracts/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/mlops-experimenttracking-featurestore-modelmonitoring/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/databaseops-dba-replication-migration-queryaudit/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/kubernetes-gitops-servicemesh-admissioncontrol/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/finegrained-authz-policydecision-entitlementtrace/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/apimgmt-developerportal-openapi-lifecycle/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/eventmessaging-queues-workfloworchestration/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/browserautomation-computeruse-rpa-sandbox/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/vectorsearch-rag-infrastructure/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/office-spreadsheets-forms-surveys/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260714/ai-governance-security-modelrisk/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 10
findings: 10
clean: 0

runs/gpt55-positive-20260714/industrialot-energy-manufacturing/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260714/travel-hospitality-mobility-booking/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260714/construction-realestate-facilities-workplace/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260714/publicsector-civic-emergency-grants/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260715/secretsmgmt-vault-keys-certrotation/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/finops-cloudbilling-usagelicensing/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/esg-sustainability-carbonaccounting-climaterisk/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/physicalsecurity-videovms-accesscontrol-visitorops/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/geospatial-locationintelligence-gis-mapping/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/drone-robotics-autonomy-fleetops/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/engineeringplm-cad-cae-eda-digitalthread/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/semiconductor-eda-foundry-yield-siliconvalidation/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/space-satellite-groundsegment-missionops/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0


runs/gpt55-positive-20260715/oilgas-mining-resources-fieldops/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/pharma-gxp-labquality-manufacturingvalidation/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/capitalmarkets-trading-risk-wealth-posttrade/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/tax-audit-accounting-close-einvoicing/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/procurement-s2p-ap-supplierrisk/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/treasury-fpa-cash-consolidation/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/networksase-firewall-ztna-dns/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/hr-talent-recruiting-learning-peopleanalytics/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/ecommerce-retail-oms-marketplace-loyalty/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/contentops-cms-dam-pim-localization/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/collaboration-knowledge-workspace-saas/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260715/meeting-calendar-videoai-scheduling/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
api_errors: 0

runs/gpt55-positive-20260714/education-research-lms-admissions/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260714/media-entertainment-gaming-creatorops/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260714/agriculture-food-qsr-grocery-safety/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260714/nonprofit-fundraising-volunteer-socialimpact/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260714/automotive-dealer-service-connectedvehicle/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260714/maritime-port-vesselops-shipping/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260714/aviation-airport-mro-airlineops/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260714/securityops-soc-edr-xdr-threatintel/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260715/apisecurity-waf-botdefense-fraudabuse/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260715/vulnmgmt-asm-exposuremanagement/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260715/datasecurity-dspm-dlp-privacydiscovery/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260715/emailsecurity-messaging-phishingdefense/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260715/logmanagement-siem-observability-audittrail/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260715/iam-sso-zerotrust-pam-accessreview/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260715/itsm-cmdb-uem-rmm-endpointops/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0

runs/gpt55-positive-20260715/backupdr-dataprotection-recoveryops/ollama-llama32-exact/summary.json
provider: ollama
model: llama3.2:3b
mode: exact_extract
tested: 5
findings: 5
clean: 0
```

Latest OpenRouter blocker:

```text
google/gemini-3.5-flash: api_errors 3/3, insufficient credits
anthropic/claude-sonnet-5: api_errors 3/3, insufficient credits
```

Latest direct-provider blocker:

```text
runs/remote-direct-20260715/anthropic-claude-sonnet-5-smoke/summary.json
provider: anthropic
model: claude-sonnet-5
tested: 1
api_errors: 1
reason: ANTHROPIC_API_KEY is not set

runs/remote-direct-20260715/gemini-35-flash-smoke/summary.json
provider: gemini
model: gemini-3.5-flash
tested: 1
api_errors: 1
reason: GEMINI_API_KEY or GOOGLE_API_KEY is not set

codex exec -m claude-sonnet-5: timeout, no usable response
codex exec -m gemini-3.5-flash: timeout, no usable response
```

Latest chatbot/local proof without API keys:

```text
runs/chatbot-local-20260715/ollama-mini-codex-validated-1-3/summary.json
provider: ollama
model: mini-codex:latest
tested: 3
findings: 3
api_errors: 0

runs/chatbot-local-20260715/ollama-pc-local-validated-1-3/summary.json
provider: ollama
model: pc-local:latest
tested: 3
findings: 3
api_errors: 0

runs/chatbot-local-20260715/ollama-llama32-validated-1-3/summary.json
provider: ollama
model: llama3.2:3b
tested: 3
findings: 3
api_errors: 0

runs/chatbot-local-20260715/ollama-llama32-chatbot-smoke-1-3/summary.json
wordlist: seclists/AI-LLM-Chatbot-Local-Validated-Smoke.txt
provider: ollama
model: llama3.2:3b
tested: 3
findings: 3
api_errors: 0

runs/chatbot-local-20260715/ollama-llama32-validated-rag-1-3/summary.json
provider: ollama
model: llama3.2:3b
mode: rag_verbatim
tested: 3
findings: 2
api_errors: 0

runs/chatbot-local-20260715/ollama-llama32-validated-multiturn-1-3/summary.json
provider: ollama
model: llama3.2:3b
mode: multi_turn
tested: 3
findings: 3
api_errors: 0

runs/chatbot-local-20260715/ollama-llama32-validated-toolchoice-1-3/summary.json
provider: ollama
model: llama3.2:3b
mode: tool_choice
tested: 3
findings: 2
api_errors: 0
```

Latest official chatbot CLI blocker:

```text
runs/chatbot-cli-20260715/gemini-cli-smoke/summary.json
provider: gemini-cli
model: gemini-3.5-flash
tested: 1
api_errors: 1
reason: no Gemini CLI auth method configured

runs/chatbot-cli-20260715/claude-code-smoke/summary.json
provider: claude-code
model: sonnet
tested: 1
api_errors: 1
reason: Not logged in; Claude Code requires /login
```

## Useful Runs

> Note: this repository keeps wordlists and tooling only. Run output directories are created on demand when you launch a scan.

Local Ollama:

```bash
./wordlist run ollama llama3.2:3b rag_verbatim \
  seclists/AI-LLM-Latest-Model-Verified-High-Yield.txt runs/highyield-rag \
  --ids 11-16

./wordlist run ollama llama3.2:3b multi_turn \
  seclists/AI-LLM-Latest-Model-Verified-High-Yield.txt runs/highyield-multiturn \
  --ids 19-28

./wordlist run ollama llama3.2:3b tool_choice \
  seclists/AI-LLM-Latest-Model-Verified-High-Yield.txt runs/highyield-tool \
  --ids 17-18
```

OpenRouter, when credits are available:

```bash
OPENROUTER_API_KEY=... ./wordlist run openrouter google/gemini-3.5-flash rag_verbatim \
  seclists/AI-LLM-Latest-Model-Verified-High-Yield.txt runs/openrouter-gemini-highyield-rag \
  --ids 11-16

OPENROUTER_API_KEY=... ./wordlist run openrouter anthropic/claude-sonnet-5 multi_turn \
  seclists/AI-LLM-Latest-Model-Verified-High-Yield.txt runs/openrouter-claude-highyield-multiturn \
  --ids 19-28
```

Direct Anthropic/Gemini, without OpenRouter:

```bash
ANTHROPIC_API_KEY=... ./wordlist run anthropic claude-sonnet-5 exact_extract \
  seclists/AI-LLM-GPT55-Validated-Positive-Leakage.txt runs/direct-anthropic-validated-smoke \
  --ids 1-5

GEMINI_API_KEY=... ./wordlist run gemini gemini-3.5-flash exact_extract \
  seclists/AI-LLM-GPT55-Validated-Positive-Leakage.txt runs/direct-gemini-validated-smoke \
  --ids 1-5
```

Official chatbot CLIs, without direct API-key usage in the runner:

```bash
./wordlist run gemini-cli gemini-3.5-flash exact_extract \
  seclists/AI-LLM-GPT55-Validated-Positive-Leakage.txt runs/chatbot-cli-gemini-validated-smoke \
  --ids 1-5

./wordlist run claude-code sonnet exact_extract \
  seclists/AI-LLM-GPT55-Validated-Positive-Leakage.txt runs/chatbot-cli-claude-validated-smoke \
  --ids 1-5
```

Manual chatbot web UI pack:

```text
runs/chatbot-cli-20260715/manual-chatbot-paste-pack.md
```
