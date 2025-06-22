+<h1 align="center"> Agente_NF - Assistente Inteligente para Notas Fiscais</h1>

<p align="center">
  Agente desenvolvido no curso <strong>Agentes Autônomos com Redes Generativas</strong> da <a href="https://www.i2a2.com.br/">I2A2</a>.
</p>

---

### Tecnologias e Frameworks Utilizados

<p align="left">
  <img src="https://img.shields.io/badge/-n8n-333333?style=flat&logo=n8n" />
  <img src="https://img.shields.io/badge/-OpenAI-333333?style=flat&logo=openai" />
  <img src="https://img.shields.io/badge/-Supabase-333333?style=flat&logo=supabase" />
</p>

Neste projeto, foi utilizada uma arquitetura **low-code**, com foco em automação inteligente e integração de dados em tempo real:

- **n8n**: Plataforma de automação baseada em nós.
- **OpenAI API**: Geração de linguagem natural contextualizada (modelo GPT-4.1-mini).
- **Supabase**: Banco de dados PostgreSQL para armazenamento das notas fiscais e seus itens.

---

### Componentes Usados no n8n

- **🔹 Chat Trigger**  
  Utilizado para simular ou receber mensagens reais de usuários. Pode futuramente ser integrado ao WhatsApp ou Telegram.

- **🧠 AI Agent (OpenAI)**  
  Responsável por interpretar e gerar respostas inteligentes. Utiliza prompt customizado e conexão com ferramentas para tomada de decisão.

- **🗄️ PostgreSQL Tools**  
  Dois nós para consultas diretas na base Supabase:
  - `nfs_cabecalho`: dados gerais da nota fiscal.
  - `nfs_itens`: produtos e serviços relacionados à nota.

- **💬 Memória de Conversa (memoryBufferWindow)**  
  Permite manter o contexto das últimas 8 interações para respostas mais coerentes e naturais.

---

### Estrutura do Banco de Dados (Supabase)

| Tabela         | Descrição                                                       |
|----------------|-----------------------------------------------------------------|
| `nfs_cabecalho` | Informações gerais da nota (emitente, valor, data, etc.).       |
| `nfs_itens`     | Itens da nota (produto, quantidade, valor, CFOP, etc.).         |

As tabelas se relacionam pela coluna `CHAVE_DE_ACESSO`, permitindo consultas cruzadas entre cabeçalho e itens da nota.

---

### Arquitetura Geral:
Usuário 
- ChatTrigger (n8n) 
- AI Agent (OpenAI + Prompt + Ferramentas) 
- PostgreSQL Tool (nfs_cabecalho e nfs_itens) 
- AI Agent 
- Resposta ao Usuário

---

### Etapas do Funcionamento

1. **Recepção da Mensagem**
   - Trigger de chat inicia a conversa com uma saudação personalizada.

2. **Processamento da Pergunta**
   - AI Agent identifica a intenção do usuário.
   - Utiliza mensagens de sistema robustas para guiar o comportamento do modelo.

3. **Consulta aos Dados**
   - Com base na `CHAVE_DE_ACESSO`, realiza buscas precisas nas tabelas do Supabase.

4. **Memória de Conversa**
   - Mantém contexto de até 8 mensagens para manter coerência.

5. **Geração da Resposta**
   - Se houver dados: retorna uma resposta clara e informativa.
   - Se não houver: responde com transparência ao usuário.

---

### 🌐 Acesse o Agente Online

[🔗 Clique aqui para acessar o agente](https://silvia-rodrigues.app.n8n.cloud/webhook/9dd6b60e-6c9f-477d-bb5f-56626ccd1b6a/chat)


### Nome do Grupo: Agentes Inteligentes Legacy
Alunos:
1. Arthur Neves de Oliveira Santos
2. Fabiana Gonçalves
3. Francisco Alisson de Souza
4. Patrícia Monteiro Barbosa
5. Silvia Marques Almeida Rodrigues
---








