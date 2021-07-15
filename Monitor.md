# Como alterar a resolução no linux

- Precisamos saber qual o perfil que estamos conectados com o comando `xrandr` alem disso também é possível saber as resoluções com mais facilidade
Exemplo:
``` 
~$ xrandr 
Screen 0: minimum 1 x 1, current 800 x 600, maximum 8192 x 8192
Virtual1 connected primary 800x600+0+0 (normal left inverted right x axis y axis) 0mm x 0mm
   800x600       60.00*+  60.32  
   2560x1600     59.99  
   1920x1440     60.00  
   1856x1392     60.00  
   1792x1344     60.00  
   1920x1200     59.88  
   1600x1200     60.00  
   1680x1050     59.95  
   1400x1050     59.98  
   1280x1024     60.02  
   1440x900      59.89  
   1280x960      60.00  
   1360x768      60.02  
   1280x800      59.81  
   1152x864      75.00  
   1280x768      59.87  
   1024x768      60.00  
   640x480       59.94  
Virtual2 disconnected (normal left inverted right x axis y axis)
Virtual3 disconnected (normal left inverted right x axis y axis)
Virtual4 disconnected (normal left inverted right x axis y axis)
Virtual5 disconnected (normal left inverted right x axis y axis)
Virtual6 disconnected (normal left inverted right x axis y axis)
Virtual7 disconnected (normal left inverted right x axis y axis)
Virtual8 disconnected (normal left inverted right x axis y axis)
  1920x1080_60.00 (0x546) 173.000MHz -HSync +VSync
        h: width  1920 start 2048 end 2248 total 2576 skew    0 clock  67.16KHz
        v: height 1080 start 1083 end 1088 total 1120           clock  59.96Hz
```
- Ao final do comando é possivel ver a resolução de sua tela

- Depois de descobrir a resolução da sua tela escreva o comando `cvt` com sua resolução
Exemplo:
```
~$ cvt 1920 1080 60
```
- Copie o resultado apos o "Modeline"
Exemplo:
```
# 1920x1080 59.96 Hz (CVT 2.07M9) hsync: 67.16 kHz; pclk: 173.00 MHz
Modeline "1920x1080_60.00"  173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync
```
- Crie um novo modo(Resolução) para o xrand com o comando `sudo xrandr --new mode` e o resultado do seu Modeline
Exemplo:
```
~$ xrandr --newmode "1920x1080_60.00"  173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync
```
- Depois disso escolha seu novo modo com o comando `sudo xrandr --addmode` o Perfil ativo e o "modo" criado
Exemplo:
```
~$ xrandr --addmode Virtual1 "1920x1080_60.00"
```
- Após isso já é possivel alterar a resolução para a resolução desejada, com o comando `sudo xrandr -s` e a resolução desejada 
Exemplo:
```
~$ xrandr -s 1920x1080
```
- Mas para salvar esssas configuracões vocês terão que utilizar o comando `gedit ~/.profile` onde abrirá um arquivo de texto no final dele vocês colarão os seus comandos `sudo xrandr --newmode` e `sudo xrandr --addmode` e salvarão o arquivo(`Ctrl+S`) assim sera vocês terão o perfil dessa resolução com um acesso muito mais facíl
Exemplo:
```
# ~/.profile: executed by the command interpreter for login shells.
# This file is not read by bash(1), if ~/.bash_profile or ~/.bash_login
# exists.
# see /usr/share/doc/bash/examples/startup-files for examples.
# the files are located in the bash-doc package.

# the default umask is set in /etc/profile; for setting the umask
# for ssh logins, install and configure the libpam-umask package.
#umask 022

# if running bash
if [ -n "$BASH_VERSION" ]; then
    # include .bashrc if it exists
    if [ -f "$HOME/.bashrc" ]; then
	. "$HOME/.bashrc"
    fi
fi

# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi

# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/.local/bin" ] ; then
    PATH="$HOME/.local/bin:$PATH"
fi

xrandr --newmode "1920x1080_60.00"  173.00  1920 2048 2248 2576  1080 1083 1088 1120 -hsync +vsync
xrandr --addmode Virtual1 "1920x1080_60.00"
```
# Fim

![tumblr_inline_p9ggi9Xp4W1qgcvsy_500](https://user-images.githubusercontent.com/59977779/125785589-2f000580-a14c-4bc2-98c0-2fe72681303f.gif)

