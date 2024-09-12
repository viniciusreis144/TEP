# TEP
Curso de Tópicos Especiais de Programação

# Aula 01
Introdução ao Desenvolvimento de Software com LLMs
Slides sobre LLMs (Modelos de Linguagem de Grande Escala)
Estudo importante sobre como esses modelos funcionam e como integrá-los no desenvolvimento de software.

Ambientes Virtuais no Python
Anotações sobre ambientes virtuais:

Ambientes virtuais = "ilhas" isoladas para gerenciar pacotes Python por projeto.
Cada projeto tem seu próprio ambiente, evitando conflitos de versão entre bibliotecas.
Por que usar?

Isolamento: Evita que um projeto interfira no outro.
Gerenciamento: Mantém controle sobre as versões dos pacotes usados.
Reprodutibilidade: Outros devs podem recriar o ambiente facilmente.
Organização: Evita confusões com várias bibliotecas no sistema global.
Como criar um ambiente virtual local:

No terminal:
python -m venv meu_ambiente

Para ativar:
meu_ambiente\Scripts\activate

Instalar pacotes (lembrar sempre de ativar o ambiente antes):
pip install <pacote>


Dica pessoal: Nomear o ambiente virtual como .venv para facilitar.
VSCode: Ambiente virtual integrado ao editor, facilita bastante. Criar e ativar direto pelo terminal do VSCode ou ajustar as configurações para usar .venv.

Testes práticos com GPTs e Groq
1. Search Tools GPTs: Usar o GPT para fazer buscas inteligentes.
2. Chat com GPT: Interagir diretamente com o GPT para tirar dúvidas ou gerar conteúdo.
3. Imagem com DALLE-3: Criar imagens a partir de descrições textuais.
4. Texto para Áudio: Converter textos em arquivos de áudio rapidamente.
5. Groq:
    Áudio para Texto: Ferramenta que transcreve áudios para texto.
    Chat com Groq: Bate-papo usando IA da plataforma Groq.
