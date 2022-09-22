# Git e Github



### GIT

É um sistema de versionamento: você controla as modificações de um projeto por meio de versões chamadas "commits". 



### Github

É um serviço online de hospedagem de repositórios Git remotos.

• Possui uma interface gráfica web: github.com 

• É uma plataforma social (usuários, página de perfil, seguidores, colaboração, etc.). Dica: currículo!

• Maior serviço do mundo de hospedagem de projetos de código aberto 

• Modelo de cobrança: gratuito para projetos de código aberto, pago para projetos privados 

• Alternativas: BitBucket, GitLab, etc.



### Repositório remoto e local

Um projeto controlado pelo Git é chamado de repositório de versionamento. 

Tipicamente uma cópia "oficial" do repositório fica salvo em um servidor (<span style="color:red;">repositório remoto</span>). 

Cada pessoa que trabalha no projeto pode fazer uma cópia do repositório para seu computador (<span style="color:red;">repositório local</span>). A pessoa então faz suas alterações no projeto (novos commits) e depois salva as alterações no servidor.



###  Configurando sua identificação no Git

```bash
	git config --global user.name "Seu nome"
	git config --global user.email "Seu email de cadastro do Github"
	
	git config --list
```

### Configurar chave SSH para o Github

SSH é um protocolo para comunicação de dados com segurança. 

O Github aboliu a autenticação somente com usuário e senha. 

A ideia básica é cadastrar previamente quais computadores podem acessar o Github em seu nome. Outros computadores não conseguem acessar. 

Para isto você deve: 

(1) Gerar uma chave SSH no seu computador 

(2) Cadastrar essa chave no seu Github

```bash
	ssh-keygen -t ed25519 -C "your_email@example.com"
```

### Salvar primeira versão de um projeto no Github

Considerando que agora seu ambiente já está todo configurado (usuário e email, visualização de arquivos ocultos, chave SSH), sempre que você criar um novo projeto, os passos básicos serão estes (troque os parâmetros em <span style="color:blue;">azul</span> pelos seus dados)

```bash
	git init
	git add .
	git commit -m "Mensagem explicativa"
	git branch -M main
	git remote add origin git@github.com:seuusuario/seurepositorio.git
	git push -u origin main
```

### Salvar uma nova versão

```bash
	git status
	git add .
	git commit -m "Mensagem explicativa"
	git push
```

### Clonar e modificar um projeto de um repositório remoto que você tem permissão para alterar

```bash
	git clone git@github.com:seuusuario/seurepositorio.git
	git add .
	git commit -m "Mensagem explicativa"
	git push
```

### Verificando o histórico de versões

```bash
	git log
```

### Listagem resumida

```bash
	git log --oneline
```

### Reset para levar todos os arquivos para o estado original, tira tudo do staged

```bash
	git reset
```

### Commit de arquivo especifico

```bash
	git add nomeDoArquivo
```

### Git diff

• Comando que mostra a diferença entre arquivos modificados 

• Dica: utilizar o VS Code, que mostra graficamente as diferenças

```bash
	git diff nomeDoArquivo
```

### Git checkout

• Permite modificar temporariamente os arquivos do projeto ao estado de um dado commit ou branch 

```bash
	git checkout codigoCommit
```

• Código do commit, HEAD 

​	• Cada commit possui um código, que pode ser utilizado para referenciar o commit 

​	• O último commit do histórico do branch corrente também pode ser referenciado pela palavra HEAD

​	• É possível referenciar um commit N versões antes de HEAD usando ~N, por exemplo: 

​		• HEAD~1 (penúltimo commit) 

​		• HEAD~2 (antepenúltimo commit) 

```bash
	git checkout HEAD~1
```

***• IMPORTANTE: antes de fazer o checkout para voltar para HEAD, certifique-se de que não haja mudanças nos arquivos. Se você acidentalmente mudou alguma coisa, desfaça as modificações usando:***

```bash
	git reset
	git clean -df
	git checkout --
```

### Voltando para o estado original

```bash
	git checkout main
```

### Arquivo .gitignore

• É um arquivo que indica o que **NÃO** deve ser salvo pelo Git. 

• Geralmente o arquivo .gitignore fica salvo na pasta principal do repositório. Mas também é possível salvar outros arquivos .gitignore em subpastas do repositório, para indicar o que deve ser ignorado por cada subpasta.

### Casos comuns de arquivos que não devem ser salvos pelo Git:

• Arquivos compilados 

​	Linguagens compiladas (C, C++, Java, C#, etc.) geram arquivos de código compilado para executar o programa localmente. 

• Arquivos de bibliotecas externas usadas no projeto 

​	Projetos reais utilizam bibliotecas externas (programas prontos disponíveis na Internet). Por exemplo, projetos JavaScript com NPM tipicamente salvam uma subpasta "node_modules" na pasta do seu projeto. 

• Arquivos de configuração da sua IDE 

​	IDE's podem salvar uma subpasta com arquivos de configuração na pasta do projeto (exemplo: .vscode). • Arquivos de configuração do seu sistema 

​	Por exemplo, sistemas Mac podem gravar uma subpasta .ds_store na pasta do projeto.



***Site criador de .gitignore: https://www.toptal.com/developers/gitignore***



# Resolvendo problemas comuns



### Como remover arquivos da área de stage (Unstage)

```bash
	git status
	git reset
```

### Como desfazer modificações não salvas

```bash
	git status
	git reset
	git clean -df
	git checkout -- .
```

### O que fazer quando abre o editor VIM

Estas ações podem abrir o editor VIM no terminal: 

​	• Fazer um commit sem mensagem 

​	• Fazer um merge de três vias 

Habilitar o modo de edição:

```bash
	i
```

### Sair do VIM, salvando as alterações:

```bash
	<ESC>
	:wq
	<ENTER>
```

### Sair do VIM, descartando as alterações:

```bash
	<ESC>
	:q!
	<ENTER>
```

### Como desfazer o último commit

Desfazer último commit sem desfazer as modificações nos arquivos:

```bash
	git status
	git reset --soft HEAD~1
```

### Como deletar commits e também modificações nos arquivos

Voltar o projeto ao estado de um dado commit (deletar commits e alterações posteriores a esse commit)

```bash
	git status
	git reset --hard <código do commit>
```

Voltar o projeto ao estado do penúltimo commit:

```bash
	git status
	git reset --hard HEAD~1
```

**<span style="color:red;">ATENÇÃO: ação destrutiva!</span>**

### Como atualizar o repositório local em relação ao remoto

```bash
	git status
	git pull <nome do remote> <nome do branch>
```

### Como resolver push rejeitado

Não é permitido enviar um push se seu repositório local está atrasado em relação ao histórico do repositório remoto! 

Você tem que atualizar o repositório local: 

```bash
	git pull <nome do remote> <nome do branch>
```

### Resolvendo conflito

• Analise o código fonte 

• Faça as edições necessárias 

• Faça um novo commit

### Como sobrescrever um histórico no Github

```bash
	git push -f <nome do remote> <nome do branch>
```

**<span style="color:red;">ATENÇÃO: ação destrutiva!</span>**

### Como apontar o projeto para outro repositório remoto

```bash
	git remote set-url origin git@github.com:seuusuario/seurepositorio.git
```



# Branches e trabalho em equipe

### Convidando colaboradores para o projeto no Github

Projetos públicos no Github podem lidos / baixados / clonados / forkados por qualquer pessoa. 

Por padrão outros usuários não tem permissão de escrita no seu repositório remoto. 

Como liberar permissão de escrita a um repositório remoto? 

​		Settings -> Collaborators

![Introdução aos branches](https://i.imgur.com/7yf3uCk.png)

### Manipulando branches localmente

Listar branches

```bash
	git branch
```

Criar branch

```bash
	git branch nome-do-branch
```

Criar branch e ativa-lo

```bash
	git branch -b ft-login
```

Deletar branch (**<span style="color:red;"> ação destrutiva!</span>**)

```bash
	git branch -d nome-do-branch
```

Deletar branch mesmo sem ter feito merge dele ainda (**<span style="color:red;"> ação destrutiva!</span>**)

```bash
	git branch -D nome-do-branch
```

### Merge fast forward

![Merge fast forward](https://i.imgur.com/EOUu2DU.png)

A operação merge serve para mesclar o histórico de um branch de origem para um branch de destino. 

O comando git pull pode ser entendido como um "merge" entre o branch do repositório remoto para o repositório local. 

O comando merge deve ser feito a partir do branch de DESTINO.

### Passo a passo

```bash
	(main) git merge ft-login
```

![Step to Step](https://i.imgur.com/U2sTWOS.png)

Atenção: o procedimento "correto" é fazer um merge do branch main para o branch de feature, e não o contrário. 

Uma vez que o branch de feature esteja devidamente mesclado, cria-se um pull request no repositório remoto.

### Procedimento pull request

![Procedimento pull request](https://i.imgur.com/RzFROGc.png)

Atenção: __<u>não</u>__ se faz atualização no branch main do repositório remoto enquanto a feature não estiver **homologada**. Isso porque o branch main tipicamente está configurado com um processo automatizado de **CI/CD**, ou seja, atualizações na branch main já disparam automaticamente uma nova build da aplicação, e/ou até mesmo a **implantação** da aplicação em **ambiente de produção**.



### Procedimento pull request

![Procedimento pull request](https://i.imgur.com/zKcOD67.png)

1) Atualize o branch main local e faça o merge do main para o branch de feature. Depois salve o branch de feature no repositório remoto

```bash
	(main) git pull origin main
	(main) git checkout ft-login
	(ft-login) git merge main
	(ft-login) git push -u origin ft-login
```

2) No repositório remoto, abra um pull request da feature enviada. 
3) Depois de passar pelo processo de homologação, aprove a pull request. 
4) Opcional: delete o branch de feature no repositório remoto.

### Merge de três vias (3-way)

![Merge de três vias (3-way)](https://i.imgur.com/ygQNIhc.png)

### Resolução de conflito

![Resolução de conflito](https://i.imgur.com/QjhA3K7.png)

Conflito ocorre quando mais de uma via alterou o mesmo arquivo. 

A resolução de conflito é uma operação manual, que exige habilidade do desenvolvedor. 

	1. Edite o código fonte, resolvendo o conflito 
	1.  Faça um novo commit

### Procedimento fork + pull request

Mesmo que você não tenha permissão de escrita em um repositório do Github, você pode enviar contribuições para este repositório. 

Este procedimento é a base para colaboração em projetos de código aberto.

Passos: 

1. Faça um fork do repositório original para o seu Github 
2. Clone seu repositório "forkado" para seu computador 
3. Crie um novo branch e faça as alterações nesse branch 
4. Envie as alterações para seu repositório "forkado" 
5. Crie uma pull request para o repositório original
