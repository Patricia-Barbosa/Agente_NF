# Agente Inteligente para Cálculo de Vale Refeição (VR)

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-2.0-blue.svg)
![LangChain](https://img.shields.io/badge/LangChain-0.1-blue.svg)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)

Este projeto, desenvolvido como parte do Desafio 4, automatiza o processo mensal de cálculo e compra de Vale Refeição (VR) para uma empresa. A solução consolida múltiplas fontes de dados, aplica regras de negócio complexas e gera um relatório final preciso para o fornecedor, além de disponibilizar um agente de IA para análises interativas dos resultados.

## 📋 Tabela de Conteúdos

- [Funcionalidades](#-funcionalidades)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Começando](#-começando)
  - [Pré-requisitos](#-pré-requisitos)
  - [Instalação e Configuração](#-instalação-e-configuração)
- [Como Executar](#-como-executar)
- [O Papel do Agente de IA](#-o-papel-do-agente-de-ia)
- [Saídas do Projeto](#-saídas-do-projeto)
- [Autor](#-autor)

## ✨ Funcionalidades

* **Consolidação de Dados**: Agrega e unifica dados de 10 planilhas distintas, incluindo informações de funcionários ativos, admissões, desligamentos, férias e afastamentos.
* **Aplicação de Regras de Negócio**: Calcula o valor do benefício aplicando regras específicas, como desconto de dias de férias e elegibilidade baseada na data de desligamento.
* **Mapeamento Inteligente**: Corrige automaticamente inconsistências nos nomes dos sindicatos entre diferentes planilhas para garantir a precisão dos cálculos.
* **Geração de Relatório para Fornecedor**: Cria a planilha final `VR MENSAL 05.2025.xlsx` no layout exato de 10 colunas, pronta para envio ao fornecedor.
* **Análise Interativa com Agente de IA**: Permite que um usuário faça perguntas em linguagem natural sobre os resultados do cálculo, como "Qual o custo total para a empresa?" ou "Quais os 5 sindicatos de maior custo?".

## 🛠️ Tecnologias Utilizadas

* **Python**: Linguagem principal para o desenvolvimento.
* **Pandas**: Para manipulação e análise de dados de alta performance.
* **LangChain & LangChain Experimental**: Framework para desenvolvimento de aplicações com LLMs, utilizado na criação do agente.
* **LangChain-OpenAI**: Biblioteca para integração com modelos de linguagem.
* **Matplotlib**: Para a geração de gráficos e visualizações.
* **Google Colab / Jupyter Notebook**: Ambiente de desenvolvimento interativo.

## 🚀 Começando

Siga estas instruções para configurar e executar o projeto em seu próprio ambiente.

### 📋 Pré-requisitos

* Uma conta Google (para acesso ao Google Drive e Google Colab).
* Uma chave de API de um provedor de LLM compatível (ex: OpenRouter), pois o agente precisa de acesso a um modelo de linguagem.

### ⚙️ Instalação e Configuração

1.  **Clone ou faça o download** deste repositório para a sua máquina local.
2.  **Faça o upload do arquivo `Desafio 4 - Dados.zip`** para uma pasta no seu Google Drive. Por exemplo: `My Drive/Colab Notebooks/`.
3.  **Faça o upload do notebook `Agente_VR_Desafio_4.ipynb`** para o Google Colab.
4.  **Configure a Chave de API**:
    * Dentro do notebook no Colab, clique no ícone de chave (Secrets) no menu à esquerda.
    * Crie uma nova "secret" com o nome `OPENROUTER_API_KEY`.
    * Cole a sua chave de API no campo "Value" e ative a permissão para o notebook acessá-la.

## ▶️ Como Executar

1.  Abra o notebook `Agente_VR_Desafio_4.ipynb` no Google Colab.
2.  Verifique no **Passo 4** se o caminho para o arquivo ZIP (`zip_file_path`) corresponde à estrutura de pastas do seu Google Drive.
3.  Execute todas as células em ordem sequencial, do topo ao fim. O notebook é autoexplicativo e cada passo está devidamente comentado.

## 🤖 O Papel do Agente de IA

O agente de Inteligência Artificial é uma peça fundamental desta solução, atendendo à exigência de uso "efetivo" de agentes no projeto.

* **Onde é usado?**: O agente é implementado no **Passo 9** do notebook, após a conclusão de todos os cálculos e a criação do dataframe final.
* **Como é usado?**: Ele utiliza a biblioteca LangChain para criar uma interface de conversação sobre os dados já processados. Utilizando o prompt customizado (`prompt-para-apoio-analise.txt`), o agente se torna um especialista na folha de pagamento de benefícios. Sua função é permitir que um usuário de negócio (como um analista de RH) realize consultas analíticas complexas em português, sem precisar escrever nenhum código.
* **Por que é efetivo?**: Ele transforma um relatório estático em uma fonte de dados interativa e auditável, agregando uma camada de inteligência e facilit

