The billing records system built on Azure Cosmos DB has reached over 2 million documents, with each document as large as 300 KB. Analysis shows that records older than 90 days are rarely accessed. This usage pattern results in excessive storage costs and RU consumption, particularly for rarely accessed data.

To resolve this, we propose a tiered storage strategy, where hot data (< 90 days) remains in Cosmos DB for high-speed access, and cold data (> 90 days) is archived to Azure Blob Storage (Cool Tier) via an Azure Function. This solution requires no API contract changes, achieves significant cost reduction, and meets all latency, simplicity, and continuity constraints.

Expected Outcomes:
    * Up to 80% reduction in Cosmos DB storage costs
    * Significantly lower RU consumption on read-heavy workloads
    * <5s cold read latency (acceptable threshold)
    * Fully transparent to users and clients (no API changes)
    * Seamless, zero-downtime deployment
