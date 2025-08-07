# 🚀 Deployment & Rollback Strategy

This document outlines the phased approach for deploying the tiered storage architecture, along with a safe and simple rollback plan in case of failure.

---

## 📦 Deployment Phases

| 🔢 Phase | ✅ Step Description                                                                 |
|---------|--------------------------------------------------------------------------------------|
| 1️⃣      | **Deploy Cold-Read Logic**<br>Update the API layer to include fallback to Blob Storage for archived records. |
| 2️⃣      | **Deploy Archival Function**<br>Enable the `TimerTrigger` in Azure Function. Begin with a dry run to validate logic without data change. |
| 3️⃣      | **Bulk Backfill**<br>Use Azure Data Factory or custom scripts to archive existing records older than 90 days. |
| 4️⃣      | **Monitor**<br>Track logs and metrics via Application Insights and dashboards to ensure system stability and correctness. |

---

## 🔄 Rollback Plan

If issues are detected during or after deployment, the following rollback steps can be taken safely:

- 🚫 **Disable Archival Function** to stop new data from being archived.
- ♻️ **Re-import archived data** from Blob Storage back into Cosmos DB using the stored JSON payloads.

---

> 🧪 _All components are designed to be idempotent and reversible for safe deployment._
