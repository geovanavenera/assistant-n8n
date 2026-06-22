
# Assistente de RH com IA — n8n + Telegram + MySQL

Projeto desenvolvido durante o curso **Oracle ONE AI For Tech**, com foco em automação com agentes de IA usando n8n.

A ideia é simples: um funcionário manda uma mensagem no Telegram perguntando sobre férias, políticas da empresa ou qualquer coisa de RH — e o agente responde consultando o banco de dados e a documentação da empresa automaticamente.

---

## Como funciona

```
Telegram → n8n (AI Agent) → MySQL + Vector Store → Telegram
```

1. O usuário manda uma mensagem pelo Telegram
2. O agente classifica se a pergunta é sobre RH ou fora do escopo
3. Se for RH, consulta o banco de dados MySQL e/ou a documentação via Vector Store
4. Responde direto no Telegram com a informação

---

## Stack

| Ferramenta | Uso |
|---|---|
| n8n | Orquestração do fluxo |
| Telegram | Interface com o usuário |
| Cohere | Modelo de linguagem + embeddings |
| MySQL | Dados dos funcionários |
| Railway | Hospedagem do banco de dados |
| Simple Vector Store | Armazenamento de documentos de RH |

---

## Funcionalidades

- Consulta de informações de funcionários por nome (com normalização para minúsculas e espaços extras)
- Acesso a políticas e documentos da empresa via busca semântica
- Classificação de intenção antes de acionar o agente, evitando buscas desnecessárias
- Memória de conversa para contexto entre mensagens

---

## Estrutura do fluxo no n8n

```
Telegram Trigger
    └── AI Agent
            ├── Cohere Chat Model
            ├── Simple Memory
            ├── Simple Vector Store (documentos)
            └── MySQL Tool (dados dos funcionários)
                    └── Send Message (resposta)
```

---

## Melhorias implementadas além do projeto base

- Normalização de nomes no SQL com `LOWER()` e `TRIM()`
- Remoção da mensagem automática do n8n nas respostas

---

## Como rodar

1. Importe o arquivo `workflow.json` no seu n8n
2. Configure as credenciais: Telegram Bot, Cohere API e MySQL
3. Suba o banco de dados no Railway e ajuste a connection string
4. Ative o workflow e teste mandando uma mensagem no Telegram

---

## Aprendizados

Foi meu primeiro projeto com agente de IA do zero. Tive que debugar bastante a conexão com o banco, a normalização de nomes e o fluxo de classificação de intenção — mas no final ficou funcional e com cara de coisa real.
