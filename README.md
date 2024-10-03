# TEP
Curso de Tópicos Especiais de Programação

# Aula 01
# Introdução ao Desenvolvimento de Software com LLMs
Slides sobre **LLMs** (Modelos de Linguagem de Grande Escala). Estudo importante sobre como esses modelos funcionam e como integrá-los no desenvolvimento de software.

## Ambientes Virtuais no Python

### Anotações sobre Ambientes Virtuais:
- Ambientes virtuais = "ilhas" isoladas para gerenciar pacotes Python por projeto.
- Cada projeto tem seu próprio ambiente, evitando conflitos de versão entre bibliotecas.

### Por que usar?
- **Isolamento**: Evita que um projeto interfira no outro.
- **Gerenciamento**: Mantém controle sobre as versões dos pacotes usados.
- **Reprodutibilidade**: Outros desenvolvedores podem recriar o ambiente facilmente.
- **Organização**: Evita confusões com várias bibliotecas no sistema global.

### Como criar um ambiente virtual local:
No terminal:
bash
python -m venv meu_ambiente

Para ativar:
bash
meu_ambiente\Scripts\activate

Instalar pacotes (lembre-se de ativar o ambiente antes):
bash
pip install <pacote>

Dica pessoal: Nomear o ambiente virtual como .venv para facilitar.

VSCode:
Ambiente virtual integrado ao editor, facilitando bastante. Criar e ativar diretamente pelo terminal do VSCode ou ajustar as configurações para usar .venv.

Testes Práticos com GPTs e Groq
Search Tools GPTs: Usar o GPT para fazer buscas inteligentes.
Chat com GPT: Interagir diretamente com o GPT para tirar dúvidas ou gerar conteúdo.
Imagem com DALLE-3: Criar imagens a partir de descrições textuais.
Texto para Áudio: Converter textos em arquivos de áudio rapidamente.
Groq:
Áudio para Texto: Ferramenta que transcreve áudios para texto.
Chat com Groq: Bate-papo usando IA da plataforma Groq.


# Aula 03

## Finalização de Testes

- Ferramentas: Exemplos de **Search Tools** e **GPTs**
- VPS, Docker, Domínio e DNS (Cloudflare)
  1. VPS, domínios (Registrar domínio)
  2. Criar conta na Cloudflare e registrar domínio

---

## Docker

Docker é uma plataforma open source que empacota uma aplicação dentro de um container, permitindo rodá-la em qualquer máquina com Docker instalado.

### Benefícios do uso do Docker no Windows (com WSL 2)
- Facilita a configuração de ambientes Unix no Windows.
- Integra-se bem com o WSL 2, sem a necessidade de licença PRO do Windows.

### Modos de usar Docker no Windows
1. **Docker Desktop com WSL2**
   - Integração com WSL 2, permitindo rodar Docker dentro do Linux.
   - Visual para administrar o Docker e rodar clusters Kubernetes localmente.
   
   **Desvantagens**: Alto consumo de memória, possível necessidade de reinicializações.

2. **Docker Engine diretamente no WSL2**
   - Mais leve e roda de forma nativa no ambiente Linux.
   - **Desvantagens**: Precisa ser instalado em cada instância do WSL 2 separadamente.

---

## Instalar Docker no WSL 2

1. Atualize o WSL para a versão mais recente:
```shell
wsl --update
```

2. Defina a versão 2 como padrão:
```shell
wsl --set-default-version 2
```

3. Instale o Ubuntu:
```shell
wsl --install
```

4. Instale Docker no Ubuntu via `apt`:
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

5. Verifique a instalação:
```bash
sudo docker run hello-world
```

---

## Containerizando Aplicação Node.js

1. Clone o repositório de exemplo:
```bash
git clone https://github.com/docker/docker-nodejs-sample
```

2. Crie um `Dockerfile` para a aplicação:
```bash
FROM node:14
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "src/index.js"]
```

3. Construa e execute a imagem Docker:
```bash
docker build -t meu-app-node .
docker run -p 3000:3000 meu-app
```

---

## Docker Compose

### Arquivo `docker-compose.yml`
```d
version: '3'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
  db:
    image: mysql:8
    ports:
      - "3306:3306"
    environment:
      - MYSQL_ROOT_PASSWORD=mysecretpassword
      - MYSQL_DATABASE=mydatabase
      - MYSQL_USER=myuser
      - MYSQL_PASSWORD=mypassword
```

---

# Aula 04

# Engenharia de Prompt

## O que é Engenharia de Prompt
A Engenharia de Prompt envolve a criação e otimização de instruções textuais, os chamados prompts, para orientar modelos de linguagem (LLMs). O foco é garantir que esses modelos compreendam e respondam de forma precisa às solicitações dos usuários.

## Configurações dos Modelos de Linguagem
- **Temperatura**: quanto menor, mais determinística é a resposta.
- **Tokens**: representa unidades de processamento de texto.
- **TopP**: controla o grau de precisão nas respostas.

## Tipos de Prompts
### Zero-shot Prompting
Solicita respostas sem fornecer exemplos prévios, como ao pedir explicações diretas: 
```d
Explique os antibióticos.
```

### Few-shot Prompting
Inclui exemplos para guiar as respostas, facilitando tarefas como classificar sentimentos em frases.

## Elementos de um Prompt
- **Instrução**: o que o modelo deve fazer.
- **Contexto**: informações complementares.
- **Entrada**: a pergunta ou informação dada ao modelo.
- **Indicador de Saída**: formato esperado da resposta.

## Dicas para Criar Prompts
1. **Seja simples e específico**: Instruções claras e diretas geram melhores resultados.
2. **Seja detalhado**: Quanto mais informações fornecidas, melhor será a resposta do modelo.
3. **Diga o que fazer**: Focar nas ações esperadas evita resultados imprecisos.

## Exemplos de Aplicações
### Resumo de Texto
Criação de prompts para resumir um conteúdo:
```d
Explique o conceito de antibióticos.
```

### Classificação de Texto
Criação de exemplos para classificar o sentimento de uma frase:
```json
Classifique o texto em neutro, negativo ou positivo.
Texto: Acho que a comida estava ok.
Sentimento:
```

### Geração de Código
Prompts para gerar código de forma eficiente:
```json
/*
Pergunte ao usuário seu nome e diga "Olá".
*/
```

## Técnicas Avançadas
### Zero-shot & Few-shot Prompting
Zero-shot refere-se à habilidade de o modelo lidar com solicitações sem exemplos prévios, enquanto Few-shot utiliza alguns exemplos para guiar a resposta.

### Chain-of-Thought Prompting
Técnica para guiar o modelo a pensar em etapas ao resolver uma tarefa.

## Exemplos de Prompts com Cadeia de Pensamento
```json
P: Um paciente chega com sintomas de febre. O médico realiza exames e diagnostica pneumonia. Explique os passos seguidos.
R: O médico fez o exame físico, solicitou exames de sangue, analisou os resultados e diagnosticou pneumonia.
```

## Outras Técnicas
- **Self-consistency**: Obtém múltiplas respostas e escolhe a mais comum.
- **Chain-of-Verification**: Verifica a veracidade das respostas iniciais geradas pelo modelo.
- **Geração com Recuperação Aprimorada (RAG)**: Usa recuperação de informações externas para melhorar as respostas.
- **React - Razão e Ação**: Estrutura que combina raciocínio e ação intercaladamente.

---

# Aula 5

## Agentes de IA com CrewAI e Llama3 usando a API Groq

Nesta aula, exploramos como criar agentes de IA utilizando a biblioteca CrewAI, o modelo Llama3 e a API Groq em Python. A ideia é configurar e executar agentes de IA de forma prática.

### Requisitos

- Python 3.8 ou superior
- Biblioteca CrewAI
- Acesso à API Groq para o modelo Llama3
- Pip para gerenciar pacotes Python

### Instalação

1. Clone o repositório:

   ```bash
   git clone https://github.com/viniciusds2020/ai_crewai_starter_template.git
   cd ai_crewai_starter_template
   ```

2. Crie um ambiente virtual:

   ```bash
   python -m venv venv
   source venv/bin/activate  # No Windows, use `venv\Scriptsctivate`
   ```

3. Instale as dependências:

   ```bash
   pip install -r requirements.txt
   ```

### Configuração

1. Obtenha uma chave de API da Groq e adicione no arquivo `.env`:
   ```bash
   GROQ_API_KEY=your_api_key_here
   ```

2. Verifique a configuração com o código a seguir:

   ```python
   import os
   from dotenv import load_dotenv
   load_dotenv()

   groq_api_key = os.getenv('GROQ_API_KEY')
   if groq_api_key is None:
       print("A chave da API não foi carregada corretamente.")
   else:
       print("Chave da API carregada:", groq_api_key)
   ```

### Uso

Execute o agente de IA com o comando:
```bash
python main.py
```

### Estrutura do Projeto

```
.
├── README.md
├── requirements.txt
├── main.py
└── .env
```

- `README.md`: Documentação.
- `requirements.txt`: Dependências do Python.
- `main.py`: Script principal para executar o agente.
- `.env`: Chave de API da Groq.

### Arquivo **agents.py**

Código para criar um sistema multi-agente com o modelo Llama3:

```python
from crewai_tools import tool
from crewai import Agent, Task, Crew
from langchain_groq import ChatGroq
from langchain_community.tools import DuckDuckGoSearchRun

# Modelo LLM - Llama3 
llm = ChatGroq(temperature=0.7, groq_api_key='sua-chave-api-groq', model_name='llama-3.1-8b-instant')

# Ferramentas - Busca na internet com DuckDuckGo
@tool('DuckDuckGoSearchRun')
def search_tool(search_query: str):
  return DuckDuckGoSearchRun().run(search_query)

# Tópico de pesquisa
topic = "Apple and AI in finance"

# Agentes
researcher = Agent(
    role = "Senior Researcher",
    goal = f"Explore trending technologies in {topic}.",
    backstory = "You are an innovative researcher.",
    tools = [search_tool],
    llm = llm,
)

writer = Agent(
    role = "Top Writer",
    goal = f"Create engaging content about {topic}.",
    backstory = "You are an expert blogger.",
    tools = [search_tool],
    llm = llm,
)

# Tarefas
research_task = Task(
    description = f"Investigate the latest AI trends in {topic}.",
    tools = [search_tool],
    agent = researcher,
)

write_task = Task(
    description = f"Write an engaging article on {topic}.",
    tools = [search_tool],
    agent = writer,
    output_file = "my-blog.md"
)

# Orquestrador
crew = Crew(
    agents=[researcher, writer],
    tasks=[research_task, write_task]
)

result = crew.kickoff(inputs={"topic": topic})
```

### Adaptando para uma nova tarefa

Podemos adaptar o projeto acima para pesquisar e redigir uma notícia sobre queimadas em Mato Grosso. O arquivo `main.py` pode ser copiado e adaptado para `agente.py`. Lembre-se de alterar o idioma para Português do Brasil e modificar os prompts de acordo.

### Instalação do Langflow

Instale o Langflow localmente com o comando:
```bash
python -m pip install langflow -U
```

Execute o Langflow com:
```bash
python -m langflow run
```

Acesse a instância local em `http://127.0.0.1:7860`.

### Exemplos de Fluxos no Langflow

- TEP - Chat com Memória
- TEP - CrewAI
- TEP - PDF RAG

---

