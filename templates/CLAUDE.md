# [Nome do Vault] — Obsidian Vault

Vault pessoal de um [sua profissão]. **Não é um repo de código** — é uma base de conhecimento em Obsidian. Todas as notas usam Obsidian-flavored markdown com wiki-links (`[[...]]`).

## Estrutura

```
Agentes/        — prompts de agentes Claude (.md). Fonte única: repos de trabalho consomem via symlink.
Trabalho/       — notas por cliente/projeto. Decisões, reuniões, incidentes.
Estudos/        — estudo pessoal. Trilhas, certificações.
Conceitos/      — notas transversais que conectam Trabalho ↔ Estudos via backlinks.
Arquivos/       — imagens, diagramas, anexos.
```

## Convenções obrigatórias

- **Idioma**: português para conteúdo, inglês para termos técnicos.
- **Links internos**: sempre `[[pasta/nota]]` (wiki-link Obsidian), nunca markdown links relativos.
- **Notas em Conceitos/**: só existem quando o mesmo tema aparece em Trabalho **e** em Estudos. Cada nota deve ter backlinks para ambos os lados.
- **MOC.md**: cada pasta tem um Map of Contents. Ao criar nota nova, **sempre adicione o link no MOC da pasta**.
- **Frontmatter**: notas de aula usam frontmatter com `tópico`, `domínio`, `data`, `sessão`. Demais notas não precisam.

## Agentes

Os agentes em `Agentes/` são **genéricos** — não mencionam cliente, conta ou path de repo. O contexto concreto vem do `CLAUDE.md` de cada repo que consome o agente.

**NUNCA modifique um agente sem confirmar com o usuário** — a alteração afeta todos os repos que o consomem via symlink.

Repos que hoje consomem:
- `/caminho/para/repo-1`
- `/caminho/para/repo-2`

<!-- Adicione mais repos conforme conectar -->

## Certificação em andamento

<!-- Descomente e preencha se estiver estudando para uma cert -->
<!--
**[NOME DA CERT]** — plano de X semanas, Yh/semana. Progresso em:
- `Estudos/Certificações/[CERT]/MOC.md` — plano macro
- `Estudos/Certificações/[CERT]/Log de estudos.md` — diário de sessões
- `Estudos/Certificações/[CERT]/Pontos fracos.md` — tópicos com erro recorrente
- `Estudos/Certificações/[CERT]/Cronograma diário.md` — distribuição semanal

O agente `cert-tutor` conduz sessões de estudo.
-->

## Clientes/Projetos ativos

| Cliente/Projeto | Descrição | Repo |
|-----------------|-----------|------|
| Exemplo Corp | Migração de infra | `/caminho/para/repo` |

## O que NÃO fazer

- **Não crie notas soltas** — toda nota pertence a uma pasta e deve estar no MOC correspondente.
- **Não duplique conteúdo** entre Trabalho e Estudos — se o tema cruza, crie/atualize em `Conceitos/` e linke dos dois lados.
- **Não use markdown links** (`[texto](path)`) — use wiki-links (`[[path|texto]]`).
- **Não assuma que este vault é um repo git** — pode não ser versionado.
