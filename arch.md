# Linux - Ambiente de Desenvolvimento - Arch

Seguir passo a passo --> https://wsldl-pg.github.io/ArchW-docs/How-to-Setup/


## 1) Instalando o Arch
Method 1: zip file
> Run Arch.exe to extract the rootfs and register to WSL

Depois que executar o Arch.exe já vai aparecer no Windows Terminal
Se não aparecer pode executar novamente o Arch.exe
Quando entrar pelo WSL 

Definir a senha do root
> [root@PC-NAME]# passwd

Depois:
> [root@PC-NAME]# echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel
(setup sudoers file.)
> [root@PC-NAME]# useradd -m -G wheel -s /bin/bash {username}
(add user)

> [root@PC-NAME]# passwd {username}
(set default user password)

No meu caso.
> passwd manel

Voltando na pasta do windows para definir o usuário
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


## 3) ZSH, Oh My ZSH ang pluguins

Install ZSH - <https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH>
> pacman -S zsh
ou
> yay -Sy zsh


Configurar o terminal zsh como default. OBS: Será necessário fazer um logout para salvar
> chsh -s $(which zsh)

Pacotes que pdem ser necessario: curl git

Plugins do ZSH --> Zinit <https://github.com/zdharma-continuum/zinit?tab=readme-ov-file#install> 
    
> bash -c "$(curl --fail --show-error --silent --location https://raw.githubusercontent.com/zdharma-continuum/zinit/HEAD/scripts/install.sh)"
    
Adicionando os plugins no zsh --> # abrir o arquivo de configurações o zsh

> nano ~/.zshrc

Adicione no final do .zshrc

    zinit light zdharma-continuum/fast-syntax-highlighting
    zinit light zsh-users/zsh-autosuggestions
    zinit light zsh-users/zsh-completions
    zinit load zdharma-continuum/history-search-multi-word
    zinit light "spaceship-prompt/spaceship-ember"

    
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

