# ChatBots - Projeto de Inteligência Artificial

Este repositório contém implementações de diferentes tipos de chatbots utilizando tecnologias de IA modernas, incluindo ChatterBot, Google Gemini e agentes inteligentes com LangChain.

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Implementações](#implementações)
  - [ChatterBot](#1-chatterbot)
  - [Gemini Chat](#2-gemini-chat)
  - [Agentes IA com LangChain](#3-agentes-ia-com-langchain)
- [Como Usar](#como-usar)
- [Contribuindo](#contribuindo)
- [Licença](#licença)

## 🎯 Sobre o Projeto

Este projeto demonstra diferentes abordagens para criar chatbots inteligentes em Python:

1. **Chatbot Simples** - Usando ChatterBot para conversas básicas em português
2. **Chatbot com Gemini** - Integração com Google Gemini API com tradução automática
3. **Agentes IA Avançados** - Sistema completo de agentes inteligentes com RAG (Retrieval-Augmented Generation)

## 🚀 Tecnologias Utilizadas

- **Python 3.11+**
- **ChatterBot** - Biblioteca para chatbots baseados em regras
- **spaCy** - Processamento de linguagem natural
- **Google Generative AI** - API do Google Gemini
- **LangChain** - Framework para desenvolvimento de aplicações com LLMs
- **FAISS** - Busca vetorial para RAG
- **Deep Translator** - Tradução automática
- **PyMuPDF** - Processamento de documentos PDF

## 📁 Estrutura do Projeto

```
ChatBots/
│
├── chatterbot.py                    # Implementação ChatterBot (script)
├── chatterbot.ipynb                 # Implementação ChatterBot (notebook)
│
├── germini.py                       # Implementação Gemini (script)
├── gemini.ipynb                     # Implementação Gemini (notebook)
│
├── AI_agents_alura.ipynb           # Agentes IA - Aula 1 e 2
├── imersao_agentes_de_IA_alura_com_google_gemini.ipynb  # Agentes IA - Completo
│
├── db.sqlite3                       # Banco de dados do ChatterBot
└── README.md                        # Este arquivo
```

## 📋 Pré-requisitos

- Python 3.11 ou superior
- pip (gerenciador de pacotes Python)
- Conta Google Cloud com API Gemini habilitada (para implementações Gemini)
- Jupyter Notebook (opcional, para executar os notebooks)

## 🔧 Instalação

### 1. Clone o repositório

```bash
git clone https://github.com/Renan-RodriguesDEV/ChatBots.git
cd ChatBots
```

### 2. Crie um ambiente virtual (recomendado)

```bash
python -m venv venv

# No Windows
venv\Scripts\activate

# No Linux/Mac
source venv/bin/activate
```

### 3. Instale as dependências

Para **ChatterBot**:
```bash
pip install ChatterBot spacy
python -m spacy download en_core_web_sm
```

Para **Gemini Chat**:
```bash
pip install google-generativeai deep-translator
```

Para **Agentes IA**:
```bash
pip install langchain langchain-google-genai google-generativeai
pip install langchain_community faiss-cpu langchain-text-splitters pymupdf
pip install langgraph
```

### 4. Configure a API Key do Google Gemini

Crie um arquivo `src/configs/creds_my.py` (para os scripts) ou configure no Google Colab:

```python
API_KEY = "sua-chave-api-aqui"
```

⚠️ **Importante**: Nunca compartilhe sua API Key publicamente!

## 💡 Implementações

### 1. ChatterBot

Um chatbot simples baseado em treinamento com listas de conversas em português.

**Características:**
- Treinamento customizado em português brasileiro
- Conversas informais sobre jogos, tecnologia e preferências
- Aprendizado contínuo durante a conversa
- Armazenamento em banco SQLite

**Arquivo**: `chatterbot.py` ou `chatterbot.ipynb`

**Exemplo de uso**:
```python
from chatterbot import ChatBot
from chatterbot.trainers import ListTrainer

chatBot = ChatBot("RenanChat", tagger_language=ENGSM)
trainer = ListTrainer(chatBot)
trainer.train(dadosdetreino)

# Iniciar conversa
mensagem = input("Mande uma mensagem para o RenanChat:")
resposta = chatBot.get_response(mensagem)
print(resposta)
```

### 2. Gemini Chat

Chatbot integrado com Google Gemini API, com tradução automática entre português e inglês.

**Características:**
- Integração com Gemini 1.5 Pro
- Tradução automática PT ↔ EN
- Histórico de conversação
- Configurações personalizáveis (temperatura, tokens, etc.)

**Arquivo**: `germini.py` ou `gemini.ipynb`

**Exemplo de uso**:
```python
import google.generativeai as genai
from deep_translator import GoogleTranslator

genai.configure(api_key=API_KEY)
model = genai.GenerativeModel(model_name="gemini-1.5-pro")
chat_session = model.start_chat()

# Tradutores
gt_pt = GoogleTranslator('en', 'pt')
gt_en = GoogleTranslator('pt', 'en')

# Conversar
message = input('Start message:')
message_en = gt_en.translate(message)
response = chat_session.send_message(message_en)
response_pt = gt_pt.translate(response.text)
print(response_pt)
```

### 3. Agentes IA com LangChain

Sistema avançado de agentes inteligentes com múltiplas funcionalidades.

**Características:**
- **Aula 1**: Agente simples com saída estruturada usando Pydantic
- **Aula 2**: RAG (Retrieval-Augmented Generation) com documentos PDF
- **Aula 3**: Sistema completo com LangGraph e fluxo de decisão

**Funcionalidades do Sistema Completo:**
- Triagem automática de solicitações
- Resposta automática baseada em documentos
- Abertura de chamados quando necessário
- Busca vetorial com FAISS
- Processamento de documentos PDF
- Fluxo condicional com LangGraph

**Arquivo**: `imersao_agentes_de_IA_alura_com_google_gemini.ipynb`

**Exemplo de fluxo**:
```
Pergunta do Usuário
        ↓
    Triagem
    /  |  \
AUTO  INFO  CHAMADO
RESOLVER
   ↓
  RAG
   ↓
Resposta com Citações
```

## 🎮 Como Usar

### Executar Scripts Python

**ChatterBot**:
```bash
python chatterbot.py
```

**Gemini Chat**:
```bash
python germini.py
```

### Executar Notebooks Jupyter

```bash
jupyter notebook
```

Em seguida, abra o notebook desejado e execute as células.

### Google Colab

Você também pode executar os notebooks diretamente no Google Colab. Os notebooks já incluem badges "Open in Colab" no topo.

## 📚 Exemplos de Conversação

### ChatterBot
```
Você: Iae mano tudo bem
Bot: Tudo numa boa e você como vai
Você: Gosta de python?
Bot: Adoro acho irado
```

### Gemini Chat
```
Você: Explique o que é machine learning
Bot: Machine learning é um subcampo da inteligência artificial...
```

### Agente IA
```
Pergunta: Posso reembolsar a internet?
Decisão: AUTO_RESOLVER
Resposta: Sim, a internet para home office é reembolsável 
via subsídio mensal de até R$ 100, conforme política de Home Office.
Citações: [Documento relevante com página]
```

## 🤝 Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para:

1. Fazer um Fork do projeto
2. Criar uma branch para sua feature (`git checkout -b feature/NovaFeature`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/NovaFeature`)
5. Abrir um Pull Request

## 📝 Notas Importantes

- **API Keys**: Mantenha suas chaves de API seguras e nunca as compartilhe publicamente
- **Modelos de linguagem**: Os modelos do spaCy e do Gemini requerem conexão com internet
- **Banco de dados**: O ChatterBot cria automaticamente um arquivo `db.sqlite3`
- **Custos**: Verifique os limites gratuitos da API do Google Gemini

## 🔍 Troubleshooting

### Erro com spaCy
```bash
python -m spacy download en_core_web_sm
```

### Erro de importação do ChatterBot
Certifique-se de que está usando Python 3.11 ou inferior, pois versões mais recentes podem ter incompatibilidades.

### Erro de API Key
Verifique se sua API Key está corretamente configurada e se a API do Gemini está habilitada no Google Cloud.

## 📖 Recursos Adicionais

- [Documentação ChatterBot](https://chatterbot.readthedocs.io/)
- [Documentação Google Gemini](https://ai.google.dev/docs)
- [Documentação LangChain](https://python.langchain.com/)
- [Curso Alura - Imersão IA](https://www.alura.com.br/)

## 👨‍💻 Autor

**Renan Rodrigues**

- GitHub: [@Renan-RodriguesDEV](https://github.com/Renan-RodriguesDEV)

## 📄 Licença

Este projeto é de código aberto e está disponível para fins educacionais.

---

⭐ Se este projeto foi útil para você, considere dar uma estrela no repositório!

🐛 Encontrou um bug? Abra uma issue!

💡 Tem uma sugestão? Pull requests são bem-vindos!
