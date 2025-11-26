# Troubleshooting

Common issues and resolutions for the **Serverless Data Lakehouse**.

## Glue ETL Issues

### 1. Glue Job Fails to Start

**Symptom:** Job stuck in "STARTING" or fails immediately.

**Resolution:**
- Check IAM role has required permissions
- Verify VPC configuration if using private subnets
- Check Glue service quotas
- Review CloudWatch logs for errors

### 2. Glue Job Out of Memory

**Symptom:** Job fails with OOM or runs very slowly.

**Resolution:**
- Increase number of DPUs
- Use Glue 3.0+ for better memory management
- Partition input data for parallel processing
- Enable job bookmarks for incremental processing

### 3. Schema Mismatch Errors

**Symptom:** Job fails due to schema evolution.

**Resolution:**
- Update Glue crawler to detect new schema
- Use Delta Lake schema evolution features
- Add schema validation in ETL logic
- Review source data for unexpected changes

## Athena Query Issues

### 4. Query Timeout

**Symptom:** Queries exceed timeout limit.

**Resolution:**
- Add partition filters to reduce scan
- Use columnar format (Parquet/Delta)
- Optimize table with MSCK REPAIR
- Consider materialized views for complex queries

### 5. High Query Costs

**Symptom:** Athena costs higher than expected.

**Resolution:**
- Review query patterns – add partition pruning
- Convert to columnar format
- Use Athena workgroups with cost limits
- Cache frequent query results

## Delta Lake Issues

### 6. Transaction Conflicts

**Symptom:** Concurrent writes failing.

**Resolution:**
- Implement retry logic with backoff
- Use partition-level isolation
- Review write patterns for conflicts
- Consider merge operations for updates

### 7. Small File Problem

**Symptom:** Query performance degraded over time.

**Resolution:**
- Run OPTIMIZE to compact files
- Configure auto-compaction
- Review ingestion batch sizes
- Schedule regular maintenance jobs

## Lake Formation Issues

### 8. Permission Denied Errors

**Symptom:** Users can't access tables they should.

**Resolution:**
- Check Lake Formation permissions
- Verify IAM role trust relationships
- Review column-level permissions
- Check data location permissions

## Cost Issues

### 9. Unexpected High Costs

**Symptom:** Monthly bill higher than estimates.

**Resolution:**
- Review Athena query patterns – optimize scans
- Check Glue DPU usage – right-size jobs
- Implement S3 lifecycle policies
- Use Glue job bookmarks for incremental processing

> For architecture details, see `ARCHITECTURE.md`.
