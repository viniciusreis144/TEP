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


# Aula 2

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

# Aula 03

# Engenharia de Prompt

## O que é Engenharia de Prompt
Engenharia de Prompt é a área responsável pela criação e otimização de instruções textuais (prompts) para maximizar a eficiência e precisão dos modelos de linguagem (LLMs). Ela inclui formulação, testes e refinamento contínuo dos prompts, sempre prezando pela clareza, neutralidade e imparcialidade.

## Configurações dos Modelos de Linguagem
- **Temperatura**: controla o nível de aleatoriedade nas respostas (quanto menor, mais determinística).
- **Tokens**: representa o número de caracteres processados.
- **TopP**: deve ser mantido baixo para obter respostas mais exatas.

## Tipos de Prompts
### Zero-shot Prompting
Solicita-se uma resposta sem exemplos prévios, como no prompt direto "Explique os antibióticos".

### Few-shot Prompting
Inclui exemplos para guiar a resposta do modelo. Por exemplo, listar sentenças com diferentes classificações de sentimento.

## Elementos de um Prompt
- **Instrução**: o que o modelo deve fazer.
- **Contexto**: informações adicionais.
- **Entrada**: a pergunta ou dado fornecido.
- **Indicador de saída**: o formato esperado da resposta.

## Dicas para Projetar Prompts
1. **Comece simples**: a especificidade e concisão tendem a gerar melhores resultados.
2. **Seja específico**: quanto mais detalhado o prompt, melhor a resposta.
3. **Foque no que fazer**: evite dizer ao modelo o que não fazer.

## Principais Técnicas
- **Zero-shot prompting**: o modelo responde sem exemplos prévios.
- **Few-shot prompting**: inclui exemplos para guiar o modelo.
- **Chain-of-Thought prompting**: exemplifica o passo a passo para que o modelo raciocine.
- **Self-consistency**: usa múltiplas respostas e escolhe a mais frequente.

## Aplicações Avançadas
- **Geração de código**: LLMs podem gerar código em linguagens específicas sem muitos detalhes.
- **Classificação de texto**: os prompts podem ser ajustados para rótulos específicos (neutro, positivo, negativo).
- **Conversação**: LLMs podem ser configurados para dar respostas técnicas ou mais acessíveis, conforme as necessidades do público.

