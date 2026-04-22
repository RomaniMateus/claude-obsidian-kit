# Exemplo: CLAUDE.md para repo Data Engineering

Este é um exemplo de como configurar o `CLAUDE.md` de um repo de data pipeline que consome os agentes do vault.

---

# Pipeline de Dados — Analytics

ETL pipeline que ingere dados de múltiplas fontes, transforma e disponibiliza para BI.

## Stack

- **Orchestration**: Airflow 2.8 (MWAA)
- **Processing**: PySpark no EMR Serverless
- **Storage**: S3 (raw → refined → curated) + Iceberg tables
- **Catalog**: AWS Glue Data Catalog
- **BI**: Metabase conectado ao Athena
- **IaC**: Terraform para infra, dbt para transformações SQL

## Estrutura do repo

```
dags/             — DAGs do Airflow (por domínio: sales/, marketing/, finance/)
spark_jobs/       — PySpark jobs
dbt/
  models/         — transformações SQL (staging → intermediate → marts)
  tests/          — data quality tests
  macros/
infra/            — Terraform para EMR, MWAA, S3, Glue
```

## Convenções

- DAGs: prefixo `<domínio>__<nome>` (ex: `sales__daily_ingest`)
- S3 paths: `s3://bucket/{raw,refined,curated}/<domínio>/<tabela>/year=YYYY/month=MM/`
- dbt: nomenclatura `stg_`, `int_`, `fct_`, `dim_`
- Testes de qualidade obrigatórios: `not_null`, `unique` em PKs, `accepted_values` em enums
- Nunca deletar dados raw — lifecycle policy move para Glacier após 90 dias

## Cérebro auxiliar

- **Vault path**: `/home/usuario/Documents/meu-vault`
- **Pasta do cliente**: `Trabalho/Analytics Pipeline`

## Status atual

| Pipeline | Status | SLA | Notas |
|----------|--------|-----|-------|
| Sales daily | Prod | 06:00 UTC | Estável |
| Marketing events | Dev | - | Testando schema evolution |
| Finance reconciliation | Not Started | 08:00 UTC | Próximo sprint |

## Limitações conhecidas

- EMR Serverless tem cold start de ~3 min (impacta SLA de pipelines < 15 min)
- Glue Catalog não suporta column-level lineage nativo
