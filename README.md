# Cosmo-Chiller
A seamless serverless solution for archiving and retrieving cold data from Azure Cosmos DB — without changing your API or impacting performance. Chill your costs, not your availability.

## 📚 Documentation

1. 🔍 [Context](docs/01_problem_context.md)  
   _Problem statement, business drivers, and goals._

2. 🏗️ [Architecture](architecture/cosmo-chiller-architecture.png)  
   _High-level and low-level architecture diagrams and explanations._

3. 🧠 [Strategy](docs/02_strategy_justification.md)  
   _Cost optimization, storage strategy, and design principles._

4. 💻 [Sample Code](azure-functions)  
   _key modules and logic that enable the tiered storage system._

5. 🔄 [Data Lifecycle](docs/03_data_lifecycle.md)  
   _Write, archive, and read paths with storage management._

6. ⚠️ [Risk Analysis](docs/04_risk_analysis.md)  
   _Failure scenarios and mitigation strategies._

7. 📈 [Monitoring & Alerting](monitor-alerts/alerts_and_metrics.md)  
   _Observability, metrics, and alert design._

8. 🚀 [Deployment & Rollback Strategy](docs/05_deployment.md)  
   _Production rollout steps, canary strategy, and rollback plan._

9. 🛠️ [Bulk Migration](scripts/bulk_migration_data_factory.md)  
   _one-time archival for existing records using Azure Data Factory or custom scripts._

