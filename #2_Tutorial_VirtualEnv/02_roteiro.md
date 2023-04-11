# <u>Texto #2:</u> Ambientes virtuais: Como iniciar um ambiente virtual para Ciência de Dados

<!-- TOC -->

- [Texto #2: Ambientes virtuais: Como iniciar um ambiente virtual para Ciência de Dados](#texto-2-ambientes-virtuais-como-iniciar-um-ambiente-virtual-para-ciência-dedados)
  - [1. Roteiro](#1-roteiro)
    - [1.1. Mostrar onde está o Python antes do `pyenv`](#11-mostrar-onde-está-o-python-antes-do-pyenv)
    - [1.2. Instalar o `pyenv`](#12-instalar-o-pyenv)
    - [1.3. Preparar e planejar o projeto](#13-preparar-e-planejar-o-projeto)
    - [1.4. Criar um ambiente virtual com uma versão específica do Python](#14-criar-um-ambiente-virtual-com-uma-versão-específica-do-python)
    - [1.5. Ativando e desativando o ambiente virtual](#15-ativando-e-desativando-o-ambiente-virtual)
      - [1.5.1. Ativando o ambiente virtual manualmente](#151-ativando-o-ambiente-virtual-manualmente)
      - [1.5.2. Ativando o ambiente virtual automaticamente usando `pyenv local`](#152-ativando-o-ambiente-virtual-automaticamente-usando-pyenv-local)
  - [2. Instalando bibliotecas](#2-instalando-bibliotecas)

<!-- /TOC -->

## 1. Roteiro

### 1.1. Mostrar onde está o Python antes do `pyenv`
- Mostrar onde o Python e seus pacotes estão instalados

### 1.2. Instalar o `pyenv`
- Iniciar instalando as dependências do `pyenv`
```bash
sudo apt-get install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm gettext libncurses5-dev tk-dev tcl-dev blt-dev libgdbm-dev git python2-dev python3-dev aria2
```

- Instalar, então, o próprio `pyenv`
```bash
curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
```

- Após instalar o `pyenv`, prestar atenção à mensagem que ele retorna para que possamos adicionar os comandos corretos ao arquivo de definição do bash
```bash
sudo echo '# Comandos do pyenv
export PYTHON_BUILD_ARIA2_OPTS="-x 10 -k 1M"
export PATH="~/.pyenv/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
```

- Reiniciar o terminal para que as modificações tenham efeito

Agora podemos verificar se o `pyenv` está funcionando consultando seus comandos e buscando ajuda caso tenhamos dúvidas em algum comando
```bash
pyenv commands

pyenv whence --help
```

---

### 1.3. Preparar e planejar o projeto
- Vou precisar do Python mais recente (*3.11.2*)
- Vou precisar do Jupyter Notebook
- Vou precisar de bibliotecas de exploração numérica de dados (*pandas* e *numpy*)
- Vou precisar de bibliotecas de visualização de dados (*matplotlib* e *seaborn*)
- Vou precisar de bibliotecas de machine learning (*scikit-learn* e *scipy*)
- Conforme formos precisando de outras bibliotecas, podemos instalá-las livremente, desde que estejamos com o ambiente virtual ativado


### 1.4. Criar um ambiente virtual com uma versão específica do Python
```bash
pyenv versions # Primeiro verificamos quais as versões estão disponíveis no computador

pyenv install --list # Para verificarmos se a versão que queremos está lá
# ----------------- ou ---------------------------
pyenv install --list | grep 3.11 # Para verificarmos quais versões da 3.11 estão disponíveis

pyenv install 3.11.2

pyenv versions # Verificamos novamente as versões disponíveis para verificarmos que a 3.11.2 agora está lá
```

Após a instalação terminar, já podemos criar nosso ambiente virtual:
```bash
pyenv virtualenvs # Para, antes de mais nada, verificar quantos e quais ambientes virtuais nós temos

pyenv virtualenv 3.11.2 meu_ambiente #Aqui vou usar a versão 3.11.2 e nomear o novo ambiente virtual de "meu_ambiente"

pyenv virtualenvs # Novamente podemos verificar se nosso ambiente foi efetivamente criado
```

### 1.5. Ativando e desativando o ambiente virtual

- Agora que temos a versão desejada instalada e o ambiente criado podemos ativá-lo e começar a usá-lo. Podemos fazer isto de duas formas:
  - Ativando o ambiente virtual manualmente a cada vez que formos utilizá-lo
  - Ativando o ambiente virtual localmente dentro do diretório do projeto de modo que, sempre que abrirmos este diretório, o ambiente virtual é automaticamente iniciado

#### 1.5.1. Ativando o ambiente virtual manualmente 
Ativar o ambiente virtual de forma manual antes de trabalhar no projeto é muito simples. Basta usarmos o comando abaixo e estamos aptos a trabalhar no ambiente escolhido.
```bash
pyenv activate meu_ambiente # Para ativarmos o ambiente meu _ambiente

pyenv virtualenvs # Para verificarmos se de fato estamos trabalhando com o ambiente que desejamos
# ----------------- ou ---------------------------
pyenv version 
```

Quando estivermos satisfeitos com o trabalho no ambiente virtual, podemos desativá-lo com o comando

```bash
pyenv deactivate
```

#### 1.5.2. Ativando o ambiente virtual automaticamente usando `pyenv local`
Se desejarmos que o ambiente virtual seja ativado automaticamente ao trabalharmos em um determinado diretório bastae que vinculemos localmente o ambiente ao diretório.
```bash
cd ./repos/meu_projeto # Primeiro devemos nos situar no diretório em que desejamos vincular 

pyenv local meu_ambiente # Definindo que a versão local do Python nesse diretório é a do ambiente meu_ambiente. Isto cria uma entrada no arquivo .python-version

echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc # Agora devemos explicitar ao inicializador do bash que ele deve ler a virtualenv assim que entrarmos no diretório
```

Caso queiramos restaurar a versão local do Python no diretório, basta usarmos
```bash
pyenv local system
```

Na imagem abaixo podemos ver a ordem de prioridade que o `pyenv` utiliza para reconhecer as diversas versões do Python em nosso computador. Esta imagem deve ser lida de cima para baixo, já que ele prioriza a versão especificada para o shell (no caminho `$PYENV_VERSION`). Caso não haja especificações para a versão do shell, o `pyenv` "desce" um degrau na pirâmide e busca a versão local especificada (no arquivo `.python-version`). Se nada for encontrado neste local, o `pyenv` desce mais um nível e busca uma versão global do Python para ser usada (no arquivo `~/.pyenv/version`). Por fim, se nenhuma das anteriores estiver especificada, o pyenv descerá até a base da pirâmide e usará a versão do Python do próprio sistema. 

<br>
<p align="center">
<img src="/home/bruno/repos/TheVirtualEnvironmentalist/#2_Tutorial_VirtualEnv/imgs/pyenv-pyramid.png" alt="piramide" >
<figcaption align = "center"><b>Pirâmide que representa a ordem de resolução prioritária do pyenv. Ela deve ser lida de cima baixo, de modo que o pyenv procura primeiro uma especificação de versão do shell, caso não encontre, ele busca uma especificação de versão local. Caso também não encontre, procura especificação da versão globa. E por fim, usa a versão do próprio sistema. Esta ordem de especificações de versões está alocada nos arquivos e na estrutura de diretórios do pyenv. Imagem original de RealPython</b></figcaption>
</p>

---

## 2. Instalando bibliotecas
Enfim podemos ajustar nosso ambiente virtual para satisfazer nossas necessidades. Como havíamos definido no planejamento do projeto, precisaremos instalar algumas bibliotecas, como pandas, numpy, seaborn, matplotlib, scikit-learn e scipy, além do Jupyter Notebook. Para isso basta ativarmos nosso ambiente virtual (de forma manual ou automática) e instalar o que desejarmos com o `pip`.

```bash
cd ~/meu_projeto # Ir até o diretório do projeto

pyenv version # Verificar se de fato estamos usando o ambiente virtual desejado 

pyenv activate meu_ambiente # Caso não esteja no ambiente virtual do projeto

pip install pandas==1.5.0 # Vamos começar pelo pandas, instalando uma versão antiga para comparar com a que já está instalada no ambiente global
```

Podemos verificar se a versão que instalamos é mesmo a desejada e prosseguir com a instalção das demais bibliotecas
```bash
pip list # Verificar os pacotes instalados e suas versões

pip install jupyter notebook seaborn scikit-learn # Podemos nos ater a estes, já que os demais pacotes são dependências destes e serão instalados de qualquer forma 
```