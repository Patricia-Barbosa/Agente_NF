<h1 align="center"> Agente_NF - Assistente Inteligente para Notas Fiscais (Python/Langchain)</h1>

<p align="center">
  Agente desenvolvido no curso <strong>Agentes Autônomos com Redes Generativas</strong> da <a href="https://www.i2a2.com.br/">I2A2</a>.
</p>

---

### Tecnologias e Frameworks Utilizados

<p align="left">
  <img src="https://img.shields.io/badge/-Python-3776AB?style=flat&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/-Langchain-333333?style=flat" />
  <img src="https://img.shields.io/badge/-Pandas-150458?style=flat&logo=pandas&logoColor=white" />
  <img src="https://img.shields.io/badge/-OpenRouter-333333?style=flat" />
  <img src="https://img.shields.io/badge/-MistralAI-ff7700?style=flat" />
  <img src="https://img.shields.io/badge/-Matplotlib-333333?style=flat&logo=matplotlib&logoColor=white" />
  <img src="https://img.shields.io/badge/-Flask-000000?style=flat&logo=flask&logoColor=white" />
  <img src="https://img.shields.io/badge/-Ngrok-0055DA?style=flat&logo=ngrok&logoColor=white" />
  <img src="https://img.shields.io/badge/-Google Colab-F9AB00?style=flat&logo=googlecolab&logoColor=black" />
  <img src="https://img.shields.io/badge/-Google Drive-4285F4?style=flat&logo=googledrive&logoColor=white" />
</p>

Neste projeto, foi utilizada uma arquitetura baseada em Python e Langchain para criar um agente capaz de analisar dados de notas fiscais armazenados em arquivos CSV:

- **Python**: Linguagem de programação principal.
- **Langchain**: Framework para desenvolvimento de aplicações com LLMs, utilizado para criar os agentes.
- **Pandas**: Biblioteca para manipulação e análise dos dados das notas fiscais carregados em DataFrames.
- **OpenRouter (com Mistral 7B Instruct)**: Serviço intermediário para acesso ao modelo de linguagem grande (LLM) Mistral AI, responsável pela interpretação das perguntas e geração das respostas.
- **Matplotlib**: Biblioteca para geração de gráficos (produtos mais vendidos, vendas por mês).
- **Flask & Ngrok**: Utilizados opcionalmente para criar uma interface web simples (chat) e expô-la publicamente.
- **Google Colab**: Ambiente de notebook utilizado para desenvolvimento e execução.
- **Google Drive**: Utilizado para armazenar os arquivos CSV das notas fiscais e o arquivo requirements.txt.

---

### Componentes Principais (Notebook Python)

- **🔹 Carregamento de Dados** &nbsp;&nbsp;
  Leitura de arquivos `202401_NFs_Cabecalho.csv` e `202401_NFs_Itens.csv` do Google Drive para DataFrames Pandas (df_cabecalho, df_itens).

- **🧠 Agentes Langchain (create_pandas_dataframe_agent)** &nbsp;&nbsp;
  `agent_cabecalho_executor`: Especializado em responder perguntas sobre os dados gerais da nota fiscal (cabeçalho). Utiliza memória para manter contexto.
  `agent_itens_executor`: Especializado em responder perguntas sobre os produtos/serviços das notas (itens).

- **🤖 LLM (OpenRouter + Mistral)** &nbsp;&nbsp;
  Instância `ChatOpenAI` configurada para usar o modelo `mistralai/mistral-7b-instruct` via OpenRouter. Chave de API gerenciada via Google Colab Secrets.

- **📊 Função de Visualização (responder_visual)** &nbsp;&nbsp;
  Lógica customizada em Python/Pandas/Matplotlib para gerar gráficos (barras, linhas) e relatórios tabulares com base na pergunta do usuário.

- **💬 Memória de Conversa (ConversationBufferMemory)** &nbsp;&nbsp;
  Utilizada especificamente pelo `agent_cabecalho_executor` para permitir perguntas de acompanhamento mantendo o contexto.

- **🌐 Interface Web (Opcional - Flask/Ngrok)** &nbsp;&nbsp;
  Uma aplicação Flask simples que fornece uma interface de chat e usa Ngrok para criar um túnel público temporário.

---

### Estrutura dos Dados (CSVs no Google Drive)

| Arquivo/DataFrame | Descrição |
|---|---|
| `df_cabecalho` | Informações gerais da nota (emitente, valor, data, etc.). |
| `df_itens` | Itens da nota (produto, quantidade, valor, CFOP, NCM, etc.). |

Os DataFrames se relacionam pela coluna `CHAVE DE ACESSO`, permitindo análises que cruzam informações do cabeçalho e dos itens.

---

### Arquitetura Geral:
Usuário -> Interface (Colab ou Chat Flask/Ngrok) -> Roteamento (pergunta para Agente Cabeçalho, Agente Itens ou Função Visual) -> Ferramentas (Pandas para consulta, Matplotlib para gráficos) + LLM (OpenRouter/Mistral para interpretação e geração) -> Resposta ao Usuário

---

### Etapas do Funcionamento

1.  **Recepção da Pergunta**
    &nbsp; O usuário digita a pergunta em uma célula do Colab (usando `invoke` nos agentes ou chamando `responder_visual`) ou na interface web (Flask).

2.  **Processamento da Pergunta**
    &nbsp; A lógica (na função `responder_visual` ou no código do Flask) direciona a pergunta para o agente correto (Cabeçalho ou Itens) ou para a lógica de gráficos/relatórios. Os agentes usam o LLM (Mistral) para planejar a execução.

3.  **Consulta/Geração**
    &nbsp; **Agentes**: O LLM gera código Python (Pandas) que é executado sobre os DataFrames.
    &nbsp; **Função Visual**: O código Python/Pandas/Matplotlib é executado diretamente para gerar gráficos ou tabelas.

4.  **Memória de Conversa**
    &nbsp; O `agent_cabecalho_executor` armazena o histórico recente para responder perguntas subsequentes com contexto.

5.  **Geração da Resposta Final**
    &nbsp; **Agentes**: O resultado da execução do código é enviado ao LLM, que formata a resposta final em linguagem natural.
    &nbsp; **Função Visual**: O gráfico Matplotlib é exibido ou a tabela Pandas é mostrada.

---

### ⚙️ Como Executar (Google Colab)

**Pré-requisitos:**
- Conta Google com acesso ao Google Drive.
- Arquivos `202401_NFs_Cabecalho.csv` e `202401_NFs_Itens.csv` no seu Google Drive.
- Arquivo `requirements.txt` salvo no seu Google Drive.
- Conta no OpenRouter.ai com Chave de API ativa.
- (Opcional) Conta no Ngrok e Authtoken.

**Configuração no Colab:**
1. Abra o notebook `Homologacao_Arthur_Agente_Desafio_Final.ipynb` no Google Colab.
2. No painel esquerdo, clique no ícone de chave (🔑 Secrets).
3. Adicione um novo Secret com o nome `OPENROUTER_API_KEY` e cole sua chave.
4. (Opcional) Adicione um novo Secret com o nome `NGROK_AUTHTOKEN` e cole seu token.

**Execução:**
1. Execute a Célula 1 (Passo 1) para instalar as dependências.
2. **IMPORTANTE:** Após a primeira instalação, **REINICIE O AMBIENTE DE EXECUÇÃO** (Runtime -> Restart session).
3. Execute as células seguintes na ordem (Célula 2, 2.1, 3, 4, 5, 6, 7, 9).
4. (Opcional) Execute a Célula 8 para iniciar a interface web Flask/Ngrok.

---

### 🌐 Acesso Online (Opcional via Ngrok)

Para usar a interface web (se a Célula 8 for executada com sucesso):

1.  Execute a Célula 8 no notebook.
2.  Copie a URL `https://....ngrok-free.app` que aparece na saída.
3.  Abra essa URL em um navegador para interagir com o agente via chat.

*Nota: O túnel Ngrok é temporário e será desativado quando a célula parar de executar.*

---

### Nome do Grupo: Agentes Inteligentes Legacy
Alunos:
1. Arthur Neves de Oliveira Santos
2. Fabiana Gonçalves
3. Patrícia Monteiro Barbosa
4. Silvia Marques Almeida Rodrigues
---
