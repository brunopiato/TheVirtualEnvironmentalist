# Roteiro para o vídeo CDS Fame

## Passos para a preparação de um roteiro

### Identifique qual é a sua audiência
- Pessoas interessadas em Ciências de Dados de diferentes níveis

### Entenda a necessidade do seu público
- Compreender como funcinam e como utilizar, de forma organizada, um ambiente virtual

### Pesquise o tema que será abordado
- Meus textos do Medium
  - Texto 01: https://medium.com/thevirtualenvironmentalist/ambientes-virtuais-nas-ci%C3%AAncias-de-dados-dfdd9ac05a19
  - Texto 02: https://medium.com/thevirtualenvironmentalist/2-ambientes-virtuais-como-iniciar-um-ambiente-virtual-para-ci%C3%AAncia-de-dados-f53977cfddb8
  - Texto 03: https://medium.com/thevirtualenvironmentalist/3-ambientes-virtuais-como-se-estrutura-um-ambiente-virtual-694ff2cd56c3
### Defina a duração ideal do vídeo
- A duração do vídeo deve ser de 12 a 15 minutos

### Divida a estrutura do roteiro
- Introdução
  - O que são ambientes virtuais e para quê servem?
- Desenvolvimento
  - Como criar e organizar um ambiente virtual usando o `pyenv`
- Conclusão
  - Mostrar a estrutura de pastas do ambiente virtual recém criado

### Determine as mensagens e emoções que serão transmitidas
- Usar ambientes virtuais para organizar projetos é fundamental

### Adeque a linguagem para o seu público


### Avalie quais ações são esperados do público após assistirem ao vídeo
- Curta, comente e compartilhe e não deixe de implementar os passos que realizamos aqui

### Revise e faça os ajustes necessários no roteiro

---

## O roteiro:
Introdução
- Olá!!! Bem vindo e bem vindo ao canal da Comunidade Data Science. 
- Eu sou Bruno Piato e hoje vou te contar um pouco sobre ambientes virtuais, de onde vieram, para quê servem e como usá-los. 
- Vamos também implementar juntos um ambiente virtual e deixá-lo pronto para trabalhar em nosso projeto.
- Antes de continuarmos, se vc ainda não está incrito no canal, aproveita pra se inscrever e não esquece de deixar seu like no vídeo e fique à vontade para compartilhar este conteúdo com quem vc achar que também vai tirar proveito dele.

Ambientes virtuais
- É muito comum a gente trabalhar em mais de um projeto simultaneamente. 
- Cada projeto tem suas particularidades e pode requerer pacotes ligeiramente distintos. Ainda mais quando pensamos nos fluxos de trabalho das empresas e nos ambientes de produção. 
- Este contexto pode escalonar rapidamente e nem sempre as versões de pacotes e bibliotecas são compatíveis. 
- Imagine, por exemplo, que em um projeto eu uso o `pandas` mais recente, a versão `2.0` neste caso e em outro o `pandas 1.5`. Como faço para ter os dois instalamos na minha máquina? 
- Sem contar que muitas vezes usamos versões diferentes do próprio interpretador do `Python`.
- As coisas podem ficar ainda mais complicadas e bagunçadas se considerarmos que grande parte dos sistemas operacionais usam um interpretador nativo do Python com bibliotecas em versões específicas e modifiá-las pode causar conflitos no próprio sistema operacional.
- Para lidar com este problema foram criados os ambientes virtuais. Eles são como caixas de isolamente para que possamos ter diferentes bibliotecas em versões distintas simultaneamente na mesma máquina sem que uma interfira na outra.

![Ambientes virtuais](https://miro.medium.com/v2/resize:fit:640/format:webp/1*Et8M3SI82Gc6yj1N6VUsVQ.png)


- Existem diversos gerenciadores de ambientes virtuais, como o `venv`, o `virtualenv`, o `conda`, etc. 
- Entretanto há uma ferramenta chamada `pyenv` que consegue gerenciar tanto as versões de bibliotecas quanto as versões do próprio interpretador do Python, deixando em paz o interpretador nativo do sistema operacional.
- Por isso esta é a ferramenta que será utilizada neste vídeo. Ela é ótima para ser usada com sistemas operacionais baseados no Unix, como as diferentes distros do Linux e o MacOS. 
- Para usá-la no Windows é necessário usar a biblioteca `pyenv-win` ou criar os ambientes através do gerenciador `conda`.
- No meu caso estou usando o Pop!_OS, uma distribuição do Linux.

Implementando um ambiente virtual usando o `pyenv`

Instalação

- Primeiro precisamos instalar as dependências e então **instalar o pyenv**. Podemos seguir o passo-a-passo de instalação do repositório do pyenv no GitHub 
```bash
 sudo apt-get install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm gettext libncurses5-dev tk-dev tcl-dev blt-dev libgdbm-dev git python2-dev python3-dev aria2

 curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
 ```

```bash
sudo echo '# Comandos do pyenv
export PYTHON_BUILD_ARIA2_OPTS="-x 10 -k 1M"
export PATH="~/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
```

Exploração dos comandos
```bash
pyenv #Comando

pyenv version #Versão

cat /home/bruno/.pyenv/version #Arquivo version

pyenv versions #Versões disponíveis

pyenv virtualenvs #Ambientes virtuais disponíveis
```

Criando um ambiente virtual novo
```bash
pyenv virtualenv --help #O que deve conter o comando de criação da virtualenv

pyenv install --list #Lista de versões disponíveis

pyenv install 3.11.2 #Versão escolhida

pyenv versions #Versões instaldas

pyenv virtualenv 3.11.2 meu_ambiente #Criando ambiente novo

pyenv versions #Versões disponíveis

pyenv virtualenvs #Ambientes disponíveis

pyenv activate meu_ambiente #Ativando o ambiente

pyenv deactivate meu_ambiente #Desativando o ambiente
```

Atribuindo um ambiente virtual a um diretório
```bash
cd ~ #Indo pro diretório home

mkdir meu_projeto #Novo diretório

cd meu_projeto #Indo pro novo diretório

pyenv version #Verificando a versão ativa

pyenv local meu_ambiente #Determinando o ambiente local

pyenv version #Verificando a versão ativa

pyenv global #Verificando a versão global

pyenv install 2.7.16 #Instalando uma nova versão

pyenv global 2.7.16 #Determinando a versão global

pwd 

pyenv version #Verificando a versão no diretório do projeto

cd .. #Saindo do diretório do projeto

pwd

pyenv version #Verificando a versão usada fora do diretório do projeto

```

















