# Exemplo: CLAUDE.md para repo DevOps (Terraform/Terragrunt)

Este é um exemplo de como configurar o `CLAUDE.md` de um repo de infraestrutura que consome os agentes do vault.

---

# Projeto XYZ — IaC Transcription

Migração de infraestrutura AWS para Terraform/Terragrunt gerenciado como código.

## Stack

- **IaC**: Terraform 1.9+ com Terragrunt 1.0+
- **Cloud**: AWS
- **Contas**: `dev` (123456789012), `prod` (987654321098)
- **Região primária**: us-east-1
- **Região DR**: us-west-2

## Estrutura do repo

```
modules/         — módulos Terraform reutilizáveis por domínio
live/            — leaves Terragrunt por account/region/domain
root.hcl         — configuração raiz Terragrunt (backend S3, provider)
CLAUDE.md        — este arquivo
PROGRESS.md      — status atual das tarefas
```

## Convenções

- Resource names em `snake_case`
- Variáveis tipadas com `description`
- `provider.tf` gerado pelo Terragrunt, não versionado em `modules/`
- Nunca `terraform apply` sem aprovação humana
- Apenas `validate`, `plan`, `fmt` automatizados

## Cérebro auxiliar

- **Vault path**: `/home/usuario/Documents/meu-vault`
- **Pasta do cliente**: `Trabalho/Cliente XYZ`

O orchestrator usa estas informações para persistir decisões, incidentes e logs no vault.

## Status atual

| Domínio | Status | Notas |
|---------|--------|-------|
| network | Done | VPC, subnets, NAT, IGW |
| compute | In Progress | EC2, ASG, ALB |
| storage | Not Started | S3, EFS |
| iam | In Progress | Roles, policies |

## Limitações conhecidas

- S3 bucket policies em inline style (Terraformer legacy)
- Alguns IDs hardcoded em `locals.tf` (migrar para `dependency` blocks)
