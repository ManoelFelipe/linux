# Linux - Ambiente de desenvolvimento - Ubuntu

1) Install Ubuntu

> sudo apt update && sudo apt upgrade

2) Install ZSH - <https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH>

> sudo apt-get install zsh

Configurar o terminal zsh como default. OBS: Será necessário fazer um logout para salvar
> chsh -s $(which zsh)

pacotes que pdem ser necessario
> sudo apt install curl git
    

3) Install Oh My ZSH
   
Oh My Zsh - a delightful & open source framework for Zsh
> sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    
4) Plugins do ZSH --> Zinit <https://github.com/zdharma-continuum/zinit?tab=readme-ov-file#install> 
    
> bash -c "$(curl --fail --show-error --silent --location https://raw.githubusercontent.com/zdharma-continuum/zinit/HEAD/scripts/install.sh)"
    
Adicionando os plugins no zsh --> # abrir o arquivo de configurações o zsh

> nano ~/.zshrc

Adicione no final do .zshrc

    zinit light zdharma-continuum/fast-syntax-highlighting
    zinit light zsh-users/zsh-autosuggestions
    zinit light zsh-users/zsh-completions
    zinit load zdharma-continuum/history-search-multi-word
    
> zinit self-update
> zinit update --all
    
Em .zshrc
dump zcompdump files into new dir instead of home dir
> export ZSH_COMPDUMP=$ZSH/cache/.zcompdump-$HOST-$ZSH_VERSION


5) Ajustando as Fontes
Instalando fontes
Nerd fonts(ícones) --> <https://github.com/ryanoasis/nerd-fonts/>
    
Instalar essas fontes no Windows Também.
> Installing · tonsky/FiraCode Wiki (github.com)
> sudo apt-get install fonts-firacode

6) Configurando Temas
    
Starship --> <https://starship.rs/guide/>
> curl -sS https://starship.rs/install.sh | sh

Add the following to the end of ~/.zshrc:
> eval "$(starship init zsh)"

Configurando --> <https://starship.rs/config/>
> mkdir -p ~/.config && touch ~/.config/starship.toml

Mudando simbolos: <https://www.nerdfonts.com/cheat-sheet>
Starship config: <https://starship.rs/presets/nerd-font>

Meu Exemplo em starship.toml no repositório. [starship.toml](/starship.toml)

Outro Exemplo: <https://fadeevab.com/my-configs-for-fancy-looking-terminal-starship-exa/>

Opcional: Spaceship --> https://spaceship-prompt.sh/config/intro/
    
7) Instalando ASDF --> https://asdf-vm.com/guide/getting-started.html
> git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.14.0

    
8) Instalar EXA: 
> sudo apt-get install exa
    
9) ALIAs
> nano ~/.zshrc

    alias list="exa --icons --group-directories-first -1 -laSghHF"
    alias ll="ls -alF"
    alias update="sudo apt-get update && sudo apt-get upgrade -y"
    alias cls='clear'
    
> source ~/.zshrc

10) DOCKER --> Install Docker Engine on Ubuntu | Docker Docs

> sudo apt-get update

> sudo apt-get install ca-certificates curl

> sudo install -m 0755 -d /etc/apt/keyrings

> sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
> sudo chmod a+r /etc/apt/keyrings/docker.asc

> echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

> sudo apt-get update
> sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

Testando:
> sudo docker run hello-world
> sudo su 
> docker ps

Rodando com o root vamos liberar para o usuário
<https://docs.docker.com/engine/install/linux-postinstall/>
> sudo groupadd docker
> sudo usermod -aG docker $USER

Testando:
> docker run hello-world
> docker ps

Nota:
> sudo systemctl disable docker.service
> sudo systemctl disable containerd.service
    
11) Portainer --> <https://docs.portainer.io/start/install-ce/server/docker/linux>

> docker volume create portainer_data

> docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest

Verificando:
> docker ps -a
> https://localhost:9443
    
12) Conda-Forge - Miniforge --> https://github.com/conda-forge/miniforge

> bash Miniforge3-Linux-x86_64.sh

/home/manel/conda_forge/miniforge3
    
    # >>> conda initialize >>>
    # !! Contents within this block are managed by 'conda init' !!
    __conda_setup="$('/home/manel/conda_forge/miniforge3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
    if [ $? -eq 0 ]; then
        eval "$__conda_setup"
    else
        if [ -f "/home/manel/conda_forge/miniforge3/etc/profile.d/conda.sh" ]; then
            . "/home/manel/conda_forge/miniforge3/etc/profile.d/conda.sh"
        else
            export PATH="/home/manel/conda_forge/miniforge3/bin:$PATH"
        fi
    fi
    unset __conda_setup
    # <<< conda initialize <<<
     
> conda config --set auto_activate_base True
> conda config --set auto_activate_base False

Se precisar:    
> nano /home/manel/.jupyter/jupyter_notebook_config.py

    ## The optional location of the settings schemas directory. If given, a handler
    #  will be added for settings.
    #  Default: ''
    c.LabServerApp.schemas_dir = '/home/manel'
    
> conda activate base

> conda deactivate
    
> conda create --name env_01 --clone base

> conda activate env_01

> conda update --all

> conda install notebook

> conda install pandas

> conda install scikit-learn

> conda install scikit-learn-intelex

> conda install statsmodels

> jupyter notebook --no-browser
   
13) SSH e GIT_HUB

13.1) Gerar a Chave
> #ssh-keygen

13.2) Copiar a chave para o cadastrar no github
> cat ~/.ssh/id_rsa.pub

13.3) Testar a conexão
>  ssh -T git@github.com

> git init

> git config --global user.email "mfcf86@gmail.com"

> git config --global user.name "ManoelFelipe"

> git config --list
   
below is used to add a new remote:
> git remote add origin git@github.com:User/UserRepo.git
below is used to change the url of an existing remote repository:
> git remote set-url origin git@github.com:User/UserRepo.git
    
> git remote -v
    
    
> git branch -M main
> git status
    
    # O git pull é um comando usado para atualizar suas branches locais de acordo com as branches remotas. Ele é uma combinação de dois comandos: git fetch seguido por git merge.

> git pull origin main
    
> git add .
> git commit -m "first commit" 
> git push -uf origin main

14) WSL - Export and Import
    
> wsl --export Ubuntu_22.04-1 c:\Users\manoe\OneDrive\TI\ubuntu-22.04_13_09_23.tar    

> wsl --import Ubuntu_22.04-2 C:\Linux\Ubuntu_16_04_24 c:\Users\manoe\OneDrive\TI\WSL\ubuntu-22.04_16_04_24.tar


15) Comando variados úteis
> find ~/Projetos -type f -name "*.Identifier" -exec rm -f {} \;

> find ~/Projetos -name "*.Identifier"