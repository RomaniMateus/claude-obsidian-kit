# Agentes do Claude

Fonte única de agentes. Repos de trabalho consomem via symlink (`repo/.claude/agents/ → vault/Agentes/`).

**Regra**: agentes são genéricos — sem menção a cliente, conta ou path. O contexto vem do `CLAUDE.md` de cada repo.

## Pipeline principal

| Agente | Função | Quando usar |
|--------|--------|-------------|
| [[Agentes/orchestrator\|orchestrator]] | Coordenador — quebra tarefas, delega, consolida | Tarefas complexas com múltiplas etapas |
| [[Agentes/engineer\|engineer]] | Executor técnico — escreve/modifica código | Implementação de features, refactoring |
| [[Agentes/code-reviewer\|code-reviewer]] | Revisor — checa qualidade, segurança, convenções | Antes de merge/deploy |
| [[Agentes/docs-generator\|docs-generator]] | Documentação — README, runbooks, CHANGELOG | Após mudanças significativas |

## Suporte

| Agente | Função | Quando usar |
|--------|--------|-------------|
| [[Agentes/daily-reporter\|daily-reporter]] | Relatório diário + log no vault | Final do dia |
| [[Agentes/incident-responder\|incident-responder]] | Análise de incidente + post-mortem no vault | Durante/após incidentes |
| [[Agentes/prompt-crafter\|prompt-crafter]] | Refina objetivos em prompts otimizados | Quando o pedido é vago |
| [[Agentes/cert-tutor\|cert-tutor]] | Tutor de certificações com spaced repetition | Sessões de estudo |

## Como consumir em um repo

```bash
mkdir -p .claude/agents
ln -s /caminho/do/vault/Agentes/*.md .claude/agents/
```
