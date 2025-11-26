# Cost Analysis (₹)

This document provides cost estimates for the **Serverless Data Lakehouse** architecture in **Indian Rupees (₹)**.

## Production Environment

At production scale (petabyte-scale data lake), the architecture typically costs:

| Service | Monthly Cost (₹) | Notes |
|---------|------------------|-------|
| **S3 Storage** | ₹20,000–40,000 | Data lake storage (Delta format) |
| **AWS Glue ETL** | ₹30,000–60,000 | DPU hours for transformations |
| **Athena Queries** | ₹15,000–30,000 | Per TB scanned |
| **EMR Serverless** | ₹25,000–50,000 | Spark job execution |
| **Glue Data Catalog** | ₹5,000–10,000 | Metadata storage |
| **Lake Formation** | ₹3,000–5,000 | Governance and access control |
| **CloudWatch** | ₹3,000–5,000 | Monitoring and logs |
| **Total** | **₹100,000–200,000** | ~$1,250–2,500/month |

## Development Environment

For dev/staging environments:

| Environment | Approx Monthly Cost (₹) | Notes |
|------------|--------------------------|-------|
| Dev | ₹15,000–25,000 | Sample data, minimal jobs |
| Staging | ₹40,000–70,000 | Production-like, reduced scale |
| Production | ₹100,000–200,000 | Full scale, all workloads |

## Cost Optimization Strategies

- **Columnar formats** – Use Parquet/Delta for 10x query cost reduction
- **Partitioning** – Partition by date/region to reduce scan costs
- **Compaction** – Regular compaction reduces small file overhead
- **Athena workgroups** – Set query cost limits per team
- **S3 lifecycle** – Move cold data to Glacier
- **Glue job bookmarks** – Process only new data incrementally

## Related Documentation

See `ARCHITECTURE.md` for service details and `DEPLOYMENT.md` for configuration options.
