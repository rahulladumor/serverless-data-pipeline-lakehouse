# Runbook

Operational guide for deploying, operating, and maintaining the **Serverless Data Lakehouse**.

## 1. Deployment

### Prerequisites

- AWS CLI configured with appropriate credentials
- Node.js 18+ and npm installed
- AWS CDK CLI installed (`npm install -g aws-cdk`)

### Deploy Steps

```bash
# Install dependencies
npm install

# Bootstrap CDK (first time only)
cdk bootstrap

# Deploy to dev
cdk deploy --context environment=dev

# Deploy to production
cdk deploy --context environment=prod
```

## 2. Data Ingestion

### Add New Data Source

1. Create Glue crawler for source
2. Define schema in Data Catalog
3. Create Glue ETL job for transformation
4. Schedule job via EventBridge
5. Verify data in Athena

### Supported Formats

- CSV, JSON, Parquet, ORC
- Delta Lake (ACID transactions)
- Avro (schema evolution)

## 3. Query Operations

### Athena Queries

```sql
-- Query Delta Lake table
SELECT * FROM lakehouse.sales
WHERE year = 2024 AND month = 1
LIMIT 100;

-- Time travel query
SELECT * FROM lakehouse.sales VERSION AS OF 10;
```

### Query Federation

```sql
-- Cross-source query
SELECT * FROM awsdatacatalog.lakehouse.sales s
JOIN postgresql.public.customers c ON s.customer_id = c.id;
```

## 4. Monitoring

### Key Metrics to Watch

- **Glue jobs**: Duration, DPU usage, errors
- **Athena**: Query duration, data scanned, costs
- **S3**: Storage growth, request rates
- **EMR Serverless**: Job duration, resource usage

### Dashboards

Pre-configured dashboards for:

- ETL pipeline health
- Query performance
- Storage metrics
- Cost tracking

## 5. Maintenance

### Regular Tasks

- Run Delta Lake OPTIMIZE weekly
- VACUUM old versions monthly
- Review partition strategy quarterly
- Update Glue job scripts as needed

### Delta Lake Maintenance

```sql
-- Optimize for better query performance
OPTIMIZE lakehouse.sales;

-- Remove old versions
VACUUM lakehouse.sales RETAIN 168 HOURS;
```

### Teardown

```bash
cdk destroy --context environment=dev
```

> For troubleshooting common issues, see `docs/troubleshooting.md`.
