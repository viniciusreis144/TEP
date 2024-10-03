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

# Aula 02

## Finalizar os Testes Práticos:
- **Tools** como **Search Tools** e **GPTs**
- VPS, Docker, Domínio e DNS (Cloudflare)

### VPS e Domínios:
1. VPS e domínios (Registrar domínio)
2. Criar conta na Cloudflare e registrar domínio

Credenciais:
- username: tep
- senha: tep123

## Docker

Docker é uma plataforma open source que empacota uma aplicação dentro de um container, permitindo que ela rode em qualquer máquina que tenha Docker instalado.

### Por que usar WSL 2 + Docker para desenvolvimento?

Montar ambientes de desenvolvimento no Windows pode ser complexo, e o desempenho pode ser insatisfatório. O Docker simplifica essa configuração, proporcionando um ambiente Unix eficiente e unificado.

### Modos de Usar Docker no Windows:

#### Docker Desktop com WSL2:
- Roda em cima da **Virtual Machine Platform** e se integra ao WSL2.
- Não requer licença PRO do Windows 10/11.
- Vantagens: ferramenta visual, extensões, fácil cluster Kubernetes.
- Desvantagens: consome mais memória e recursos.

#### Docker Engine (Nativo) no WSL2:
- Docker puro no ambiente Linux.
- Vantagens: consome menos memória.
- Desvantagens: instalação necessária para cada instância do WSL 2.

### Instalação Docker no WSL2:

1. Atualizar o WSL:
   ```bash
   wsl --update

2. Definir a versão 2 do WSL como padrão:
wsl --set-default-version 2

3. Instalar Ubuntu:
wsl --install

4. Configurar limites de recursos no arquivo .wslconfig:
[wsl2]
memory=8GB
processors=4

### Instalando Docker no Ubuntu:

1. Adicionar repositório do Docker:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
echo "deb [arch=$(dpkg --print-architecture)] https://download.docker.com/linux/ubuntu stable" | sudo tee /etc/apt/sources.list.d/docker.list
sudo apt-get update

2. Instalar pacotes do Docker:
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

3. Verificar instalação:
sudo docker run hello-world

### Como Containerizar uma Aplicação Node.js
Pré-requisitos:
Docker Desktop e Git instalados.

Passo 1: Obtenha a aplicação de exemplo
git clone https://github.com/docker/docker-nodejs-sample
apt install nodejs
apt install npm

Passo 2: Teste a aplicação localmente:
npm install
node src/index.js

Passo 3: Containerização com Docker
Crie o arquivo Dockerfile:
FROM node:14
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "src/index.js"]

Crie o arquivo .dockerignore:
node_modules
npm-debug.log
Dockerfile
.dockerignore

Construa a imagem Docker:
docker build -t meu-app-node .

Execute o container:
docker run -p 3000:3000 meu-app

Usando Docker Compose:
docker compose version
version: '3'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/usr/src/app
    environment:
      - NODE_ENV=production

Execute o Docker Compose:
docker compose up --build
   
