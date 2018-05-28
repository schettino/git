# Git

### Desenvolvimento de Software 3

---

![Image](./assets/md/assets/1.png)

---

## Tópicos - Parte 1

* Introdução
* Comandos iniciais
* Fases do commit
* Workflows
* Desafios comuns

---

## Tópicos - Parte 2

* Code review
* Github
* CI & CD
* Exemplo: do commit ao publish
* Open source

---

## Introdução

* Contexto histórico
* Por que Git?
* O que é um repositório

---

## Comandos iniciais

---

* **git init**: cria um diretório .git com subdiretórios para objetos e referências
* **git branch**: operações em _branches_ como listar, criar e remover
* **git checkout**: altera branch a ser trabalhado
* **git add** indexa arquivos a serem commitados
* **git commit _-m_**: consolida modificações

---

### Exemplo: inicialização de um repositório para um novo projeto

---

```console
  home$ mkdir projeto && cd projeto
  projeto$ git init
  projeto$ echo "Hello From Git" >> README.md
  projeto$ git add README.md
  projeto$ git commit -m "started readme.me file"
  [master (root-commit) f35a9c8] started readme.me file
  1 file changed, 1 insertion(+)
  create mode 100644 README.md
```

---

```console
projeto$ git log --oneline
f35a9c8 (HEAD -> master) started readme.me file
```

![Image](./assets/md/assets/g1.png)

---

```console
  projeto$ git checkout -b dev
  Switched to a new branch 'dev'
  projeto$ echo "This is a demo repo" >> README.md
  projeto$ git add README.md
  projeto$ git commit -m "added repo description"
   [dev 596ff92] added repo description
    1 file changed, 1 insertion(+)
```

---

```console
  projeto$ git log --oneline
  596ff92 (HEAD -> dev) added repo description
  f35a9c8 (master) started readme.me file
```

![Image](./assets/md/assets/g2.png)

---

```console
git diff master
```

![Image](./assets/md/assets/g3.png)

---

## Fases do commit

---

## Unstaged

* Contém, à priori, todas as modificações no diretório do projeto
* alterações que permaneçam nesse estado não serão enviadas à origem

---

## Staging

* através do comando git-add, as modificações realizadas são indexadas.
* novas alterações no arquivo passam a ser seguras
* representa um estado anterior ao commit

---

## Commit

* todas as alterações indexadas são encapsuladas em um commit
* deve conter uma mensagem curta e auto explicativa
* gera-se um hash único para essas alterações

---

## HEAD

* Representa o um ponteiro para a referência do branch atual que, por sua vez, é um ponteiro para o último commit realizado nesse branch.
* O diretório do projeto será um reflexo do útlimo commit associado à HEAD

---

![workflow](https://git-scm.com/book/en/v2/images/reset-workflow.png)

---

# Workflows

---

* Centralizado
* Feature Branching
* Gitflow

---

## Centralizado

---

![Image](./assets/md/assets/w1.png)

---

* commits são feitos diretamente no branch master
* ideal para quem está em trasição do SVN
* à medida que o projeto e time crescem, essa estratégia pode se tornar um problema

---

## Feature Branch

---

![Image](./assets/md/assets/w2.png)

---

* Funcionalidades são desenvolvidas isoladamente
* Minimiza a ocorrência de conflitos
* Ao serem finalizadas, as funcionalidades são unificadas no branch **master**
* Apesar de proporcionar uma melhor organização do desenvolvimento, não são definidas aqui para lidar com fluxo de correção de bugs, publicação e testes.

---

# Gitflow

---

* Aborda praticamente todas as situações esperadas no ciclo de desenvolvimento e manutenção de um projeto
* Facilita a integração de ferramentas para CI e CD.
* Conflitos são mínimos
* Facilita a manutenção de mais de uma versão do sistema em produção
* Atende a todos os tamanhos de projetos

---

### Possui branches para

* Hotfixes
* Features
* Releases

---

![Image-w3](./assets/md/assets/w3.png)

---

1.  **develop** é criado a partir do **master**
2.  **relase** é criado a partir do **develop**
3.  **feture-x** é criado a partir do **develop**
4.  Após finalizada, realiza-se o merge do **feature-x** no **develop**
5.  Após preparada a release, realiza-se o merge do respectivo branch **release** no **develop** e no **master**
6.  Se um problema é identificado no **master** um branch **hotfix-x** é criado
7.  Quando **hotfix-x** é finalizado, é feito o merge no **master** e **develop**

---

## Sincronizando repositório com a origem

* **git remote**: configurações de origem do repositório
* **git push**: envia modificações para origem
* **git pull**: baixa últimas modificações da origem
* **git merge** unifica dois branches
* **git rebase**

---

## Desafios comuns

---

* origin/branch recebeu atualizações
* merges realizados no ancestral do branch atual

---

## Outros problemas

* Commit com mensagem e/ou arquivos errados
* Commit em branch errado
* Merge realizado em branch errado
* Hitórico de commits não preservado

---

## Soluções

* git-reset e git-amend
* git rebase
* git pull --rebase
* git merge --no-ff

---

### Desfazendo commit local

**git-amend**

Desfaz último commit, movendo alterações de volta para `staging` e cria um novo commit com as correções.

Novas alterações que entraram em `staging` serão commitadas também.

---

**git-amend**

_Problemas_:

* Commit anterior já havia sido enviado
* Commit dado em branch errado

---

**git-amend** <br />
_Commit anterior já havia sido enviado_

_amend_ afetará histórico do branch. Alguém da equipe pode ter iniciado um novo trabalho baseado no commit a ser removido.

Envio modificações no histórico é impedido a menos que use `git push --force`

---

**git-amend** <br />
_Commit dado em branch errado_

Solução: `git reset [--soft | --mixed | --hard] ..`

---

**git-reset** <br />

---

### Próximos desafios

* Desfazer um `rebase`
* Lidando com rebases que ocorrem na origem
* 3-way merge

---

<!-- REFERÊNCIAS -->

### Referências

* [Pro Git 2nd Edition (2014), _Scott Chacon_](https://github.com/progit/progit2)
* [Atlassian tutorials](https://www.atlassian.com/git/tutorials)
* [Gitflow, _Vincent Driessen_](http://nvie.com/posts/a-successful-git-branching-model/)
* [git-merge vs git-rebase](https://www.derekgourlay.com/blog/git-when-to-merge-vs-when-to-rebase/)
