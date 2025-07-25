
<h1 align="center"> Agente_NF - Assistente Inteligente para Notas Fiscais</h1>

<p align="center">
  Agente desenvolvido no curso <strong>Agentes Autônomos com Redes Generativas</strong> da <a href="https://www.i2a2.com.br/">I2A2</a>.
</p>

---

### Tecnologias e Frameworks Utilizados

<p align="left">
  <img src="https://img.shields.io/badge/-Python-333333?style=flat&logo=python" />
  <img src="https://img.shields.io/badge/-Pandas-333333?style=flat&logo=pandas" />
  <img src="https://img.shields.io/badge/-LangChain-333333?style=flat&logo=langchain" />
  <img src="https://img.shields.io/badge/-OpenRouter-333333?style=flat&logo=openai" />
  <img src="https://img.shields.io/badge/-Google%20Colab-333333?style=flat&logo=google-colab" />
</p>

Neste projeto, foi utilizada uma arquitetura baseada em Python para a criação de um agente inteligente, com foco em análise de dados e respostas em linguagem natural:

- **Python**: Linguagem principal para o desenvolvimento do agente.
- **Pandas**: Manipulação e análise de dados tabulares (CSV de notas fiscais).
- **LangChain**: Framework para construção de agentes com LLMs.
- **OpenRouter (Mistral-7B-Instruct)**: Plataforma para uso do modelo `mistralai/mistral-7b-instruct` via API.
- **Google Colab**: Ambiente em nuvem para execução do notebook interativo.

---

### Componentes Usados no Código

- **🧠 Agente LangChain (create_pandas_dataframe_agent)**  
  Responsável por interpretar perguntas e gerar respostas a partir dos DataFrames do Pandas. Utiliza prompt customizado e ferramentas Python para realizar operações nos dados.

- **📊 Pandas DataFrames**  
  Dois DataFrames principais para armazenamento e análise:

  - `df_cabecalho`: Dados gerais da nota (emitente, data, valor total, etc.).
  - `df_itens`: Produtos e serviços (descrição, valor, quantidade, CFOP, etc.).

- **💬 Memória de Conversa**  
  Embora o uso de `memoryBufferWindow` não esteja explícito, o agente preserva contexto básico durante a interação com o modelo de linguagem.

---

### Estrutura dos Dados (Pandas)

| DataFrame     | Descrição                                                        |
|---------------|------------------------------------------------------------------|
| `df_cabecalho`| Informações gerais da nota fiscal (emitente, data, valor, etc.) |
| `df_itens`    | Itens da nota (produto, quantidade, valor unitário, CFOP, etc.) |

Ambos os DataFrames são integrados pela coluna `CHAVE_DE_ACESSO`, permitindo análise cruzada entre itens e cabeçalhos.

---

### Arquitetura Geral:

Usuário  
→ Interface Web Flask (mensagem)  
→ Agente LangChain (Pandas + Prompt)  
→ DataFrames `df_cabecalho` e `df_itens`  
→ Agente LangChain  
→ Resposta ao Usuário

---

### Etapas do Funcionamento

1. **Recepção da Mensagem**
   - O usuário envia uma pergunta sobre notas fiscais por meio de uma interface web (Flask + HTML + JS).

2. **Processamento da Pergunta**
   - O agente interpreta a intenção da pergunta via modelo `mistralai/mistral-7b-instruct` utilizando LangChain.
   - Um prompt customizado define o comportamento analítico do agente.

3. **Consulta aos Dados**
   - O agente utiliza Pandas para filtrar, agrupar ou buscar informações nos CSVs carregados como DataFrames.
   - A coluna `CHAVE_DE_ACESSO` permite cruzamento de dados entre `df_cabecalho` e `df_itens`.

4. **Geração da Resposta**
   - O agente retorna a resposta de forma clara, objetiva e em português.
   - Em caso de ausência de dados, a resposta é transparente ao usuário.

---

### 🌐 Acesse o Agente Online

> Atualmente, o agente é executado em ambiente Google Colab e exposto por ngrok.  
> Para testar, execute o notebook `Arthur_Agente_Desafio_3.ipynb`.

---

### Nome do Grupo: Agentes Inteligentes Legacy

Alunos:
1. Arthur Neves de Oliveira Santos  
2. Fabiana Gonçalves  
3. Francisco Alisson de Souza  
4. Patrícia Monteiro Barbosa  
5. Silvia Marques Almeida Rodrigues

---
