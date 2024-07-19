## 1) SSH

Gerar a Chave
> ssh-keygen

Copiar a chave para o cadastrar no github
> cat ~/.ssh/id_ed25519.pub

Configurar:

> git config --global user.email "mfcf86@gmail.com"

> git config --global user.name "ManoelFelipe"

> git config --list

Testar a conexão
> ssh -T git@github.com


## 2) GIT_HUB

> git init
   
below is used to add a new remote:
> git remote add origin git@github.com:User/UserRepo.git

> git remote add origin git@github.com:ManoelFelipe/Enem

below is used to change the url of an existing remote repository:
> git remote set-url origin git@github.com:User/UserRepo.git

> git remote set-url origin git@github.com:ManoelFelipe/Enem
    
> git remote -v

> git branch -M main

> git status
    
    O git pull é um comando usado para atualizar suas branches locais de acordo com as branches remotas. Ele é uma combinação de dois comandos: git fetch seguido por git merge.

> git pull origin main
    
> git add .

> git commit -m "first commit"
 
> git push -uf origin main

## 3) Git Ignore

> touch .gitignore

> git rm -r --cached .ipynb_checkpoints/

Exemplos
> https://gist.github.com/octocat/9257657

Docs
> https://git-scm.com/docs/gitignore

> https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#_ignoring


