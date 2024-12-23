
<!-- README.md é gerado a partir deste README.Rmd. Por favor, edite  e renderize este arquivo -->

# Tutorial de Uso do Git/Github no Virtual Studio Code

<!-- badges: start -->
<!-- badges: end -->

Este tutorial de uso do Git/GitHub no Visual Studio Code (VS-Code) tem
como objetivo fornecer orientações práticas para usuários iniciantes e
intermediários sobre como usar o Git e o GitHub diretamente na interface
do VS Code e na página do GitHub a fim de realizar controle de versão de
códigos de projetos de programação. Utilizaremos principalmente o
terminal do Git Bash no VS-Code.

# 1. Instruções Inicias para uso do Git/Github

1.  Crie uma conta gratuita no GitHub em: <https://github.com/>

2.  Baixe e instale o Git a partir do link:
    <https://git-scm.com/downloads>

3.  Ao fim da instalação do Git, abra e feche o Git Bash.

4.  Faça o teste para verificar se o Git foi instalado corretamente.
    Digite em um terminal:

    ``` bash
    git --version
    ```

    Se tudo estiver funcionando, deve aparecer a versão do Git instalada
    no seu sistema operacional.

## 1.1 Configuração Básica do Git/Github

1.  Abra o terminal no VS Code e configure o nome e e-mail do Github
    para seus commits:

    ``` bash
    git config --global user.name "Seu Nome"
    ```

    ``` bash
    git config --global user.email "seuemail@example.com"
    ```

## 1.2 Configurando a Comunicação com o GitHub via Chave SSH

Para configurar a comunicação segura entre seu repositório local e o
GitHub, você deve gerar e adicionar uma chave SSH:

1.  **Gerar uma Chave SSH** (caso ainda não tenha uma):

    Abra o Git Bash e digite o seguinte comando para gerar uma chave
    SSH:

    ``` bash
    ssh-keygen -t ed25519 -C "seu-email@example.com"
    ```

    - Pressione `Enter` para salvar a chave no local padrão
      (`~/.ssh/id_ed25519`).

    - Defina uma senha para proteger a chave, se desejar.

2.  **Adicionar a Chave SSH ao SSH Agent**:

    Primeiro, inicie o agente SSH:

    ``` bash
    eval "$(ssh-agent -s)"
    ```

    Depois, adicione a chave:

    ``` bash
    ssh-add ~/.ssh/id_ed25519
    ```

3.  **Copiar a Chave SSH a ser adicionada no GitHub**:

    Para copiar a chave pública (que deve ser adicionada ao GitHub):

    ``` bash
    cat ~/.ssh/id_ed25519.pub | clip  # Sua chave é copiada para o clipboard
    ```

4.  **Adicionar a chave SSH ao GitHub**:

    - Vá até as configurações da sua conta no GitHub ([Configurações SSH
      no GitHub](https://github.com/settings/keys)).

    - Clique em **New SSH key**.

    - Cole a chave copiada no campo e dê um nome para identificá-la,
      como “Meu notebook” ou “Desktop pessoal”.

    - Salve a chave.

5.  **Testar a conexão com o GitHub**:

    ``` bash
    ssh -T git@github.com
    ```

    Se configurado corretamente, você verá uma mensagem de boas-vindas
    do GitHub

6.  Caso seu sistema não suporte ed25519, use o **algoritmo rsa**:

    ``` bash
    eval "$(ssh-agent -s)"
    ```

    ``` bash
    ssh-keygen -t rsa -b 4096 -C "seu-email@example.com"
    ```

    ``` bash
    cat ~/.ssh/id_rsa.pub
    ```

    - O conteúdo da chave pública começará com `ssh-rsa` e será uma
      linha longa de texto. Copie todo o conteúdo.

    - Repita as **etapas 4 e 5** acima para finalizar a configuração por
      esse outro algoritmo.

# 2. Como criar repositório

Vamos criar nosso primeiro repositório para uso pessoal e, também,
verificar se as conexões entre o VS-Code e Github via Git estão
funcionando corretamente.

## 2.1 Criando repositório primeiro no Github

A maneira mais eficiente de criar um novo repositório é diretamente pelo
site do GitHub, pois isso garante que todas as configurações sejam
corretamente definidas desde o início.

1.  Acesse sua conta no GitHub, acesse a guia Repositories e clique no
    botão verde **`New`** no canto superior direito da página para criar
    um novo repositório.

    <img src="images/clipboard-2992832090.png" width="605" />

2.  Defina o nome do repositório, adicione uma descrição (opcional), e
    escolha se deseja que o repositório seja público ou privado.

3.  Marque a opção **“Add a README file”** para inicializar o
    repositório com um arquivo `README.md`, que você pode editar
    posteriormente.

4.  Preencha as informações conforme figura abaixo e clique no botão
    **`Create repository`** para finalizar a criação.

    <img src="images/criando-repo-github.png" width="631" />

### 2.1.1 Clonando o Repositório no Seu Computador

Depois de criar o repositório no GitHub, o próximo passo é clonar o
repositório para sua máquina local, criando uma cópia que você poderá
modificar posteriormente no VS-Code. Além disso, esta etapa verifica se
a comunicação via Git está funcionando.

1.  No GitHub, acesse a página do repositório recém-criado e clique no
    botão verde **`<>Code`**, conforme figura abaixo. Em seguida, copie
    a URL fornecida para clonar o repositório (por exemplo, algo como
    [`https://github.com/seu-usuario/seu-repositorio.git`](https://github.com/seu-usuario/seu-repositorio.git)).

    <img src="images/url_repos.png" width="375" />

2.  No Git Bash, navegue até o diretório onde deseja clonar seus
    repositórios e digite o seguinte comando:

    ``` bash
    git clone https://github.com/seu-usuario/seu-repositorio.git
    ```

> Ao executar este comando, será criada uma cópia local do repositório
> em seu computador, permitindo que você faça edições e atualizações
> quando necessário. Durante o processo de clonagem, o Git
> automaticamente configura uma conexão remota chamada `origin`, que
> aponta para a URL do repositório original em sua conta. Desde que você
> seja o proprietário do repositório, esta configuração automática
> elimina a necessidade de executar manualmente o comando
> `git remote add` para conectá-lo remotamente ao respositório original
> no Github. Veja na seção 3 como clonar repositórios de terceiros.

3.  Abra o VS-Code a partir do seu terminal (Pode ser o Git Bash),
    estando dentro da pasta do projeto clonado:

    ``` bash
    cd seu-repositorio/
    code .
    ```

### 2.1.2 Implementando alterações em seu projeto

Agora que o repositório foi colando no seu computador, você pode
realizar pequenas alterações para testar o controle de versão com Git e
GitHub. Estes procedimentos são aplicáveis quando apenas você interage
com o seu próprio repositório.

#### Crie pastas e arquivos:

No VS Code, crie uma nova pasta e adicione um novo arquivo dentro dessa
pasta (por exemplo, uma pasta chamada `teste` e um arquivo chamado
`teste.py`).

#### Etapas com Git no Terminal do VS Code:

1.  **Adicionar as alterações ao staging area:**

    ``` bash
    git add .
    ```

2.  Criar um commit com uma mensagem explicativa:

    ``` bash
    git commit -m "Criação de pasta e arquivo de teste"
    ```

3.  Enviar as alterações para o repositório remoto (GitHub):

    ``` bash
    git push origin main
    ```

    Estas instruções cobrem o fluxo básico para adicionar, comitar e
    enviar alterações iniciais para o GitHub usando o Git no terminal do
    VS Code.

### 2.1.3 Alterando o arquivo `README.md` via GitHub

1.  **Acesse seu repositório no GitHub**: Abra o navegador e vá para a
    página do seu repositório no GitHub.

2.  **Edite o arquivo `README.md`**: Dentro do repositório, clique no
    arquivo `README.md` para abri-lo e selecione a opção **Edit** (ícone
    de lápis) para editar o conteúdo do arquivo diretamente na interface
    do GitHub.

3.  **Faça uma alteração simples**: Realize uma modificação no arquivo,
    como adicionar uma linha de texto para testes, por exemplo:
    `"Alteração de teste realizada no GitHub"`.

4.  **Salve a alteração**: Após realizar a modificação, role para baixo
    e clique em **Commit changes**. Você pode adicionar uma mensagem de
    commit para descrever a alteração (ex.:
    `"Teste de edição via GitHub"`). Em seguida, clique em **Commit
    changes** para salvar a atualização.

5.  **Baixe as alterações para o VS Code**: Agora que a alteração foi
    realizada no GitHub, é necessário atualizar o repositório local no
    VS Code para sincronizar com a versão online.

    - No VS Code, abra o terminal e execute o comando:

      ``` bash
      git pull origin main
      ```

    - Esse comando busca as últimas alterações da branch `main` do
      GitHub e as aplica no repositório local, garantindo que o
      `README.md` atualizado seja baixado.

6.  **Confirme a atualização local**: Após o comando `git pull`,
    verifique se as alterações no `README.md` foram aplicadas
    corretamente no VS Code. Abra o arquivo `README.md` no VS Code e
    confira se a nova linha adicionada aparece.

### 2.1.4 **Excluindo Pastas e Arquivos do Versionamento usando o `.gitignore`**

Nem todos os arquivos e pastas precisam ser compartilhados no
repositório. Para evitar que certos arquivos sejam versionados, você
pode listá-los no arquivo `.gitignore`, garantindo que apenas os
arquivos relevantes sejam rastreados pelo Git.

1.  **Abra ou crie o arquivo `.gitignore`**: No VS-Code, navegue até a
    raiz do projeto e verifique se o arquivo `.gitignore` existe. Caso
    contrário, crie um novo arquivo com esse nome (`.gitignore`) na
    raiz.

2.  **Adicione os arquivos e pastas a serem ignorados**: No arquivo
    `.gitignore`, liste os padrões de nomes de arquivos e pastas que
    você deseja excluir do versionamento. Por exemplo:

    ``` bash
    # Ignorar arquivos temporários do R
    *.Rhistory
    *.Rdata

    # Ignorar diretórios específicos
    /data
    /output
    ```

    Cada linha representa um padrão a ser ignorado pelo Git. Prefixe com
    `/` para excluir um diretório inteiro.

3.  **Salve e faça um commit das alterações**: Salve o arquivo
    `.gitignore` e, em seguida, faça o commit e o push das alterações
    para o GitHub:

    ``` bash
    git add .gitignore
    git commit -m "Adiciona configurações de arquivos e pastas a serem ignorados"
    git push origin main
    ```

4.  **Verifique se o `.gitignore` está funcionando**: Para garantir que
    os arquivos listados estejam de fato sendo ignorados, tente
    adicionar algum arquivo incluído no `.gitignore` e verifique se ele
    não aparece como uma mudança rastreável. Isso confirma que o Git
    está seguindo as regras configuradas no `.gitignore`.

## 2.2 Criando o Repositório Localmente e Vinculando ao GitHub

Embora seja mais eficiente criar o repositório diretamente no GitHub e
depois cloná-lo para o computador, também é possível iniciar um
repositório localmente e vinculá-lo ao GitHub. Esse fluxo cria o projeto
no caminho especificado em seu computador, configura o Git local e,
posteriormente, sincroniza o projeto com o GitHub.

#### Passo a Passo:

1.  **Crie uma pasta para o projeto**: No local desejado em seu
    computador, crie uma pasta para o projeto ou navegue até a pasta já
    existente. Você pode também criar a pasta do projeto no computador e
    abrir o VS-Code nesta pasta.

    ``` bash
    mkdir nome_do_projeto
    cd nome_do_projeto
    code .  # Abre o VS-Code na pasta do repo
    ```

2.  **Inicie o repositório Git local**: Dentro da pasta do projeto, crie
    alguns arquivos com o VS-Code e depois inicialize um novo
    repositório Git.

    ``` bash
    git init
    ```

3.  **Adicione arquivos e faça um commit inicial**: Adicione os arquivos
    do projeto ao Git e crie o primeiro commit. O comando `commit` cria
    uma nova versão do projeto.

    ``` bash
    git add .
    ```

    ``` bash
    git commit -m "Commit inicial"
    ```

    ``` bash
    git log  # Verificar histórico dos commits feitos
    ```

    ``` bash
    git log --all 
    ```

    O comando `git log --all` é usado para mostrar todos os commits que
    temos, quando fazemos o comando `git checkout hash-do-commit`.

4.  **Crie um repositório vazio no GitHub**: Acesse o GitHub, vá para a
    aba de criação de repositórios e crie um novo repositório vazio com
    o mesmo nome do projeto. **Não adicione nenhum arquivo ao
    repositório no GitHub** (como README.md ou .gitignore), pois o
    repositório deve estar vazio para evitar conflitos.

5.  **Vincule o repositório local ao GitHub**: No terminal, adicione o
    repositório GitHub como um repositório remoto, substituindo
    `seu-usuario` e `nome_do_repositorio` pelos nomes correspondentes.

    ``` bash
    git remote add origin https://github.com/seu-usuario/nome_repositorio.git
    ```

    ``` bash
    git branch -M main  # Renomeia master para main
    ```

6.  **Envie o commit inicial para o GitHub**: Envie o conteúdo do
    repositório local para o GitHub.

    ``` bash
    git push -u origin main
    ```

    O parâmetro `-u` configura a branch `main` local para acompanhar
    automaticamente a branch `main` do GitHub, facilitando futuros
    comandos `git push`.

    Agora, seu repositório está vinculado ao GitHub e sincronizado. A
    partir daqui, você pode continuar fazendo commits e enviando as
    alterações para o repositório remoto.

## 2.3 Configurando Git e GitHub para um Projeto Existente no Computador

Se você já possui um projeto no seu computador e deseja vinculá-lo ao
Git e ao GitHub, pode fazer isso sem precisar criar um novo projeto do
zero. Siga os passos abaixo para configurar o controle de versão e
sincronizar o projeto com o GitHub.

1.  **Abra o projeto no VS Code**: Navegue até o diretório do seu
    projeto e abra-o no VS Code. Você pode usar o comando abaixo no
    terminal para abrir o VS Code diretamente na pasta do projeto:

    ``` bash
    code .
    ```

2.  **Inicialize o Git no projeto**: No terminal do VS Code, inicialize
    o repositório Git no diretório do projeto para começar a rastrear as
    alterações.

    ``` bash
    git init
    ```

3.  **Adicione os arquivos ao controle de versão**: Adicione todos os
    arquivos do projeto ao Git para prepará-los para o commit.

    ``` bash
    git add .
    ```

4.  **Faça o commit inicial**: Crie o commit inicial com uma mensagem
    que descreva a adição do projeto ao Git.

    ``` bash
    git commit -m "Commit inicial do projeto existente"
    ```

5.  **Crie um repositório no GitHub**: Acesse o GitHub e crie um
    repositório vazio com o mesmo nome do projeto. **Não adicione nenhum
    arquivo ao repositório no GitHub**, pois ele deve estar vazio para
    evitar conflitos com o projeto local.

6.  **Conecte o repositório local ao GitHub**: No terminal do VS Code,
    adicione o repositório do GitHub como um remoto chamado `origin`.
    Substitua `seu-usuario` e `nome_do_repositorio` pelos valores
    corretos.

    ``` bash
    git remote add origin https://github.com/seu-usuario/nome_repositorio.git
    ```

7.  **Envie o projeto para o GitHub**: Envie o commit inicial do
    repositório local para o GitHub.

    ``` bash
    git push -u origin main
    ```

    O parâmetro `-u` estabelece um vínculo entre a branch `main` local e
    a branch `main` no GitHub, facilitando futuros comandos de
    `git push`.

Esses passos conectam seu projeto local ao Git e sincronizam-no com o
GitHub, criando um repositório remoto pareado com o repositório local. A
partir de agora, você pode continuar a usar o Git para controlar as
versões e o GitHub para fazer backup e colaborar no projeto.

------------------------------------------------------------------------

# 3. Clonando e Bifurcando um Repositório (Fork)

Ao colaborar em projetos no GitHub e em equipe, você pode precisar
clonar ou bifurcar (fazer um fork) um repositório. Bifurcar cria uma
cópia do repositório em sua própria conta GitHub, permitindo trabalhar
em uma versão independente, mas ainda conectada ao repositório original
para facilitar contribuições futuras.

## 3.1 Bifurcando o Repositório do GitHub e Clonando no seu computador

1.  **Faça o Fork do Repositório**: No GitHub, acesse o repositório do
    mantenedor a partir do qual deseja bifurcar e clique no botão
    **Fork** no canto superior direito e depois em
    `+ Create a new fork`. Isso cria uma cópia do repositório em sua
    conta GitHub.

    ![](images/botao-fork.png)

2.  **Clone o Repositório Forkado**: Após ter feito o fork, você pode
    clicar na seta ao lado do botão **`<>Code`** para poder copiar o
    link HTTPS ou SSH para poder clonar o repositório.

3.  **Abra o VS Code e Clone o Repositório**: No VS Code (ou no git
    bash), abra o terminal e clone o repositório usando o link copiado a
    partir de sua conta no Github:

    ``` bash
    git clone https://github.com/seu-usuario/nome-repositorio.git>
    ```

    Esse comando cria uma cópia local do repositório forkado. Substitua
    `<URL_do_repositorio_forkado>` pelo link HTTPS ou SSH.

4.  **Navegue até a pasta do repositório clonado**:

    ``` bash
    cd nome_do_repositorio
    ```

    **Através do Git Bash:**

5.  Você pode também o processo acima dentro de uma pasta de
    repositórios, abrir o git bash, clonar o repo, ir para basta e
    depois abrir o VS-Code a partir dessa pasta. Use a sequência de
    colandos abaixo:

    ``` bash
    git clone <URL_do_repositorio_forkado>
    cd nome_do_repositorio
    code .
    ```

## 3.2 Configurando o Repositório Original como Remoto Upstream

Para manter seu fork sincronizado com o repositório original, adicione o
repositório original como um remoto adicional chamado `upstream`:

1.  **Adicione o repositório original como `upstream`**: sicronize o
    repositório remoto upstream usando o link copiado a partir da conta
    do proprietário original no Github

    ``` bash
    git remote add upstream https://github.com/usuario-original/nome-repositorio.git
    ```

2.  Verifique os repositórios local e remoto conectados

    ``` bash
    git remote -v
    ```

## 3.3 Mantendo seu Fork Atualizado

Quando desejar incorporar atualizações do repositório original
(`upstream`) ao seu fork `local` e `origin` no Github, basta seguir
estas etapas:

1.  **Buscar atualizações do repositório original**:

    ``` bash
    git checkout main    # Mude primeiro para a main
    git fetch upstream   # Busca atualizações 
    ```

2.  **Mesclar as atualizações**:

    ``` bash
    git merge upstream/main  # Mescala atualizações à branch local atual (main)
    ```

    O comando `git merge` deve ser executado na sua branch `main local`.
    A branch **`main` do `upstream` (ou seja, o repositório original)**
    é mesclada **na sua branch `main` local**.

3.  **Enviar as atualizações** para a sua cópia do repositório no Github

    ``` bash
    git push origin main
    ```

    Isso é necessário para enviar as atualizações mescladas do seu
    repositório local para o repositório do fork no GitHub (ou seja, seu
    `origin`). Assim, seu repositório remoto no GitHub também ficará
    sincronizado com o repositório original (upstream), refletindo as
    mudanças mais recentes.

> **`git push origin main`** é usado para enviar essas atualizações
> mescladas do seu repositório local para o seu repositório no GitHub
> (`origin`), garantindo que o seu fork também esteja atualizado com o
> repositório original.
>
> Isso sincroniza seu fork com as mudanças mais recentes do repositório
> original, mantendo seu projeto atualizado para futuras contribuições.

## 3.4. Criando branch e faça commit para as suas mudanças

Sempre que for colaborar, crie uma branch nova para trabalhar de forma
eficiente. Depois faça seus commits e pushes. Na seção 4.2, há uma
descrição mais detalhada desse processo de colaboração. A título de
exemplo, seguem os comandos para se colaborar:

``` bash
git checkout -b nome-branch # Crie a branch e comece a fazer alterações
git status
git add .
git status
git commit -m "Descreva as alaterações"
git push origin nome-branch
```

## 3.5. Explicação de termos do mundo Git

- **origin**:
  - É o nome padrão dado ao repositório remoto quando você clona ou
    bifurca (fork) um projeto.

  - Refere-se ao link do seu próprio repositório no GitHub, ou seja, o
    fork que está sob a sua conta de usuário.

  - Quando você executa `git push origin main`, está enviando as
    atualizações para o seu repositório no GitHub (o fork).
- **upstream**:
  - É o nome que se usa para o repositório remoto original, ou seja, o
    repositório principal do projeto de onde você fez o fork.

  - Configurar o `upstream` permite que você busque as atualizações mais
    recentes do repositório original sem afetar as suas próprias
    modificações no fork.

  - Você utiliza comandos como `git fetch upstream` e
    `git merge upstream/main` para trazer as mudanças mais recentes do
    repositório original, mantendo seu fork atualizado.
- **main**:
  - É o nome padrão da principal branch de desenvolvimento na maioria
    dos repositórios Git (anteriormente chamada de `master`).

  - Geralmente, a branch `main` contém o código mais estável e
    atualizado do projeto.

  - Ao mesclar (`merge`) a branch `main` do `upstream` ao seu
    repositório local, você garante que a main do seu fork local esteja
    em sincronia com o código estável do projeto.
- **Repositório local**: A cópia completa do repositório no seu
  computador, onde você faz todas as edições e testes.
- **Repositório remoto**: A versão do repositório hospedada em um
  servidor, como o GitHub, que pode ser acessada e compartilhada com
  outros colaboradores.

------------------------------------------------------------------------

# **4. Trabalhando com Versionamento no Terminal**

## 4.1. Versionando enquanto Mantenedor

Após ter criado uma cópia de seus repositório no seu computador e
sabendo que o mesmo poderá ser em bifurcação (fork) com outros
colaboradores, você como proprietário (mantenedor) pode querer aprimorar
ainda mais seus códigos dentro do projeto de análise. Siga os passos
abaixo para inserir suas alterações em arquivos editáveis como `.html`,
`.css`, `.htm`, `.py`, `.R`, `.Rmd`, `.qmd`, `.csv`, `.xlsx`, etc, ou
para adicionar arquivos não editáveis às pastas do projeto.

> **Nota:** Essas etapas são válidas quando você é o proprietário do
> repositório original. Usaremos apenas o terminal Git-bash do VS-Code
> para trabalhar de maneira eficiente com o Git. Clique neste
> <a href="https://www.youtube.com/watch?v=dSPVkmzuK60"
> target="_blank">link</a> para ver instrução de como configurar o
> Gitbash como terminal padrão no VS-Code.

### **4.1.1 Configuração inicial do upstream**

Enquanto mantenedor do repositório, você não precisa fazer configuração
inicial de upstream com o comando `git remote add upstream url-repo` .
Isso será necessário quando você for um colaborador de um projeto em
fork, conforme explicado na `Seção 3`.

### 4.1.2 Atualizando sua main local

1.  Mude para a branch `main` local:

    ``` bash
    git checkout main
    ```

2.  Use os comandos `git fetch origin` ou `git pull origin main` para
    obter as últimas alterações do repositório remoto (`origin`) que
    está no GitHub. Porém, as duas funcionam de forma diferente.

    1)  ) O comando `git fetch origin` busca as atualizações do
        repositório remoto, mas não as aplica automaticamente ao seu
        branch local. É útil se você deseja revisar as mudanças antes de
        aplicá-las. Depois teria que fazer `git merge origin/main` .
        Caso você deseje usar esse procedimento de revisar e mesclar,
        segue abaixo a sequência completa de comandos:

        ``` bash
        git fetch origin           # Busca as atualizações do repositório remoto sem aplicá-las

        git diff main origin/main  # Mostra as diferenças entre sua branch local e a versão no remoto
        git merge origin/main      # Mescla as atualizações do remoto na sua branch local
        git log --oneline          # Visualiza o histórico de commits para confirmar as mudanças
        ```

    <!-- -->

    2)  Já o comando **mais usado** é o `git pull origin main`, o qual
        busca as atualizações e já as mescla com a sua branch local.
        Aqui, `main` é o nome do branch principal. Caso você utilize
        outro branch principal (como `master`), substitua `main` por
        `master`.

    ``` bash
    git pull origin main 
    ```

    Esta opção com `git pull` será a **preferida** e mais **usada**,
    principalmente quando você já sabe que os códigos são provenientes
    de fontes confiáveis.

### **4.1.3 Criando nova branch antes de fazer mudanças**

1.  Crie e mude para uma nova branch para trabalhar em uma nova
    funcionalidade:

    ``` bash
    git checkout -b nome-branch
    ```

<!-- -->

2.  Para listar as branches locais e verificar em qual delas você está
    trabalhando, utilize:

    ``` bash
    git branch
    ```

### 4.1.4 Fazendo alterações no projeto

- Modifique múltiplos arquivos em diferentes pastas, conforme
  necessário.

- Crie novos arquivos ou exclua arquivos que não são mais necessários.

- Mantenha as alterações focadas na funcionalidade/correção em que está
  trabalhando.

- Realize commits frequentes para não perder o trabalho.

> Como **exercício**, faça modificações no arquivo de código `Python`
> chamado `script.py` ou insira uma linha de texto no arquivo
> `textos.txt`.

1.  Após realizar as modificações, verifique quais arquivos foram
    modificados

    ``` bash
    git status
    ```

<!-- -->

2.  Verifique as alterações específicas em cada arquivo:

    ``` bash
    git diff nome-darquivo
    ```

<!-- -->

3.  Adicione alterações ao stage:

    - Específico:

      ``` bash
      git add nome-arquivo
      ```

    - Todos os arquivos:

      ``` bash
      git add .
      ```

4.  Salve as alterações em um commit

    ``` bash
    git commit -m "Descrição das alterações"
    ```

<!-- -->

5.  Caso precise modificar o último commit (antes do push)

    ``` bash
    git commit --amend -m "Nova mensagem de commit"
    ```

### 4.1.5 Atualizando sua Branch com a Main Antes do Pull Request

1.  Busque as últimas alterações do repositório original

    ``` bash
    git fetch origin
    ```

<!-- -->

2.  Reaplique seus commits sobre a versão mais atual do origin

    ``` bash
    git rebase origin/main
    ```

<!-- -->

3.  Envie sua branch atualizada para seu repositório `origin`.

    ``` bash
    git push origin nome-branch
    ```

### 4.1.6. Criando e Gerenciando o Pull Request (PR)

Após enviar suas alterações para seu repositório, você precisa criar um
Pull Request (PR) para que suas mudanças sejam incorporadas ao
repositório original.

1.  Acesse a página do seu fork no GitHub e crie um `Pull Request`:

    - Clique no botão `Compare & Create Pull request` e depois em
      `Crea pull request`.

    - Inclua um título claro, uma descrição detalhada das alterações,
      referência a issues relacionadas (se houver), e evidências de
      testes, prints ou GIFs (se aplicável).

2.  Após criar o PR:

    - Como as modificações foram feitas por você mesmo, voê já pode
      mesclar e finalizar as alterações.

    - Se precisar responder a comentários de outros mantenedores do
      projeto e, neste caso, necessitar fazer ajustes, faça as
      alterações (sem precisar criar nova branch) e os novos commits
      serão automaticamente incluídos no PR:

      ``` bash
      git add .
      git commit -m "Ajustes conforme revisão do PR"
      git push origin nome-branch
      ```

3.  Aguarde a revisão e aprovação:

    - Esteja disponível para discutir as alterações.

    - O(s) mantenedor(es) pode(m) solicitar modificações antes do merge.

4.  O mantenedor ou proprietário do projeto aprova as alterações e faz o
    **`Merge`**

    - Clique em `Merge pull request` e depois em `Confirm merge`

### 4.1.7 Após o Merge do PR

Após o aviso de aprovação das alterações e realização do merge, você
deve atualizar as alterações na sua main do computador e apagar a branch
criada, se necessário.

1.  Retorne para a branch `main`

    ``` bash
    git checkout main
    ```

<!-- -->

2.  Atualize sua `main` local com as mudanças do `origin`

    ``` bash
    git pull origin main
    ```

3.  Remova a branch de feature localmente

    ``` bash
    git branch -d nome-branch
    ```

4.  Remova a branch de feature do seu repositório remoto

    ``` bash
    git push origin --delete nome-branch
    ```

------------------------------------------------------------------------

## **4.2. Colaborador em Repositório com Fork**

Caso você não seja o mantenedor do repositório, será necessário criar um
`Pull Request` (PR) para solicitar a inclusão das suas alterações na
branch principal (geralmente chamada de `main` ou `master`). Siga os
passos abaixo para colaborar corretamente num projeto utilizando os
comando do Git:

### 4.2.1 Configuração inicial do upstream

Se você ainda não fez a configuração inicial do upstream do respositório
clonado em seu computador (reveja subtópico [3. Clonando e Bifurcando um
Repositório (Fork)](#clonando-e-bifurcando-um-repositório-fork)), será
necessário fazê-lo para conectar seu repositório local ao repositório
original (upstream), conforme abaixo :

``` bash
git remote add upstream https://github.com/dono-original/nome-repositorio.git
```

### 4.2.2 Atualizando a Branch Main Local

Antes de iniciar o trabalho, garanta que a branch `main` do seu
repositório local esteja atualizada com a versão mais recente do
repositório remoto.

1.  Mude para a branch main:

    ``` bash
    git checkout main
    ```

<!-- -->

2.  Busque atualizações do repositório original:

    ``` bash
    git fetch upstream
    ```

<!-- -->

3.  Integre mudanças do `upstream/main` em sua `main` local

    ``` bash
    git merge upstream/main
    ```

<!-- -->

4.  Atualize seu fork no GitHub

    ``` bash
    git push origin main
    ```

### 4.2.3 Criando nova branch de feature

1.  Crie e mude para uma nova branch de funcionalidade ou de correções:

    ``` bash
    git checkout -b nome-branch
    ```

<!-- -->

2.  Se já tiver a branch e ela foi criada anteriormente, faça um merge
    ou rebase para incorporá-la à versão atual:
    - Merge:

      ``` bash
      git checkout nome-branch
      git merge main
      ```

    - Rebase:

      ``` bash
      git checkout nome-branch
      git rebase main
      ```

> **Nota:** O `merge` cria um novo commit de mesclagem, enquanto o
> `rebase` reaplica seus commits sobre as mudanças da `main`. Use o
> método que preferir, levando em consideração o fluxo de trabalho da
> equipe.

### 4.2.4 Fazendo Alterações no Projeto e Comitando

Nesta etapa, faça as alterações necessárias no projeto, como modificar
arquivos, adicionar novos arquivos ou pastas:

- Modifique múltiplos arquivos em diferentes pastas.
- Crie novos arquivos conforme necessário.
- Exclua arquivos que não são mais necessários.
- Mantenha as alterações focadas na funcionalidade/correção em que está
  trabalhando.
- Realize commits frequentes para não perder o trabalho.

1.  Verifique quais arquivos foram modificados:

    ``` bash
    git status
    ```

<!-- -->

2.  Verifique as alterações específicas em cada arquivo:

    ``` bash
    git diff nome-arquivo
    ```

<!-- -->

3.  Adicione as alterações ao stage:

    - Específico:

      ``` bash
      git add nome-arquivo
      ```

    - Todos os arquivos:

      ``` bash
      git add .
      ```

4.  Salve as alterações em um commit:

    ``` bash
    git commit -m "Descrição das alterações"
    ```

<!-- -->

5.  Caso precise modificar o último commit (antes do push)

    ``` bash
    git commit --amend -m "Nova mensagem de commit"
    ```

### 4.2.5 Atualizando com Upstream Antes do PR

É muito importante fazer esta etapa para ter certeza de que você possui
a versão mais estável e atualizada em sua `main` local.

1.  Busque as últimas alterações do upstream:

    ``` bash
    git fetch upstream
    ```

<!-- -->

2.  Reaplique seus commits sobre a versão mais atual do `upstream`:

    ``` bash
    git rebase upstream/main
    ```

<!-- -->

3.  Envie sua branch atualizada para seu fork no github:

    ``` bash
    git push origin nome-branch
    ```

### 4.2.6 Criando e Gerenciando Pull Request (PR)

1.  Após ter feito o envio das atualizações, vá até a página do seu fork
    no GitHub e crie um Pull Request:

    - Clique no botão `Compare & Pull Request`. Outra forma de abrir a
      Pull Request seria ir na branch criada e clicar no botão
      `Contribute` e depois em em `Open pull request`;
    - Somente se necessário, adicione uma descrição mais detalhada
      explicando a Solicitação de Mudanças, pois a mensagem de commit
      pode ser insuficiente.

2.  Clique em “`Create Pull Request`” para submeter a solicitação de
    alteração e aguarde a mesclagem do mantenedor do repo.

3.  Após criar o PR:

    O proprietário **clica na mensagem da commit** para ver o que foi
    alterado no projeto. Surge os arquivos modificados, destacando as
    linhas mudadas. O **proprietário** pode tomar três decisões:

    - **Aprovar a `Pull Request`.** Basta clicar em **`Review changes`**
      e depois marca a oção **`Approve`** e então clica em
      **`Submit review`** para encerrar a revisão. Surgirá a janela de
      mesclar (Merge) a alteração com a main original. Clique em
      **`Merge Pull Request`** e depois em **`Confirme merge`** .

    - **Recusar a Pull request e** explicar porque recusou a
      modificação.

    - **Ou solicitar modificações**. Se o proprietário precisar
      solicitar modificações, alguns procedimentos específicos deverão
      ser tomados, conforme se segue:

      - **Para o Proprietário do Repositório que solicitas as alterações
        de código:**

        1.  **Revise e comente nas linhas**: Depois que acessar a PR,
            clique no nome do commit e o arquivo modificado será aberto.
            Observe as linhas a serem mudadas e clique no sinal de mais
            `+` azul. Escreva um comentário explicando o que precisa ser
            alterado no código e clique no botão **Start Review** para
            iniciar a revisão e fará com que a PR fique pendente
            (pending).

        2.  **Solicite alterações**: Para finalizar a solicitação de
            alterações, clique na seta ao lado do botão
            **`Finish your review`**. Uma nova janela se abre e deixe um
            comentário explicativo, marque a opção **`Request changes`**
            e clique em **`Submit review`**. Isso sinalizará ao
            colaborador que há ajustes a serem feitos antes da aprovação
            (mensagem de e-mail será enviadada com o comentário da
            modificação a ser revisada), aparecendo também na sequência
            da Pull Request um botão de aviso chamado
            `Changes requested` de cor laranja. **Seja acessível para
            dúvidas**: Informe que o colaborador pode comentar no PR
            caso precise de esclarecimentos.

      - Para o **Colaborador que fará as modificações solicitadas:**

        1.  **Leia os comentários**: Revise os comentários e entenda o
            que precisa de ajustes nos códigos. Neste ponto, o
            colaborador não precisa mudar nada na Pull Request.

        2.  **Altere o código**: Faça as modificações na mesma branch
            criada antes em seu repositório local e realize todos os
            testes para ver se a funcionalidade foi alcançada ou o
            código foi corrigido. Salve os arquivos.

        3.  **Envie as mudanças para o PR**: Utilize os códigos abaixo
            para enviar as mudanças. Observe que será necessário outra
            commit para salvar as novas modificações.

            ``` bash
            # Faça as alterações necessárias 
            git add . 
            git commit -m "Ajustes conforme revisão do PR" 
            git push origin nome-branch
            ```

        4.  **Comente e finalize**: Se precisar de dar mais informações,
            use os comentários no PR para discutir e esclarecer pontos
            que você achou pertinente durante as alterações do código.

    Por fim, o proprietário do repositório verifica as correções
    clicando na nova commit desse Pull Request no Github; então, confere
    as mudanças e depois termina a revisão cliclando em
    **`Review changes`**, adicionando um comentário na janela que se
    abre, indicando se as modificações foram bem sucedidas. Depois,
    seleciona a opção **Approve** e clica em **`Submit Review`** para
    concluir. A janela do Pull Request se abrirá novamente, permitindo
    que o proprietário finalize o processo de mesclagem clicando em
    **`Merge Pull Request` e `Confirme merge`**.

### 4.2.7 Atualização da main `local` e `origin` após aprovação do PR

Depois que seu Pull Request (PR) for **revisado e aprovado pelos
mantenedores do projeto**, é importante realizar algumas etapas de
limpeza e organização no seu repositório local e remoto. Isso mantém seu
ambiente de trabalho organizado e sincronizado com o projeto principal.
Siga os comandos abaixo para atualizar suas branches e remover as que
não são mais necessárias:

1.  Retorne para a branch `main`:

    ``` bash
    git checkout main
    ```

<!-- -->

2.  Atualize sua `main` local com as mudanças do `upstream`:

    ``` bash
    git pull upstream main
    ```

<!-- -->

3.  Atualize a `main` do seu fork no Github:

    ``` bash
    git push origin main
    ```

<!-- -->

4.  Remova a branch de funcionalidade localmente:

    ``` bash
    git branch -d nome-branch
    ```

<!-- -->

5.  Remova a branch de funcionalidade do seu fork remoto:

    ``` bash
    git push origin --delete nome-branch
    ```

### 4.2.8 Considerações Finais

- **Pull Request (PR)** é o processo mais comum para sugerir mudanças em
  um projeto colaborativo no GitHub. Ao criar um PR, você solicita que
  suas alterações sejam revisadas e integradas à branch principal.

- **Comunicação**: Descreva claramente o que foi alterado no PR para
  facilitar a revisão. Isso ajuda o mantenedor a entender o contexto das
  mudanças.

- **Boa Prática**: Sempre trabalhe em branches separadas para manter a
  organização do repositório e garantir que a branch principal se
  mantenha estável.

------------------------------------------------------------------------

# 5. Recuperando Trabalho sem Branch

Se você fez alterações em arquivos, mas não criou uma branch e nem as
comitou, e percebeu que deveria estar trabalhando em uma nova branch,
não se preocupe. É possível criar uma nova branch e mover suas
alterações para ela, sem perder nada. Veja como proceder:

## 5.1 Salvando Alterações Atuais

1.  Salve temporariamente suas alterações não commitadas:

    ``` bash
    git stash save "Alterações em progresso"
    ```

## 5.2 Atualizando Main e Criando Branch

1.  Busque atualizações do repositório original:

    ``` bash
    git fetch upstream # Ou ...
    git fetch origin
    ```

<!-- -->

2.  Integre as mudanças do `upstream`:

    ``` bash
    git merge upstream/main  # Ou ...
    git merge origin/main
    ```

<!-- -->

3.  Crie e mude para uma nova branch:

    ``` bash
    git checkout -b sua-branch
    ```

## 5.3 Recuperando Alterações

1.  Recupere as alterações salvas no stash:

    ``` bash
    git stash pop
    ```

## 5.4 Após Resolver Conflitos (se houver)

1.  Adicione os arquivos resolvidos ao stage:

    ``` bash
    git add .
    ```

<!-- -->

2.  Crie um commit com as alterações:

    ``` bash
    git commit -m "Descrição das alterações recuperadas"
    ```

<!-- -->

3.  Envie a branch para seu fork:

    ``` bash
    git push origin sua-branch
    ```

## 5.5 Criando Pull Request e Procedimentos Seguintes

Após enviar suas alterações para seu fork, passe para a parte de criar
um Pull Request no GitHub e siga os procedimentos conforme descrito
anteriormente para proprietários ([4.1.6. Criando e Gerenciando o Pull
Request (PR)](#criando-e-gerenciando-o-pull-request-pr)) ou
colaboradores ([4.2.6 Criando e Gerenciando Pull Request
(PR)](#criando-e-gerenciando-pull-request-pr)) do repositório.

------------------------------------------------------------------------

# 6. Apagando Modificação Caso Haja Erro

Se ocorrer algum erro, é possível voltar ao estado anterior à
modificação. Você pode até reverter para um estado anterior mais
distante, mas é importante ter cuidado ao resetar commits mais antigos,
pois isso pode impactar o histórico do projeto. Mesmo que isso não seja
sempre necessário, é útil saber como proceder caso precise corrigir
algo.

## 6.1 Visualizar Histórico de Commits

Primeiro, você precisa verificar o histórico de commits e identificar o
ponto para o qual deseja reverter o projeto. Para isso, use o comando:

``` bash
git reflog
```

Esse comando exibirá uma lista com o histórico de commits e seus
identificadores (hashes), que são códigos alfanuméricos de 8 caracteres.
Identifique o commit anterior ao erro que você deseja corrigir.

## 6.2 Reverter ou Resetar o último commit

Para apagar a última modificação que foi mesclada (merged) em um projeto
usando Git, você tem algumas opções. Aqui está a forma mais segura de
fazer isso:

1.  Para reverter o último commit mesclado mantendo o histórico:

    ``` bash
    git revert HEAD
    ```

<!-- -->

2.  Se você quer remover completamente o último commit (não recomendado
    se já foi compartilhado):

    ``` bash
    git reset --hard HEAD~1
    ```

**Importante:**

- `revert` é mais seguro pois cria um novo commit que desfaz as
  alterações

- `reset --hard` é mais arriscado pois apaga o histórico

- Se o commit já foi enviado para o repositório remoto (pushed), use
  `revert`

- Se for local e ainda não compartilhado, pode usar `reset`

## 6.3 Resetar para um Commit Anterior

Para voltar a um commit anterior, execute o seguinte comando,
substituindo o identificador do commit pelo hash correspondente:

``` bash
git reset --hard 7d0932f
```

Esse comando redefine o repositório local para o estado do commit
especificado, desfazendo qualquer alteração feita após ele. **Cuidado**:
isso removerá qualquer mudança não comitada.

## 6.4 Revertendo o Reset (Opcional)

Se você mudar de ideia e quiser restaurar o commit que acabou de
resetar, pode voltar atrás executando novamente o comando `git reflog` e
usando o identificador do commit que deseja recuperar:

``` bash
git reset --hard 5a6cc0a
```

## 6.5 Sincronizar com o Repositório Remoto

Após fazer um reset local, é importante garantir que o repositório
remoto também esteja atualizado. Se o repositório remoto tiver commits
que você reverteu no local, será necessário forçar a atualização para
alinhar ambos os históricos. Isso pode sobrescrever as alterações no
servidor remoto, então tenha certeza das suas mudanças.

Para forçar o push das alterações locais para o repositório remoto,
utilize:

``` bash
git push --force
```

Esse comando força a sobrescrição do histórico remoto com o histórico
local.

## 6.6 Considerações Importantes

- **Usar `git reset --hard` com cautela**: Esse comando remove
  permanentemente as alterações que não foram comitadas e pode alterar o
  histórico de commits.

- **Reverta apenas se necessário**: Antes de usar o `--force` para
  sobrescrever o repositório remoto, certifique-se de que isso não
  afetará o trabalho de outros colaboradores.

- **Alternativa com `git revert`**: Em vez de usar `reset --hard`, você
  pode usar `git revert` para desfazer alterações sem alterar o
  histórico. Isso cria um novo commit que desfaz as mudanças, mantendo a
  integridade do histórico de commits.

------------------------------------------------------------------------

## 7. Descartando Alterações em Arquivos Específicos

Se você fez alterações em um arquivo, mas ainda não fez o commit e
deseja descartar essas modificações, retornando o arquivo ao estado do
último commit, siga os passos abaixo usando o Terminal do Git:

### 7.1 Verificar o Status do Repositório

Antes de qualquer ação, é importante verificar o estado atual do
repositório e ver quais arquivos foram modificados ou estão prontos para
commit.

``` bash
git status
```

Esse comando listará os arquivos que foram modificados e se estão ou não
no staging area (prontos para serem commitados).

### 7.2 Descartar as Alterações em um Arquivo Específico

Se você deseja descartar todas as modificações feitas em um arquivo
específico e restaurá-lo ao estado do último commit, use o seguinte
comando:

``` bash
git checkout -- nome-do-arquivo
```

Esse comando descarta as alterações locais não commitadas no arquivo
especificado, retornando-o ao estado do último commit.

### 7.3 Remover Arquivos do Stage (Caso Estejam Preparados para Commit)

Se o arquivo já foi adicionado ao staging area (ou seja, preparado para
commit com `git add`), mas você quer removê-lo dessa área sem descartar
suas alterações, use o comando abaixo:

``` bash
git reset HEAD nome-do-arquivo
```

Esse comando remove o arquivo do staging area e desfaz o `git add`, mas
mantém as alterações feitas no arquivo. Isso é útil quando você quer
revisar ou modificar mais antes de commitá-lo.

------------------------------------------------------------------------

# 8. Boas Práticas Gerais e Comandos Úteis

### 8.1 Boas Práticas

- **Commits Pequenos e Frequentes**: Realize commits de maneira
  frequente e com descrições claras. Isso facilita a revisão do código e
  ajuda a identificar pontos de erro rapidamente.

- **Sincronize Regularmente**: Faça `git pull` regularmente antes de
  começar a trabalhar para garantir que você está com a versão mais
  recente do projeto. Isso evita conflitos e confusões.

- **Use Branches**: Sempre crie uma nova branch para implementar
  mudanças específicas, mantendo a branch `master` ou `main` estável.

- **Revisão de Código (Pull Requests)**: Utilize Pull Requests para
  revisar as alterações de forma colaborativa antes de mesclá-las à
  branch principal. Isso melhora a qualidade do código e reduz o risco
  de bugs.

- **Mensagens de Commit Claras e Descritivas**: Escreva mensagens de
  commit que descrevam claramente as alterações feitas.

- **Verifique Arquivos Temporários**: Certifique-se de não incluir
  arquivos temporários ou irrelevantes no commit.

- **Mantenha um `.gitignore` Atualizado**: Mantenha o arquivo
  `.gitignore` atualizado para evitar que arquivos desnecessários sejam
  incluídos no repositório.

- **Teste Suas Alterações**: Sempre teste suas alterações antes de
  realizar um commit.

- **Revise Suas Alterações Antes do Commit**: Faça uma revisão cuidadosa
  das alterações antes de commitá-las.

- **Desfazer Alterações em Arquivos Específicos**: Para desfazer
  alterações em arquivos específicos, consulte a seção [7.2 Descartar as
  Alterações em um Arquivo
  Específico](#descartar-as-alterações-em-um-arquivo-específico).

- **Desfazer o Último Commit (Antes do Push)**: Para desfazer o último
  commit antes do push, utilize:

  ``` bash
  git reset --soft HEAD~1
  ```

## 8.2 Comandos Úteis

- **Mostrar Estado Atual do Repositório**:

  ``` bash
  git status
  ```

- **Listar Todas as Branches Locais**:

  ``` bash
  git branch
  ```

- **Mostrar Todos os Repositórios Remotos Configurados**:

  ``` bash
  git remote -v
  ```

- **Exibir Histórico de Commits de Forma Resumida**:

  ``` bash
  git log --oneline
  ```
