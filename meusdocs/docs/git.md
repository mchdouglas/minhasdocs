## Git

<p>Se você caiu nesta documentação provavelmente criou vergonha na cara e decidiu aprender sobre o git (na verdade isso é mais um tutorial do que uma documentação, que serve tanto para eu aprender a passar meus conhecimentos como para você que está lendo aprender). </p>

## Vamooos nessaaa!!

<p>Antes de começarmos e sairmos digitando comandos que nem loucos, vamos a uma breve e chata(porém importante) história sobre o git.</p>

## Uma Breve História do Git

<p>Uma Breve História do Git
Como muitas coisas na vida, o Git começou com um pouco de destruição criativa e uma controvérsia de fogo.

O núcleo (kernel) do Linux é um projeto de código aberto com um escopo bastante grande. A maior parte da vida da manutenção do núcleo o Linux (1991-2002), as mudanças no código eram compartilhadas como correções e arquivos. Em 2002, o projeto do núcleo do Linux começou usar uma DVCS proprietária chamada BitKeeper.

Em 2005, a relação entre a comunidade que desenvolveu o núcleo do Linux e a empresa que desenvolveu BitKeeper quebrou em pedaços, e a ferramenta passou a ser paga. Isto alertou a comunidade que desenvolvia o Linux (e especialmente Linux Torvalds, o criador do Linux) a desenvolver a sua própria ferramente baseada em lições aprendidas ao usar o BitKeeper. Algumas metas do novo sistema era os seguintes:

- Velocidade

- Projeto simples

- Forte suporte para desenvolvimento não-linear (milhares de ramos paralelos)

- Completamente distribuído

- Capaz de lidar com projetos grandes como o núcleo o Linux com eficiência (velocidade e tamanho dos dados)

Desde seu nascimento em 2005, Git evoluiu e amadureceu para ser fácil de usar e ainda reter essas qualidades iniciais. Ele é incrivelmente rápido, é muito eficiente com projetos grandes, e ele tem um incrível sistema de ramos para desenvolvimento não linear.

[Clique aqui para acessar essa história](https://git-scm.com/book/pt-br/v2/Come%C3%A7ando-Uma-Breve-Hist%C3%B3ria-do-Git).

# Primeiros passos

<p>Primeiramente iremos instalar o git, no meu caso utilizo o sistema operacional linux mint e para este deve ser utilizado o seguinte comando:</p>
<code>sudo apt install git</code>
<p>Se você utiliza outro sistema operacional acesse:</p>

[esse guia de downloads](https://git-scm.com/downloads)

## Configuração inicial

<p>Seguidamente utilizaremos o <code>git config</code> para a configuração do nome do usuário e do email.Abram o terminal e digitem:</p>
<code>git config --global user.name "Digite aqui seu nome de usuário"</code>
<p>E se você achar que não deu certo só porque não apareceu nada no seu terminal você está errado. Confiem em mim kkkk, o user name  já está configurado. Agora vamos configurar o email, se liga no comando abaixo:</p>
<code>git config --global user.email "Digite aqui seu email"</code>
<p>Agora para realmente saber se tudo deu certo digite: <code>git config user.name</code> que deverá retornar o nome do usuário. E do email fica como tarefa hahaa.

## Inicializando um repositório

A primeira etapa para utilização do git, é você definir o seu Working Directory(Diretório de trabalho). Para isso existem várias formas. Vamos as duas principais:

Para novos projetos, onde você ira iniciar e enviar os arquivos locais existentes para um repositório vazio, vamos utilizar os seguintes comandos:

```git
git init
git add remote origin seurepositorio
```

Para projetos que já existem no servidor, você ira utilizar os seguintes comandos:

```git
git clone seurepositorio
```

## Adicionando arquivos

O primeiro comando que precisamos utilizar é para adicionar arquivos ao seu WorkTree. O comando git é `git add`. Vamos aos exemplos:

Adicionar o arquivo `readme.md` : `git add readme.md`  
Adicionar todos arquivos `js` : `git add .js`  
Adicionar todos os `arquivos` : `git add .`

## Commitando as alterações

Após adicionar os arquivos, precisamos informar as alterações, mensagens que eles sofreram. Para isso vamos utilizar o comando `git commit`. Vamos aos exemplos:

Enviando o primeiro commit: `git commit -m "Primeiro commit"`<br>
Commit de uma aleração: `git commit -m "Foi alterado tal coisa"`

## Enviando as alteações para o servidor

Após definir seus commits, precisamos enviar os mesmos para o servidor. Para isso utilizamos o comando `git push`

Comando padrão para enviar `git push -u origin SEUBRANCH`

_o parâmetro -u indica o usuário que está no git config_
_o paramentro origin indica que irá para a origem no proximo parâmetro_
_SEUBRANCH indica o branch que você esta trabalhando_.

## Extras

As vezes ficar digitando a senha toda vez que for dar um push pode ser um pouco cansativo.Para isso existe uma configuração de chave ssh que pode te ajudar muito com essa situação. Então siga as instruções abaixo para gerar uma chave ssh e adicioná-la no seu github.

### Gerando a chave ssh

Primeiramente abra o terminal e cole o seguinte comando:
`ssh-keygen -t rsa -b 4096 -C "seu-emaill@examplo.com"`. E
se aparecer algumas perguntas só vai dando enter (são configurações desnecessárias).<br>Pronto agora sua chave foi gerada e para acessá-la digite `cd ~/.ssh`.

### Vinculando ao Github

Agora basta copiar a chave publica dentro do diretoŕio que você acessou o arquivo tem o seguinte nome `id_rsa.pub`. <br>
Depois de ter copiado o conteúdo do arquivo basta acessar sua conta no github ir nas configurações e procurar por SSH and GPG keys, vai em New SSH Key, feito isso aparecerá pra você dar um título para sua chave e bem abaixo um campo para colar ela.
Feito isso está tudo configurado.<br>
Para saber se está tudo certo digite o seguinte comando para testar: `ssh -T git@github.com` se retornar com seu username e uma mensagem de sucesso está tudo correto. Parabéns você sabe ler uma documentação kkkk.

### Alguns problemas

As vezes você já deve ter um repositório conectado por https, e não por SSH. Para ver na qual está conectado digite `git remote -v`, se retornar algo como `origin https://github.com/......` você está usando o serviço de http e para funcionar o ssh você precisa remover esse controle remoto com `git remote rm origin`, logo em seguida copie o link SSH e adicone como novo controle remoto com o seguinte comando `git remote add origin <link_ssh_copiado>`.<br> Se você segui a risca essa documentação tudo deverá estar funcionando. Você pode encontar esse tutorial [aqui](https://stackoverflow.com/questions/33880832/github-ssh-key-claiming-it-is-not-used).
