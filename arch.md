# Linux - Ambiente de Desenvolvimento - Arch

## 1) Instalando o Arch
Seguir passo a passo --> https://wsldl-pg.github.io/ArchW-docs/How-to-Setup/

Method 1: zip file
> Run Arch.exe to extract the rootfs and register to WSL

Depois que executar o Arch.exe já vai aparecer no Windows Terminal
Se não aparecer pode executar novamente o Arch.exe
Quando entrar pelo WSL 

Definir a senha do root

> [root@PC-NAME]# passwd

Depois:
(setup sudoers file.)

> [root@PC-NAME]# echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel


(add user)

> [root@PC-NAME]# useradd -m -G wheel -s /bin/bash {username}


> [root@PC-NAME]# passwd {username}
(set default user password)

No meu caso.
> passwd manel

Voltando na pasta do windows para definir o usuário
Usar o cmd para esse comando

> Arch.exe config --default-user {username}
(setting to default user)

Quando entrar no Arch 

> sudo pacman-key --init

> sudo pacman-key --populate

> sudo pacman -Sy archlinux-keyring

> sudo pacman -Su

> sudo pacman -Syyuu

> sudo pacman -Sy wget openssh

> nano ~/.nanorc

include /usr/share/nano/sh.nanorc
 

## 2) Agora vamos instalar o repositório dos usuários AUR 
Site: <https://aur.archlinux.org/>

Para isso precisamos **yay** - <https://github.com/Jguer/yay>
> sudo pacman -S --needed git base-devel

> cd /tmp

> git clone https://aur.archlinux.org/yay.git

> cd yay

> makepkg -si

> rm -rf yay

Para atualizar com pacman e yay:
> sudo pacman -Syu

> yay -Syu


## 3) ZSH, Oh My ZSH ang pluguins

Install ZSH - <https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH>
> sudo pacman -S zsh

> yay -Sy zsh


Configurar o terminal zsh como default. OBS: Será necessário fazer um logout para salvar
> chsh -s /bin/bash

> chsh -s /usr/bin/zsh

> sudo usermod --shell /bin/bash {user}

> sudo usermod --shell /usr/bin/zsh {user}

Pacotes que pdem ser necessario: curl git
Ajustando o History
Em .zshrc: export HISTFILE=~/.zsh_history

> touch .zsh_history

> ls -l $HISTFILE

> chmod 600 $HISTFILE

> chown {user} $HISTFILE

    ####### History ###############
    HISTFILE=~/.zsh_history
    HISTSIZE=10000
    SAVEHIST=10000
    export HISTFILE=~/.zsh_history
    setopt EXTENDED_HISTORY          # Write the history file in the ':start:elapsed;command' format.
    setopt INC_APPEND_HISTORY        # Write to the history file immediately, not when the shell exits.
    setopt SHARE_HISTORY             # Share history between all sessions.
    setopt HIST_EXPIRE_DUPS_FIRST    # Expire a duplicate event first when trimming history.
    setopt HIST_IGNORE_DUPS          # Do not record an event that was just recorded again.
    setopt HIST_IGNORE_ALL_DUPS      # Delete an old recorded event if a new event is a duplicate.
    setopt HIST_FIND_NO_DUPS         # Do not display a previously found event.
    setopt HIST_IGNORE_SPACE         # Do not record an event starting with a space.
    setopt HIST_SAVE_NO_DUPS         # Do not write a duplicate event to the history file.
    setopt HIST_VERIFY               # Do not execute immediately upon history expansion.
    setopt APPEND_HISTORY            # append to history file
    setopt HIST_NO_STORE             # Don't store history commands
    ###############################
    setopt correct

Plugins do ZSH --> Zinit <https://github.com/zdharma-continuum/zinit?tab=readme-ov-file#install> 
    
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


## 4) Fontes e Configurando o Starship

Ajustando as Fontes - Instalando fontes
Nerd fonts(ícones) --> <https://github.com/ryanoasis/nerd-fonts/>

<https://archlinux.org/packages/extra/any/ttf-fira-code/>
    
Instalar essas fontes no Windows Também.
E no perfil do Windows Terminal do 

> yay -Sy ttf-fira-code

Starship --> <https://starship.rs/guide/>
> yay -Sy starship

Add the following to the end of ~/.zshrc:
> eval "$(starship init zsh)"

Configurando --> <https://starship.rs/config/>
> mkdir -p ~/.config && touch ~/.config/starship.toml

Mudando simbolos: <https://www.nerdfonts.com/cheat-sheet>
Starship config: <https://starship.rs/presets/nerd-font>

## 5) Criando Alias de comando úteis
Instando comando úteis
<https://zaiste.net/posts/shell-commands-rust/>
> yay -Sy bat exa fd ripgrep procs grex
    
ALIAs
> nano ~/.alias

    alias list="exa --icons --group-directories-first -1 -laSghHF"
    alias ll="ls -alF"
    #alias update="sudo apt-get update && sudo apt-get upgrade -y"
    alias cls='clear'

    alias ls='exa --icons'
    alias cat='bat'
    alias find='fd'
    alias grep='rg'
    alias ps='procs'

> echo 'source ~/.alias' >> ~/.zshrc

> source ~/.zshrc

## 6) Instalando ASDF
Site: <https://asdf-vm.com/guide/getting-started.html>
> yay -Sy asdf-vm

> echo 'source /opt/asdf-vm/asdf.sh' >> ~/.zshrc

> asdf plugin update --all

Pyton:
> asdf plugin-add python

> yay -Sy tk

> asdf list-all python

> asdf install python {version}

> asdf global python {version}

NodeJs:
> asdf plugin-add nodejs

> asdf list-all nodejs

> asdf install nodejs {version}

> asdf global python {version}

JAVA:
> asdf plugin-add java

> asdf list-all java

> asdf install java {version}

> asdf global java {version}

> echo 'source ~/.asdf/plugins/java/set-java-home.zsh' >> ~/.zshrc

Vericiar a Variável $JAVAHOME
> echo $JAVA_HOME

> asdf list

Para mais linguagens etc
<https://gist.github.com/felipefontoura/726f88e67b8fa68f18a6e399a6e529a2>

## 7) Instalando Docker, Docker Compose e Portaniner

> yay -S docker

> sudo systemctl start docker

> sudo systemctl status docker 

> docker --version

Depois da Instalação
<https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user>

> sudo groupadd docker

> sudo usermod -aG docker $USER

> newgrp docker

> docker run hello-world

Docker Compose
> yay -S docker-compose

Portaniner
Link: <https://docs.portainer.io/start/install-ce/server/docker/linux>
> docker volume create portainer_data

> docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ee:latest


## 8) Instalando Conda-Forge
Link: <https://conda-forge.org/download/>
/home/manel/Downloads/Conda_Forge

Gosto de instalar em: /home/manel/conda_forge/miniforge3
> bash Miniforge3-Linux-x86_64.sh

> conda config --set auto_activate_base False

> conda activate base

> conda create -n env_01

> conda activate env_01

> conda create -n tf tensorflow

> conda deactivate

> conda update --all

> conda instal notebook matplotlib plotly seaborn

> conda install scikit-learn statsmodels

> jupyter notebook --no-browser

> jupyter-lab --no-browser

> conda info --envs

> conda remove --name env_01 --all

> pip install --upgrade pip

> conda update --all

## 9) Outros

WSL - Export and Import
    
> wsl --export Ubuntu_22.04-1 c:\Users\manoe\OneDrive\TI\ubuntu-22.04_13_09_23.tar
    
> wsl --import Ubuntu_22.04-2 C:\Linux\Ubuntu_16_04_24 c:\Users\manoe\OneDrive\TI\WSL\ubuntu-22.04_16_04_24.tar

> sudo pacman -Syu

> yay -Syu

> yay -Ps


