Faça uma varredura de saúde no vault Obsidian e reporte o que precisa de atenção.

## Verificações

### 1. Notas órfãs
Procure arquivos `.md` (exceto MOCs) que **não são referenciados** por nenhum `[[backlink]]` em outra nota.

### 2. MOCs desatualizados
Para cada pasta que tem `MOC.md`, verifique se **todas as notas .md da pasta** estão listadas no MOC.

### 3. Links quebrados
Procure `[[...]]` que apontam para notas que **não existem**.

### 4. Conceitos candidatos
Procure temas que aparecem tanto em `Trabalho/` quanto em `Estudos/` mas que **não têm** nota em `Conceitos/`.

### 5. Agentes — consistência
Verifique se os agentes em `Agentes/` estão consistentes:
- Nenhum agente referencia cliente específico (devem ser genéricos)
- Todos listados no `Agentes/MOC.md`

## Formato de saída

### Vault saudável
[o que está OK]

### Precisa de atenção
[problemas encontrados, com path do arquivo e sugestão de fix]

### Oportunidades
[conceitos candidatos, notas que poderiam ser conectadas melhor]
