# Revisão da base de código: problemas e tarefas sugeridas

## 1) Tarefa para corrigir erro de digitação
**Problema encontrado:** no README há erros de escrita em inglês que afetam clareza.
- "Clone the repository and **made** updates..." (o correto é "make updates").
- "...will require **stoping** and restarting Jekyll" (o correto é "stopping").

**Tarefa sugerida:**
- Corrigir os erros de digitação no `README.md` e fazer uma varredura rápida adicional por termos semelhantes.

**Critério de aceite:**
- Trechos corrigidos para inglês gramaticalmente correto.
- Sem alteração de significado das instruções.

## 2) Tarefa para corrigir um bug
**Problema encontrado:** a função `parse_markdown_cv` em `scripts/cv_markdown_to_json.py` usa detecção de seção com regex muito ampla (`^([A-Za-z\s]+)$`), o que pode interpretar linhas comuns de texto como títulos de seção e quebrar o parsing do CV.

**Tarefa sugerida:**
- Ajustar a lógica de identificação de seções para usar delimitadores mais robustos (por exemplo, títulos Markdown reais, lista de seções esperadas, ou regras baseadas em contexto).
- Adicionar validação para evitar criação de seções espúrias.

**Critério de aceite:**
- CV de exemplo é parseado sem seções incorretas.
- Conteúdo textual não estruturado não passa a ser tratado como título.

## 3) Tarefa para ajustar comentário/discrepância de documentação
**Problema encontrado:** o `README.md` referencia "LICENSE.md", mas no repositório o arquivo presente é `LICENSE`.

**Tarefa sugerida:**
- Atualizar a referência no README para apontar para `LICENSE`.
- Revisar links internos equivalentes no README para evitar outros caminhos inválidos.

**Critério de aceite:**
- Link/menção de licença consistente com o nome real do arquivo.
- Sem links quebrados na documentação principal.

## 4) Tarefa para melhorar um teste
**Problema encontrado:** não há testes automatizados para o script `scripts/cv_markdown_to_json.py`, que contém regras de parsing com risco de regressão.

**Tarefa sugerida:**
- Criar testes unitários (ex.: `pytest`) cobrindo ao menos:
  1. extração de seções válidas,
  2. prevenção de seções falsas,
  3. parse de educação com/sem GPA,
  4. parse de experiência com intervalos de datas e bullets.
- Incluir um fixture de CV mínimo e um fixture com casos limite.

**Critério de aceite:**
- Suite de testes executa localmente com comando único.
- Cobertura mínima das funções críticas de parsing definida no PR.
