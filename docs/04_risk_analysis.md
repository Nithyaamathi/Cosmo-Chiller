# 🔴 Failure Scenarios & Mitigations

This section outlines potential failure scenarios in the tiered storage system and how each is addressed through architectural design, Azure-native tooling, and defensive coding practices.

---

## 🛡️ Failure Matrix

| ⚠️ **Scenario**                          | 🛠️ **Mitigation Strategy**                                                                                                                                       |
|------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ❌ **Archival Function Failure**         | - ✅ Enable retry policies on the Azure Function App.<br>- 🧾 Function is **idempotent** (ensures no duplication on retry).<br>- 📊 Alerting via **Application Insights** for proactive monitoring. |
| ⚠️ **Partial Archival (only blob or DB updated)** | - ⚙️ Treated as a **transactional unit** — blob upload is completed **before** updating Cosmos DB.<br>- ⛔ Cosmos DB patch will **not proceed** if blob write fails.<br>- 💡 Use `Try-Catch-Finally` with explicit failure logging. |
| 🔁 **Race Condition (read during archival)** | - 🕒 Cosmos retains full document until **after** stub replacement completes.<br>- 🔐 Use **ETags** to enforce concurrency control and prevent reads mid-transition. |
| 🧊 **Cold Storage Down (Blob Unavailable)** | - 🚫 API layer detects Blob read failure and returns **HTTP 503 – Service Unavailable** with user-friendly `"Please try later"` message.<br>- ⚡ Optionally implement **in-memory or Redis cache** for hot-access archived documents to minimize impact. |

---

## 🧠 Design Principles

- **Idempotency** ensures operations can safely be retried without side effects.
- **Fail-fast design** prevents silent corruption or data loss.
- **Observability-first** — failures are logged and surfaced before they impact SLAs.
- **Fallback mechanisms** ensure user experience degrades gracefully during outages.

---

## 📈 Alert Recommendations

- 🔔 Set up alert rules for:
  - Function execution failures
  - Blob write failures
  - Cold read latencies
  - BlobNotFound errors

---

## ✅ Summary

> 🔐 _"Robust systems are not those that never fail — they're the ones that recover fast and safely."_  

This failure handling strategy builds confidence for production-grade tiered storage with resilience and observability at its core.


