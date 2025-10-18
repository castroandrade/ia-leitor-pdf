# Chatbot Inteligente para Artigos Científicos (TCC) com IA Generativa

## 🎯 Objetivo

Este projeto, desenvolvido para um desafio da DIO, implementa um sistema de busca inteligente para artigos científicos em formato PDF. O objetivo é auxiliar estudantes e pesquisadores a extrair informações e correlacionar ideias de múltiplos documentos de forma rápida e contextual, utilizando Inteligência Artificial Generativa e busca vetorial.

A solução funciona como um assistente virtual que "lê" os documentos carregados e responde a perguntas com base estritamente no conteúdo deles.

## ✅ Funcionalidades Principais

- **Carregamento de Múltiplos PDFs:** O sistema é capaz de processar diversos arquivos PDF de uma vez, criando uma base de conhecimento unificada.
- **Indexação Vetorial:** Utiliza a técnica de *embeddings* para transformar o conteúdo textual em vetores, permitindo buscas por similaridade semântica.
- **Geração de Respostas com Base em Fontes:** As respostas são geradas por um modelo de linguagem (LLM) e fundamentadas nos trechos mais relevantes dos documentos originais, mitigando o risco de "alucinações" da IA.
- **Interface de Chat Interativa:** Permite que o usuário faça perguntas em linguagem natural e receba respostas contextuais em tempo real.

## 🛠️ Tecnologias Utilizadas

- **Linguagem:** Python
- **Framework de Orquestração:** LangChain
- **Modelo de Embeddings e LLM:** OpenAI (ou outro de sua preferência)
- **Banco de Dados Vetorial:** FAISS (para buscas de similaridade em memória)
- **Manipulação de PDFs:** PyPDF
- **Interface (Opcional, mas recomendado):** Streamlit

## 📂 Estrutura do Repositório

```
/
├── docs/                    # Pasta para armazenar seus artigos em PDF
├── inputs/                  # Contém exemplos de perguntas
├── .gitignore               # Ignora arquivos sensíveis (ex: .env)
├── Chatbot_TCC.ipynb        # Notebook com todo o processo de desenvolvimento
├── README.md                # Este arquivo
├── requirements.txt         # Lista de dependências do projeto
└── .env.example             # Template para as chaves de API
```

## 📈 Como Funciona? O Processo (RAG)

O sistema utiliza a arquitetura **RAG (Retrieval-Augmented Generation)**, que funciona em duas etapas principais:

1.  **Indexação (Ingestão de Dados):**
    - **Carregamento:** Os PDFs da pasta `/docs` são carregados.
    - **Divisão:** O texto de cada documento é dividido em pequenos pedaços (chunks).
    - **Embedding:** Cada chunk é transformado em um vetor numérico por um modelo de embeddings.
    - **Armazenamento:** Esses vetores são armazenados em um banco de dados vetorial (Vector Store), como o FAISS, que permite buscas de alta velocidade.

2.  **Recuperação e Geração (Interação via Chat):**
    - **Pergunta do Usuário:** O usuário envia uma pergunta.
    - **Busca Vetorial:** A pergunta é transformada em um vetor e o sistema busca no Vector Store os chunks de texto mais semanticamente similares à pergunta.
    - **Augmentação do Prompt:** Os chunks recuperados (o "contexto") são inseridos em um prompt junto com a pergunta original.
    - **Geração de Resposta:** O prompt completo é enviado a um modelo de linguagem (LLM), que gera uma resposta coesa e baseada exclusivamente no contexto fornecido.

## 🚀 Como Executar o Projeto

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/seu-usuario/chatbot-tcc-dio.git
    cd chatbot-tcc-dio
    ```

2.  **Crie um ambiente virtual e instale as dependências:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    pip install -r requirements.txt
    ```

3.  **Configure suas chaves de API:**
    - Renomeie o arquivo `.env.example` para `.env`.
    - Abra o arquivo `.env` e insira sua chave da API da OpenAI (ou de outro provedor).

4.  **Adicione seus PDFs:**
    - Coloque os artigos científicos que deseja analisar dentro da pasta `/docs`.

5.  **Execute o Notebook:**
    - Abra o `Chatbot_TCC.ipynb` em um ambiente Jupyter e execute as células sequencialmente.

## 💡 Insights e Aprendizados

- **Poder da Busca Semântica:** A busca vetorial é muito mais poderosa que a busca tradicional por palavras-chave, pois entende o significado e o contexto por trás das palavras.
- **Controle sobre a IA (Grounding):** A técnica RAG é fundamental para criar aplicações de IA confiáveis para nichos específicos, pois "força" o modelo a basear suas respostas em fontes de dados controladas, aumentando a precisão e a confiabilidade.
- **Modularidade do LangChain:** O framework LangChain facilita a conexão de diferentes componentes (carregadores de dados, modelos de texto, vector stores), permitindo a criação de aplicações complexas com código limpo e organizado.

## 🔮 Possibilidades Futuras

- **Deploy da Aplicação:** Criar uma interface web com Streamlit e fazer o deploy na Streamlit Community Cloud ou Hugging Face Spaces.
- **Adicionar Memória:** Implementar um sistema de memória para que o chatbot se lembre de perguntas anteriores na mesma conversa.
- **Citar Fontes:** Aprimorar o sistema para que, junto com a resposta, ele indique exatamente qual trecho e de qual PDF a informação foi extraída.
- **Suporte a Outros Formatos:** Expandir a capacidade para processar arquivos `.docx`, `.txt`, ou até mesmo URLs de páginas web.
