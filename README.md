
<!-- README.md é gerado a partir deste README.Rmd. Por favor, edite  e renderize este arquivo -->

# Tutorial de Uso do Git/Github com R e Rstudio

<!-- badges: start -->
<!-- badges: end -->

## Objetivo

O **Projeto Teste Fork** tem como objetivo fornecer orientações práticas
para usuários iniciantes e intermediários sobre como usar o Git e o
GitHub diretamente na interface do RStudio para controle de versão de
projetos. Na primeira parte, utilizamos as funções do pacote `usethis`,
e na seção “Trabalhando com Versionamento”, passamos a usar diretamente
os comandos do Git.

# Instruções Inicias para uso do Git/Github

1.  Crie uma conta gratuita no GitHub <https://github.com/>

2.  Descarregue o arquivo executável do Git neste link
    <https://git-scm.com/downloads>

3.  Instale o Git e depois abra e feche o Git Bash ao fim da instalação.
    Feche e reinicie o Rstudio para reconhecer o local de instalação do
    Git (Normalmente, fica em *C:/Program Files/Git/bin/git.exe*).

4.  Carregue o pacote `usethis` para configurar o Git para uso no
    Rstudio

``` r
library(usethis)
```

# Configurando o Git/Github no RStudio

5.  Vamos usar o pacote `usethis` e os comando abaixo para parear com a
    sua conta remota no Github. Acesse o nome da sua conta e e-mail em
    Configurações –\> Perfil Público (Settings).

``` r
usethis::use_git_config(user.name = "Seu Nome", 
                        user.email = "seu.email@exemplo.com")
```

6.  Criar um novo token ou regenerar o token (codigo de 40 dígitos serão
    produzido)

``` r
usethis::create_github_token() # Muda para o site do Github para fazer login
```

Depois de fazer login, gere o token na própria página do Github e o
copie o número. Você deverá colocar esse número no arquivo `.Renviron`.
O `.Renviron` é um arquivo de configuração do R que permite que você
especifique variáveis de ambiente para que fiquem disponíveis para o R.
Ele é muito usado para disponibilizar senhas, chaves de API, etc. -
coisas que são secretas - e por isso não é boa prática colocá-las no
código. Então execute o seguinte comando:

7.  **Abra o arquivo .Renviron**

``` r
usethis::edit_r_environ()
```

8.  Crie uma nova linha nesse arquivo, digitando primeiramente :
    GITHUB_PAT=SEU_TOKEN. Exemplo:

`GITHUB_PAT=ghp_Ko3mdlNJpBzQ7lvzKTvGFg91f6HpBQlablalba`

9)  Após adicionar o token copiado do site, pule uma linha e salve o
    arquivo.
10) Reinicie o RStudio: CTRL + SHIFT + F10

# Como criar repositório

## Criando repositório primeiro no Github

1.  A forma mais eficiente de criar repositório é fazer via o site do
    Github, pois tudo fica devidamente configurado

2.  Clique no notão verde **New**

3.  Preencha as informações conforme figura abaixo

<img src="images/clipboard-142360520.png" width="637" />

## Clone o repositório em seu computador

1.  Clone o repositório para que seja criado na sua máquina local.
    Clique no botão verde **Code**. Copie a url do projeto para poder
    clonar.

2.  Em seguida, no RStudio, você pode criar uma cópia desse repositório
    para trabalhar em **Projeto com Versionamento** indo em
    `File–> New projec`t e escolha a opção de `Version Control –> Git` e
    coloque a **url** do repositório e especifique a pasta onde este
    será salvo.

3.  Ao fazer desta maneira, seu respositório já fica vinculado ao git do
    seu computador e, obviamente, está pareado com o Github na internet.

<img src="images/clipboard-3984491672.png" width="376" />

## **Implemente pequenas mudanças no seu projeto de teste**

1.  Faça pequenos testes de alteração no seu repositório teste, como:
    *criar pasta e arquivo nesta pasta, comitar (versionar) por meio da
    aba `git` botão `Commit`, realizar `Push`*`.`

2.  Verifique no servidor do Github as suas alterações.

3.  Agora, faça alteração no arquivo `Readme.md` no Github web, commit e
    depois faça Pull no RStudio. Observe no arquivo se houve a mudança.

## Inclua pastas e arquivos no arquivo .gitignore

Geralmente precisamos que arquivos e pastas não sejam
compartilhados/divulgados. Para isso, insira as pastas e arquivos no
arquivo .`gitignore`. Verifique neste Projeto_Teste_Fork quais pastas e
arquivos não são compartilhados.

## Criando o Repositório no Computador

Não é a forma mais recomendada, mas é possível criar um repositório
pareado com o Github, no computador primeiro, da sequinte maneira:

``` r
usethis::create_project(path = "D:/Git/Clube_Codigo/Nome_Projeto")
usethis::use_git()    # Digite no console desse projeto para ligá-lo ao Git
usethis::use_github() # Digite no console desse projeto para levá-lo ao Github
```

**A partir de um projeto existente no computador:**

Você também pode criar a partir de um
`Projeto já existem em seu computador`. Primeiro carregue o projeto e
depois use as duas útlimas linhas de comando acima para ligá-lo ao Git e
carregá-lo ao Github.

# Clonando e bifurcando um respositório (fork)

## Fazendo um fork com o usethis

Quando queremos trabalhar em colaboração com mais pessoas, podemos não
só clonar um respositório, mas também bifurcá-lo ao mesmo tempo. Para
isso, utilize os comandos abaixo.

``` r
usethis::create_from_github(
  repo_spec = "https://github.com/Evaldo-Martins-STAT/Projeto_Teste_Fork",
  destdir = "D:/Git/Clube_Codigo/",
  fork = TRUE)
```

## **Fazendo um Fork do Repositório no GitHub**

1.  Acesse o repositório original no GitHub.

2.  Clique no botão **Fork** no canto superior direito para criar uma
    cópia do repositório em sua conta.

3.  Siga os passos acima para clonar o repositório forkado em seu
    computador

# Contribuindo com um Projeto de Análise

## Passo a passo de como fazer modificações

Após ter criado uma cópia do repositório a partir do Github remoto
usando a opção de fork (Bifurcamento), você pode querer melhorar o
código desse projeto de análise. Siga os passo abaixo para inserir as
suas linhas de código, seja em arquivos `*.R`, `*.Rmd`, `*.qmd`,
`*.csv`, `*xlsx`, ou quaisquer outros arquivos editáveis, ou inserir
outros não editáveis dentro das pasta do projeto.

1.  **Primeiro, sempre** crie um galho ou ramificação (**branch**) - A
    criação de branch é recomendada antes de alterar qualquer arquivo do
    projeto em que você pretende contribuir. É importante que você
    esteja na branch principal (master) e use o comando abaixo no
    console, dando nome apropriado à branch que reflita as modificações
    que deseja implementar.

<!-- -->

2.  Depois, comece a fazer as contribuições nos arquivos desejados ou
    mesmo criar novos arquivos e pastas. Você fará pequenas pequenas
    modificação no arquivo Readme.Rmd, mais especificamente na Tabela
    abaixo, incluindo seu nome e e-mail. Depois renderize (aperte no
    botão `Knit`) para concluir a produção, também, do arquivo
    `Readme.md`.

3.  Após término das suas alterações, realize o `Commit` com os comando
    do git mais abaixo e o faça o `push` para as modificaçãoes irem para
    o repositório do Github. Siga procedimentos mais abaixo

4.  A página do Github se abrirá para que você possa completae o
    `Pull Request (PR)`

5.  Então comente as mudanças que fez e clique em
    `Criar Requerimento Pull` (ou `Create Pull Request`)

6.  Aguarde o mantenedor do projeto fazer a mesclagem (Merge). Após a
    mesclagem, aparecerá o botão Merged (Ou Mesclado). Só então você
    finaliza sua contribuição, fechando a brunch no Rstudio

    **Obs1:** Quanto ao mantenedor, a mesclagem da branch de
    modificações com a branch master do projeto pode ser feita no
    Github. Após mesclar com a branch `master`, o mantenedor pode
    inclusive fazer pequenas alterações nas linhas de código recém
    mescladas e incluir um novo `Commit` e `Push`.

7.  Por sua vez, quando receber um aviso do mantenedor de que foi aceita
    a sua contribuição, o (a) colaborador(a) deve voltar para a branch
    `master` no RStudio, e então realizar o
    <span style="color: lightblue;">**Pull**</span> para atualizar as
    contribuições suas mescladas e outras que eventualmente o mantenedor
    do repositório acrescentou.

8.  Volte à branch que você criou e delete-a usando os comando abaixo no
    terminal

9.  Apague a branch no seu computador e no Github

10. Pronto, você está com a versão mais atualizada na sua brach
    principal (master)

    **Obs2**: Como boa prática, sempre comunique o mantenedor de suas
    modificaçãoes.

## **Trabalhando com versionamento no Terminal**

De agora em diante, vamos trabalhar via Terminal do RStudio a fim de
trabalhar de forma mais profissional com o versionamento de códigos.

### **Verificando o histórico de atualizações**

Certifique-se de que você está no diretório do projeto, digitando
`getwd()` no console. Agora vamos ver o histórico de comando. Digite no
terminal:

`git reflog`

A aparecerá uma lista de todos os commits (versionamentos) que você já
fez no projeto e de seus colaboradores. Vamos agora executar as etapas
listadas acima

### **Criação de Branches e Commits**

- Antes de criar a branch para começar as modificações, verifica as suas
  branches locais como o comando

`git branch`

Aparecerão as branches e a branch atual, que será destacada em verde.

- Vamos agora criar uma nova branch em que trabalharemos no arquivo
  Readme.Rmd para aprendermos a usar essas funcionalidades do git.
  Chamaremos essa branch de “leia-me”.

`git branch leia-me`

Verifique se ela foi criado com o comando abaixo ou na aba Git do
Rstudio

`git branch`

- É preciso mude agora para a branch em que deseja trabalhar. Digite os
  seguintes comando:

`git checkout leia-me`

`git branch`

### Realizando alterações

Vamos agora fazer umas alterações pequenas no arquivo Readme.Rmd e
salve-o (Renderize que você já vai salvar), e depois feche-o.

**Cadastre seu nome e endereço de e-mail abaixo:**

| \#  |              Nome              |          e-mail           |
|:---:|:------------------------------:|:-------------------------:|
|  1  |    Evaldo Martins da Silva     |   evaldomartins@ufpa.br   |
|  2  | Rayane Leticia Furtado Pinheio | rayanefurtado63@gmail.com |
|  3  | Carlos Thayan Moreira Ferreira | thayanmoreira1@gmail.com  |
|  4  |          Elton Correa          |    eltonpesc@gmail.com    |
|  5  |                                |                           |
|  6  |                                |                           |
|  7  |                                |                           |

Lista de Colaboradores do Projeto (Repositório).

- Digite o seguinte comando abaixo para identificar qualquer modificação
  nos arquivos:

`git status`

- Adicione a modificação. Mas lembre que a modificaçõa ainda não foi
  para a branch master

`git add .`

`git status`

### Fazendo o commit e push das modificações

- Vamos fazer o commit dessa alteração (versionamento)

`git commit -m "Adicionando nome e e-mail"`

- Estando tudo certo até agora, faça o `git push` para enviar ao Github

`git push`

Ele dá uma mensagem de erro quando criamos uma branch nova. Copie a
sugestão de comando e execute novamente.

`git push --set-upstream origin leia-me`

- Verifique agora no Github as duas versões do arquivo de texto em cada
  uma das branches, ou seja, `leia-me` e `master`.

### Realizando a mesclagem

- É preciso, então, realizar a MESCLAGEM da `leia-me` para a `master`.
  Se vc for o mantendedor do projeto, volte ao terminal do RStudio e
  digite:

`git branch`

Agora vamos unir o código. Você vai entrar na branch que vai receber as
atualizações, no caso a branch master com os seguintes comandos:

`git checkout master`

`git branch`

Agora podemos mesclar da `leia-me` para a `master`.

**Obs**: Antes de fazer a mesclagem, recomenda-se puxar (pull) as
atualizaçãoes que estão no servidor para a sua máquina, pois pode ser
que algum outro colega fez atualizações (é preciso não mexer na mesma
parte de funcionalidade do código que você) e você pode correr o risco
de estar fazendo mesclagem com uma versão antiga. Digite os comandos
abaixo:

`git pull`

`git merge leia-me`

- Faça agora o git push para enviar ao Github remoto

`git push`

Agora vá na branch master do Github remoto e verifique se o código foi
atualizado na master. Só adicione os códigos que foram testados e estão
funcionando corretamente.

### Apague as branches locais e remota

- Finalmente, `apague a branch local e remota.` Mude para outra branch,
  como a master e apague a branch local

  `git checkout master`

  `git branch -d nome-da-branch`

- Se quiser forçar a exclusão de uma branch se ela ainda não foi
  mesclada, use:

  - `git branch -D nome-da-branch`

- Para apagar a branch no repositório remoto, você precisa usar o
  seguinte comando

  `git push origin --delete nome-da-branch`

**Obs: Caso não seja o mantenedor do projeto,** veja como se faz o
processo de alterar/comitar/empurrar/mesclar/apagar branch em *Criando
uma Pull Request* usando o terminal.

## **Mais um exercício de aplicação**

Vamos criar mais uma linha no arquivo de texto (ou outra funcionalidade
qualquer no projeto)

1.  Faça a atualização: `git pull` na master

2.  Crie a sua branch e mude para ela:
    `git checkout -b sistema-de-login master`

3.  Crie um novo arquivo txt chamado
    `sistema de login.txt (ou login2.txt)` e salve-o.

4.  Digite `git add . && git status` e o arquivo ficará pronto para ser
    adicionado

5.  Confirme essas alterações: `git commit -m "Criado sistema de Login"`

6.  Digamos que tudo esteja funcionando e checado o código remotamente,
    volte para a master:

    `git checkout master && git branch`

7.  Atualize o código da master: `git pull`

8.  Agora sim, você pode mesclar: `git merge sistema-de-login master`

9.  Mande essa alteração para o servidor: `git push`

10. Observe no servidor do github as alterações

11. Apague a branch:
    `git checkout master && git branch -d nome-da-branch`

12. Apague a branch remotamente:
    `git push origin --delete nome-da-branch`

# **Criando um Pull Request**

Em alguns casos, só vamos conseguir unir códigos se fizermos uma
requisição para uma pessoa responsável pelo repositório através do
processo chamado Pull request. Vamos imaginar que você queira fazer
alterações via a branch sistema-de-login.

1.  Vamos entrar na nossa master `(git checkout master)`, fazer
    `git pull` e depois mudar para a branch sistema-de-login:
    `git checkout sistema-de-login`

2.  Altere o arquivo `login.txt` acrescentando a linha: “Digite sua
    idade**“** e salve o arquivo.

3.  Adicione : `git add . && git status`

4.  Agora faça commit:
    `git commit -m "Adicionado idade ao sistema de login"`

5.  Agora, seu código precisa ser mesclado por outra pessoa da equipe.
    Você faz um push e não mescla nada como feito acima. Digite de
    dentro da branch modificada: `git push`

6.  O Sitema vai pedir que digite um novo comando:
    `git push --set-upstream origin sistema-de-login`

7.  Veja na página no Github e observará que aparece a branch
    sistema-de-login atualizada recentemente e que pede para comparar e
    fazer Pull Request. Clique em `Compare & Pull Request`

8.  O sistema muda para a janela indicando que a solicitação de
    mesclagem vai da branch sistema-de-login para a master

9.  Você pode explicar mais em comentários ao mantenedor sobre sua
    contribuição e clique em `Create Pull Request`

10. A pessoa que tiver o poder para fazer a revisão e mesclar, pode
    clicar em `Merge Pull Request`

11. Vá para master e faça um git pull para obter as modificações
    mescladas

12. Apague a branch: veja acima como apagar um branch pelo terminal.

# **Apagando a última modificação**

Caso aconteça algum erro, é possível voltar ao momento anterior às
modificações (ou até ainda a um anterior a este se os conflitos forem
grandes, mas **tenha muito cuidado em resetar commits mais antigos**).
Observamos que esta parte de reverter mudanças pode não ser tão
necessária, pois usamos poucos linhass de códigos. Mesmo assim, vamos
ver algumas funções básicas , caso precise. Primeiro vemos o histórico
de atualizações.

1.  Digite `git reflog` no terminal e veja qual o identificador do
    commit (`hash do commit`, um número alfanumérico com 8 caracteres)
    anterior a essa modificação

2.  Para resetar mudanças posteriores, digite o comando seguinte
    acompanhado do identificador anterior : `git reset --hard 7d0932f`

    **Obs:** Caso vc se arrependa dessa eliminação, você pode voltar
    atrás, fazendo um `git reflog` e digitar o numero de identificação
    da modificação que se arrependeu de apagar:
    `git reset --hard 5a6cc0a`

3.  Mas se vc quer continuar com a modificação, você precisará que o
    histórico local do seu repositório não fique atrás do histórico
    remoto. Você deve forçar que o histórico remoto seja igual ao local
    (o que pode sobrescrever alterações remotas, para isso tenha certeza
    da modificação). Você deve usar o comando  
      
    **`git push --force`**

    Obs: veja a partir do minuto 23:00 do vídeo
    `Curso de Git e Github Completo 2023` para mais esclarecimentos.

# **Considerações Finais**

- **Reverter um commit:** Mantém o histórico do commit original e
  adiciona um novo commit que desfaz as mudanças.

- **Resetar para um estado anterior:** Reescreve a história do
  repositório, removendo commits subsequentes.

- **Recomenda-se toda vez que fizer um commit, fazer `git push`**, antes
  de fazer novas alterações, para evitar a mensagem de 1 ou 2 commit a
  frente das modificações. Dá pra fazer, mas cuidado em fazer pull entre
  seu commit e seu push, pois pode gerar conflito de versões. Tudo para
  evitar trabalhar em versões não atualizadas.

- O “Pull with rebase” na aba Git, e especificamente na interface do
  RStudio, é uma operação que combina o comando **`git pull`** com a
  opção **`--rebase`**. Isso significa que, ao buscar e integrar as
  mudanças do repositório remoto, suas mudanças locais não commitadas ou
  suas novas alterações serão reaplicadas no topo do histórico do
  repositório remoto. **Isso é particularmente útil quando fazemos reset
  para um commit no passado**. Outras situações em que **devemos usar o
  Pull with rebase:**

  - **Manter um histórico de commit limpo e linear**: Ao usar rebase, o
    histórico do commit parece como se todas as mudanças fossem
    aplicadas uma após a outra, sem os commits de merge.

  - **Colaborar em um projeto com muitos colaboradores**: Um histórico
    linear facilita a compreensão do que foi alterado e por quem.

    ## Descartando alterações

**Como descartar alterações não commitadas em um arquivo e retornar ao
estado do último commit**? Siga os seguintes comandos no Terminal do
Git:

`git status`

`git checkout -- nome-do-arquivo`

`git reset HEAD nome-do-arquivo (Para remover alterações no stage)`

## Alterações não comitadas e sem ter feito uma branch

É possível **mover modificações não commitadas para uma nova branch?**

Sim. Vamos ver os passos necessários para criar uma nova branch, mover
suas alterações para essa nova branch e depois commitá-las.

- `git status`
- `git checkout -b nova-branch`
- `git status`
- `git add .`
- `git commit -m "Descrição das alterações"`
- `git push origin nova-branch`

# Mais informações

**Mais informações neste vídeo:**

[Curso de Git e Github COMPLETO 2023 \[Iniciantes\] + Desafios + Muita
Prática](https://www.youtube.com/watch?v=kB5e-gTAl_s&t=539s)

[Curso gratuito Git e Github \#7 - Desfazendo
commit](https://www.youtube.com/watch?v=CAlg29rF2VY)  

**E nesta série Riffomonas (Code Club):**

[How to set up git for a bioinformatics project: using version control
with git and GitHub](https://www.youtube.com/watch?v=DnwEaa5QtpI)

[Integrating RStudio with a new or existing project on GitHub
(CC120)](https://www.youtube.com/watch?v=sxErFMF7BJY&list=PLmNrK_nkqBpJtNdQBPhPWjIFRYeFOGfJ1&index=10)

[Easy ways to go back in your git commit history with RStudio
(CC153)](https://www.youtube.com/watch?v=Y9h-1u6uQ6c&list=PLmNrK_nkqBpJtNdQBPhPWjIFRYeFOGfJ1&index=7)

# Anexo de criação do arquivo Readme.rmd

Para criar o Readme.rmd usei a função `usethis::use_readme_rmd()` . O
que há de tão especial sobre usar o `README.Rmd` em vez de apenas o
`README.md`?

Res.: Você pode incluir chunks como este:

``` r
summary(cars)
#>      speed           dist       
#>  Min.   : 4.0   Min.   :  2.00  
#>  1st Qu.:12.0   1st Qu.: 26.00  
#>  Median :15.0   Median : 36.00  
#>  Mean   :15.4   Mean   : 42.98  
#>  3rd Qu.:19.0   3rd Qu.: 56.00  
#>  Max.   :25.0   Max.   :120.00
```

Você ainda precisará renderizar `README.Rmd` regularmente, para manter
`README.md` atualizado.

Você também pode incorporar gráficos, por exemplo:

![](README_files/figure-gfm/pressure-1.png)<!-- -->

Nesse caso, não se esqueça de fazer o commit e enviar (push) os arquivos
de figura resultantes para que eles sejam exibidos no GitHub.
