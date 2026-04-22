# Claude Code + Obsidian — Starter Kit

Um sistema que transforma seu vault Obsidian em **memória persistente** para agentes Claude Code. O trabalho que você faz nos seus repos vira conhecimento durável no vault — e o conhecimento do vault alimenta os agentes de volta.

## A ideia em 30 segundos

```
┌─────────────────────────────────────────────────────────┐
│                    OBSIDIAN VAULT                        │
│                                                         │
│  Trabalho/          Estudos/          Conceitos/        │
│  ├── Cliente A/     ├── Trilha X/     ├── Tema 1.md     │
│  │   ├── Log.md     ├── Trilha Y/     ├── Tema 2.md     │
│  │   ├── Decisões/  └── Certs/        └── ...           │
│  │   └── Incidentes/                                    │
│  └── Cliente B/                                         │
│                                                         │
│  Agentes/  ← fonte única de agentes (genéricos)        │
│  ├── orchestrator.md                                    │
│  ├── code-reviewer.md                                   │
│  └── ...                                                │
└───────────┬───────────────────────────┬─────────────────┘
            │ symlink                   │ symlink
            ▼                           ▼
     ┌──────────────┐           ┌──────────────┐
     │  Repo A      │           │  Repo B      │
     │  .claude/    │           │  .claude/    │
     │   agents/ ──►│ Agentes/  │   agents/ ──►│ Agentes/
     │  CLAUDE.md   │           │  CLAUDE.md   │
     │  (contexto)  │           │  (contexto)  │
     └──────────────┘           └──────────────┘
```

**Agentes ficam no vault** (genéricos, sem menção a cliente/projeto).
**Contexto fica no repo** (cada `CLAUDE.md` injeta o contexto específico).
**Symlinks conectam** — editar um agente no vault atualiza todos os repos.

## Por que funciona

1. **Sem duplicação**: um agente, N repos. O contexto muda, o comportamento não.
2. **Conhecimento durável**: decisões, incidentes e aprendizados ficam no vault com backlinks — não se perdem em threads de chat.
3. **Estudo integrado**: o que você aprende no trabalho vira nota de estudo (via `Conceitos/`), e vice-versa.
4. **Vault health**: slash commands verificam notas órfãs, MOCs desatualizados e links quebrados.

## Como usar este kit

### 1. Copie a estrutura para seu vault

```bash
# Copie os templates para o seu vault Obsidian
cp -r templates/* /caminho/do/seu/vault/
```

Isso cria:
- `Agentes/` com agentes genéricos prontos para adaptar
- `Conceitos/` com MOC vazio
- `.claude/commands/` com slash commands úteis
- `CLAUDE.md` template
- `MOC.md` raiz

### 2. Adapte o CLAUDE.md do vault

Abra `CLAUDE.md` e preencha:
- Sua área de atuação (DevOps, backend, data, etc.)
- Estrutura de pastas que faz sentido pro seu trabalho
- Clientes/projetos ativos
- Certificação em andamento (se houver)

### 3. Conecte seus repos de trabalho

Em cada repo que quiser usar os agentes:

```bash
# Crie o diretório .claude no repo
mkdir -p .claude/agents

# Symlink para os agentes do vault
ln -s /caminho/do/seu/vault/Agentes/*.md .claude/agents/

# Crie um CLAUDE.md no repo com o contexto específico
```

No `CLAUDE.md` do repo, adicione uma seção "Cérebro auxiliar" apontando pro vault:

```markdown
## Cérebro auxiliar

- **Vault path**: `/caminho/do/seu/vault`
- **Pasta do cliente**: `Trabalho/<nome do cliente>`
```

### 4. Personalize os agentes

Os agentes em `templates/Agentes/` são **genéricos de propósito**. Adapte para sua stack:
- `code-reviewer.md` — mude os checklist items para sua linguagem/framework
- `tf-engineer.md` → renomeie para `engineer.md` e adapte para seu domínio
- `cert-tutor.md` — mude a certificação alvo

### 5. Use os slash commands no vault

```bash
cd /caminho/do/seu/vault
claude  # abre o Claude Code no vault

# Dentro do Claude Code:
/garden          # verifica saúde do vault
/review-study    # revisa notas de estudo
/report          # gera relatório diário
```

## Estrutura do kit

```
templates/
├── CLAUDE.md                    # Template do vault — adapte para seu contexto
├── MOC.md                       # Hub raiz do vault
├── Agentes/
│   ├── MOC.md                   # Índice dos agentes
│   ├── orchestrator.md          # Coordenador principal
│   ├── code-reviewer.md         # Revisão de código
│   ├── daily-reporter.md        # Relatório diário + log no vault
│   ├── docs-generator.md        # Gerador de documentação
│   ├── incident-responder.md    # Resposta a incidentes + post-mortem
│   ├── prompt-crafter.md        # Refinador de prompts
│   ├── engineer.md              # Executor técnico (adapte para sua stack)
│   └── cert-tutor.md            # Tutor de certificações (qualquer cert)
├── Conceitos/
│   └── MOC.md
├── .claude/
│   └── commands/
│       ├── garden.md            # Varredura de saúde do vault
│       └── review-study.md      # Revisão de notas de estudo
examples/
├── CLAUDE-repo-devops.md        # Exemplo de CLAUDE.md para repo DevOps
├── CLAUDE-repo-backend.md       # Exemplo de CLAUDE.md para repo backend
└── CLAUDE-repo-data.md          # Exemplo de CLAUDE.md para repo data eng
```

## Princípios de design

### Agentes genéricos, contexto específico
Os agentes nunca mencionam cliente, conta, região ou path. Tudo isso vem do `CLAUDE.md` do repo. Isso permite que o mesmo agente funcione em qualquer projeto.

### Vault como cérebro auxiliar
O vault não é só anotação — é memória ativa. Os agentes **escrevem de volta** no vault:
- `orchestrator` → decisões em `Trabalho/<cliente>/Decisões/`
- `daily-reporter` → log em `Trabalho/<cliente>/Log de trabalho.md`
- `incident-responder` → post-mortems em `Trabalho/<cliente>/Incidentes/`

### MOC everywhere
Toda pasta tem um `MOC.md`. Toda nota nova é adicionada ao MOC. Isso garante que nada se perde no vault.

### Conceitos como ponte
`Conceitos/` só existe quando um tema cruza trabalho e estudo. Cada nota tem backlinks para ambos os lados — o grafo do Obsidian mostra as conexões.

## FAQ

**Preciso do Obsidian?**
Tecnicamente não — funciona com qualquer editor de markdown. Mas o Obsidian dá o grafo de backlinks, a busca por `[[wiki-links]]` e os plugins que fazem o vault brilhar.

**Funciona com qualquer linguagem/stack?**
Sim. Os agentes são templates — adapte o `code-reviewer` para Python, Go, Rust, whatever. O sistema é agnóstico de stack.

**Precisa ser git?**
O vault não precisa ser git (o meu não é). Os repos de trabalho normalmente são.

**Posso ter mais de uma certificação?**
Sim. Crie uma pasta por cert em `Estudos/Certificações/` e o `cert-tutor` detecta automaticamente.
