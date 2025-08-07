### The Challenge: "Cost Optimization for Azure Cosmos DB"

You are a Principal Cloud Solutions Architect with deep expertise in designing and optimizing highly scalable, cost-effective serverless solutions on Microsoft Azure. You specialize in data-intensive applications and have a proven track record of solving complex data management and cost challenges for enterprise systems.
Your task is to analyze the following business problem and produce a comprehensive, production-ready solution proposal. You must go beyond a theoretical overview and provide a detailed, actionable plan.

##1. Problem Context & Mandate

#Scenario: We operate a serverless architecture on Azure. A core service writes and reads billing records stored in an Azure Cosmos DB (NoSQL API). The system is heavily read-biased.

#Core Challenge: The Cosmos DB collection has grown to over 2 million records, with individual records reaching up to 300 KB. This has led to a significant and escalating cost profile. Analysis shows that records older than 90 days are very rarely accessed. Our primary objective is to drastically reduce storage and operational costs.

#Mandatory Constraints:
Performance: Latency for retrieving old records (older than 90 days) must be in the order of seconds (e.g., < 5 seconds). Latency for recent records must remain low.
Simplicity: The solution must be straightforward to implement and maintain with a small engineering team.
Business Continuity: The solution must guarantee zero data loss and be implemented with zero service downtime.
API Stability: The public-facing read/write API contracts for accessing billing records must not change. The backend refactoring should be entirely transparent to the API consumers.

##2. Core Task: Strategy Recommendation

Analyze potential architectural patterns for this problem. Common patterns include Data Tiering to Blob Storage, using Cosmos DB's native Time-To-Live (TTL) feature for archival, or leveraging a different database for cold storage.
Your primary task is to recommend the single best strategy and provide a robust justification for your choice. Your justification must evaluate the chosen strategy against alternatives based on the following criteria:
Maximum Cost Reduction (both storage and Request Units/throughput).
Implementation Simplicity & Maintainability.
Performance & Reliability of the end-to-end data lifecycle (write, archive, hot read, cold read).
Seamless Integration with the existing serverless architecture.

##3. Required Deliverables

You must structure your response into the following five distinct sections.

#Section 1: Written Proposal Document A formal document that includes:
Executive Summary: A brief overview of the problem, the proposed solution, and expected outcomes (e.g., projected cost savings).
Chosen Strategy & Justification: A detailed explanation of your recommended architecture (e.g., "Tiered Storage with Azure Functions and Blob Storage") and a compelling argument for why it is superior to the alternatives.
Data Lifecycle Management: A clear description of the data flow:
How new records are written.
The process and trigger for archiving data from Cosmos DB.
How the system differentiates between a "hot" read (Cosmos DB) and a "cold" read (archive).
The end-to-end process for retrieving an archived record.

#Section 2: Architecture Diagram Provide the MermaidJS code within a code block for a detailed architecture diagram. The diagram must illustrate the current components and the new components you are proposing, showing all data flows for both read and write paths (hot and cold).

#Section 3: Python Implementation Artifacts Provide Python code snippets for the key logical components of the solution. Assume the use of Azure Functions.
archive_billing_records_function: A time-triggered Azure Function (function_app.py and function.json binding examples) that identifies and moves records older than 90 days from Cosmos DB to the archive tier. Include logic for verification and safe deletion.
read_billing_record_logic: A code snippet representing the core logic inside the existing read API's backing function. This code must implement the "fallback" pattern:
Try to fetch the record from the "hot" tier (Cosmos DB).
If it returns a "not found" error, fetch the record from the "cold" archive tier.
Return the record to the user, maintaining the original API contract.

#Section 4: Production Readiness & Risk Analysis This section is critical. Demonstrate forward-thinking by addressing potential real-world issues.
Failure Scenarios & Mitigation: What could go wrong?
Archival Failure: What happens if the archival function fails midway? How do you prevent data loss or partial archival? (e.g., dead-letter queues, idempotent operations).
Race Conditions: Could a record be requested for read while it's being archived? How do you handle this?
Cold Storage Failure: What if the cold storage is temporarily unavailable? How should the API respond?
Monitoring & Alerting: What specific metrics should be monitored to ensure the health of this new system? (e.g., archival success/failure rate, cold read latency, function execution count). Suggest specific Azure Monitor alert rules.
Deployment & Rollback Strategy: Propose a phased, low-risk deployment plan. How would you roll back the changes safely if a critical issue is discovered post-deployment?  


Proceed with generating the complete, detailed response.
