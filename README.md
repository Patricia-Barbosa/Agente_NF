# Agente_NF
Agente desenvolvido no curso Agentes Autônomos com  Redes Generativas da I2A2.
# Framework e Tecnologias Utilizadas
![N8N](https://img.shields.io/badge/-n8n-333333?style=flat&logo=n8n)

Neste projeto, foi utilizada uma arquitetura low-code com foco em automação inteligente e integração de dados em tempo real, por meio das seguintes tecnologias: n8n (Node-based Workflow Automation)
# Elementos usado no n8n:
*Trigger de Chat:*
- para receber mensagens do usuário de forma simulada ou real (como em um chatbot ou WhatsApp).
  
*AI Agent:*
- um nó com modelo de linguagem conectado à OpenAI, responsável por interpretar perguntas e gerar respostas com base nas consultas.
  
*Ferramentas PostgreSQL:* 
- dois nós conectados à base Supabase, um para a tabela nfs_cabecalho e outro para nfs_itens, ambos com consultas diretas aos dados.
  
*Memória de Conversa:*
- implementada com memoryBufferWindow, permite ao agente manter contexto e coerência nas interações.
- Modelo de Linguagem: GPT-4.1-mini foi utilizado inicialmente.
# Foi utilizado a API da OpenAI para gerar respostas naturais e contextualizadas. 
![OpenAI](https://img.shields.io/badge/-OpenAI-333333?style=flat&logo=OpenAI)

# Supabase.
![Supabase](https://img.shields.io/badge/-Supabase-333333?style=flat&logo=supabase)

Foi a plataforma escolhida para armazenar os dados estruturados em duas tabelas:

*nfs_cabecalho:* com dados gerais das notas fiscais (emitente, destinatário, valor, data, etc.).

*nfs_itens:* com os itens comercializados em cada nota (produto, quantidade, valor, CFOP, etc.).
A relação entre as tabelas se dá pela coluna "CHAVE_DE_ACESSO", permitindo ao agente realizar consultas cruzadas conforme a pergunta do usuário.
# Arquitetura Geral
Usuário → ChatTrigger (n8n) 
        → AI Agent (OpenAI + Regras) 
        → PostgreSQL Tool (Supabase - Tabelas nfs_cabecalho e nfs_itens) 
        → AI Agent → Resposta Inteligente ao Usuário
# Etapas e Componentes da Solução
1. Recepção de Mensagens (ChatTrigger)
2. O nó ChatTrigger simula a entrada de mensagens do usuário, podendo futuramente ser integrado ao WhatsApp ou Telegram.
- Mensagem de boas-vindas personalizada (“Olá! 👋 Meu nome é Sabrina...”) dá início à conversa.
3. Processamento da Pergunta (AI Agent + GPT)
- O AI Agent é o núcleo de tomada de decisão da solução.
- Ele utiliza:
o	System Message robusto para orientar o modelo de linguagem sobre como deve agir.
o	Conexões com ferramentas específicas para acesso seguro aos dados (nfs_cabecalho, nfs_itens).
- O modelo de linguagem GPT-4.1-mini (via OpenAI API) interpreta a pergunta do usuário e decide qual tabela consultar.
4. Consulta aos Dados (Supabase + PostgreSQL Tools)
- Dois nós PostgresTool fazem a ponte com o Supabase:
o	Um para a tabela nfs_cabecalho (dados da nota).
o	Outro para a tabela nfs_itens (produtos e serviços).
- As consultas são feitas com base na CHAVE_DE_ACESSO para manter a integridade relacional dos dados.
5. Memória de Conversa (Simple Memory)
- O componente memoryBufferWindow mantém o contexto de até 8 interações.
- Garante que o agente "lembre" de perguntas anteriores e mantenha coerência nas respostas.
6. Resposta ao Usuário
- O agente monta uma resposta clara e didática com base nos dados reais.
- Se os dados não estiverem disponíveis, o agente responde de forma transparente:
“Não é possível responder com os dados disponíveis.”
