# Exemplo: CLAUDE.md para repo Backend (API)

Este é um exemplo de como configurar o `CLAUDE.md` de um repo backend que consome os agentes do vault.

---

# API do Produto Z

API REST em Python/FastAPI com PostgreSQL. Serve o frontend web e o app mobile.

## Stack

- **Runtime**: Python 3.12
- **Framework**: FastAPI + SQLAlchemy 2.0 + Alembic
- **DB**: PostgreSQL 16 (RDS)
- **Cache**: Redis (ElastiCache)
- **CI/CD**: GitHub Actions → ECR → ECS Fargate
- **Monitoramento**: Datadog APM + CloudWatch

## Estrutura do repo

```
src/
  api/            — rotas FastAPI (por domínio: users/, orders/, payments/)
  models/         — SQLAlchemy models
  services/       — lógica de negócio
  repositories/   — acesso a dados
tests/
  unit/
  integration/
alembic/          — migrations
docker-compose.yml
```

## Convenções

- Type hints em tudo — `mypy --strict` no CI
- Testes: `pytest` com coverage mínimo 80%
- Migrations: sempre reversíveis (`upgrade` + `downgrade`)
- Env vars via `.env` (nunca commitado) — template em `.env.example`
- Branches: `feature/`, `fix/`, `chore/` → PR → `main`

## Cérebro auxiliar

- **Vault path**: `/home/usuario/Documents/meu-vault`
- **Pasta do cliente**: `Trabalho/Produto Z`

## Status atual

| Feature | Status | Notas |
|---------|--------|-------|
| Auth (JWT) | Done | Refresh token flow |
| Users CRUD | Done | |
| Orders | In Progress | Falta webhook de pagamento |
| Payments | Not Started | Integração Stripe pendente |

## Limitações conhecidas

- Rate limiting ainda não implementado (usando Cloudflare como workaround)
- Bulk operations sem paginação server-side em `/orders`
