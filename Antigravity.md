# Guia do Antigravity para Criação de Fluxos no n8n

Este guia define as diretrizes, metodologias e padrões que eu (Antigravity) seguirei ao trabalhar com você na criação, depuração e gerenciamento de fluxos de trabalho no n8n. Este processo utilizará fortemente as capacidades do servidor MCP (`n8n-mcp`) e as melhores práticas das Skills do n8n (`n8n-skills`).

---

## 🚀 Como Trabalharemos Juntos

A construção de fluxos programáticos exige precisão. O processo seguirá estes passos centrais:

1. **Descoberta via Templates (Sempre a prioridade)**
   Antes de construir qualquer configuração do zero, procurarei em modelos já existentes (`search_templates`) baseados no que você precisa (ex: processamento de webhooks, integrações com o Slack, IA agentes).

2. **Pesquisa e Configuração de Nós (_Nodes_)**
   Caso não exista um modelo, buscarei os nós adequados (`search_nodes` e `get_node`). Prestarei atenção extra às operações suportadas e a quais propriedades dependem de outras (ex: `sendBody` ativando `contentType`).

3. **Validação Rigorosa e em Múltiplos Níveis**
   Nunca entregaremos um fluxo sem validá-lo. O fluxo passará por:
   - Validação mínima (checagem rápida de campos obrigatórios).
   - Validação completa (simulando tempo de execução).
   - Validação do fluxo estrutural e de expressões (conectividade e `JSONs` válidos).

4. **Iteração Silenciosa pelo MCP**
   Realizarei buscas (`search`), leituras de documentação (`docs`) e validações de ferramentas n8n operando em paralelo silenciosamente. Você não será bombardeado com meus pensamentos e requisições, apenas verá a resposta estruturada após as requisições obterem sucesso.

---

## 🧠 Conhecimento Absorvido (n8n-skills)

Ao criar seu fluxo no n8n, aplicarei essas habilidades intrínsecas documentadas pelas `n8n-skills`:

### 1. Sintaxe de Expressão n8n
- Uso impecável de expressões como `$json`, `$node`, `$now`, e `$env`.
- Cuidado Crítico: Os dados originados de *webhooks* ou requisições sempre estarão estruturados dentro de `$json.body` ou `$json.query`.

### 2. Padrões de Arquitetura Comprovados
- Empregarei padrões baseados no mundo real na concepção do fluxo (processamento em batch realista, lógica assíncrona, arquitetura com subfluxos quando complexo, etc.).

### 3. Escrevendo Código Otimizado (Code Nodes)
- **Preferência pelo JavaScript:** Apenas usarei Python se estritamente necessário. O JavaScript suporta todo contexto fundamental.
- Acesso de entrada: Utilizarei os padrões atualizados como `$input.all()`, `$input.first()` e `$input.item()`.
- O retorno do nó código SEMPRE será um *array* com campos `json`, exemplo: `[{json: { chave: "valor" }}]`.

---

## ⚠️ Regras Essenciais e Armadilhas Evitadas

1. **NUNCA confiar nos padrões (Defaults)!**
   Valores padrões são a causa #1 de falhas nos fluxos dinâmicos em momento de execução. Sempre escreverei parâmetros essenciais de forma explícita.

2. **Cuidado nas conexões condicionais (nó `IF` / `Switch`)**
   Quando definir dependências e conexões, utilizarei as rotas lógicas adequadamente (como o uso do parâmetro `branch: "true"` ou `branch: "false"`) nas definições do nó ou comandos do MCP.

3. **Validação contra "Falsos Positivos"**
   Entendo o processo de validação de *loop*. Se esbarrarmos num erro do nó de validação, auto-corrigirei ou trarei clareza caso o *schema* do MCP esteja agindo como um falso-positivo.

---

## 🛠️ Passos Seguintes

Para ativarmos este trabalho de alta velocidade:

1. Assim que instalarmos o MCP do n8n em seu editor / ambiente Claude, teremos acesso a ferramentas como: `search_templates`, `get_node`, `validate_node`, `n8n_test_workflow`, etc.
2. Certifique-se de configurar o MCP conforme especificado pelo criador (@czlonkowski) passando o seu `N8N_API_URL` e `N8N_API_KEY` para que eu tenha poderes não apenas documentais, mas de implantação de fluxos completos.

Me diga qual será nosso primeiro fluxo de automação para que possamos começar!
