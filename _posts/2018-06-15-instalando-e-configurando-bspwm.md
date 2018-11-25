---
layout: post
title:  "Instalando e configurando o bspwm"
date:   2018-06-15
description: "Bspwm é um gerenciador de janelas do tipo tiling. Na minha opinião, um dos melhores WM.
Sua configuração é simples, sem nenhuma complicação."
author: 'Mashn'
tags: bspwm
---

Bspwm é um gerenciador de janelas do tipo tiling. Na minha opinião, um dos melhores WM. Sua configuração é simples, sem nenhuma complicação. Este tutorial assume que você já tem o X11 instalado.

Iremos utilizar os seguintes pacotes para deixá-lo funcional:

- bspwm
- sxhkd
- xsetroot (também chamado de xorg-xsetroot em algumas distros)
- st (ou qualquer outro terminal)

Vou me basear na distribuição Void Linux para descrever os passos, já que é a distro que uso.

## Instalação

1. Instalando os pacotes necessários:

```sh
$ xbps-install bspwm sxhkd xsetroot st
```

2. Copiando os arquivos de configuração.

Se você não tem o diretório .config já criado, agora é hora de criá-lo. Tenha certeza de não estar como root nesta parte. Nós também iremos copiar as configs de exemplo do bspwm e sxhkd.

```sh
$ mkdir -p ~/.config/{bspwm,sxhkd}
$ cp /usr/share/doc/bspwm/examples/bspwmrc ~/.config/bspwm
$ cp /usr/share/doc/bspwm/examples/sxhkdrc ~/.config/sxhkd
```

Agora que o bspwm já está instalado, vamos fazer alguns ajustes.

3. Finalizando.

Alguns WM, incluindo o bspwm, não inicia o cursor corretamente. Para resolver isso, faça com que o xsetroot inicie junto com o bspwm, adicionando a seguinte linha no arquivo bspwmrc:

> xsetroot -cursor_name left_ptr &

No arquivo sxhkdrc, temos a seguinte configuração:

```sh
super + Return
urxvt
```

Como podem ver, super + Return inicia o terminal, que no caso é o urxvt-unicode. Podemos mudar para o terminal que instalamos, o st.

```sh
super + Return
st
```

E para finalizar, adicione esta linha no arquivo `~/.xinitrc`.

```sh
exec bspwm
```

Após isso, você já tem seu bspwm pronto para uso.

## Configuração

4. Entendendo como funciona sua config:

```sh
#!/bin/sh

sxhkd &
(Os serviços que quiser que inicie junto com o WM, podem ser incluídos aqui.)

bspc monitor -d I II III IV V VI VII VIII IX X
(O nome das workspaces, pode renomear como quiser cada um deles)

bspc config border_width 2
bspc config window_gap 12
bspc config split_ratio 0.52
bspc config borderless_monocle true
bspc config gapless_monocle true
(Aqui vem as configurações das bordas e gaps.)

bspc rule -a Gimp desktop=’^8’ state=floating follow=on
bspc rule -a Chromium desktop=’^2’
bspc rule -a mplayer2 state=floating bspc rule -a
Kupfer.py focus=on bspc rule -a Screenkey manage=off
(Regras para as janelas. É aqui que se define em qual workspace a janela será aberta, e o comportamento da mesma.)
```

Podemos adicionar algumas configurações extras, como:

```sh
bspc config focus_follows_pointer true
(O foco da janela segue o cursor.)

bspc config normal_border_color "#528588"
bspc config focused_border_color "#dee3e0"
bspc config presel_feedback_color “#2c3939”
(Cores.)
```

5. Regras.

As regras podem ser confusas para alguns, então irei explicar seu funcionamento.
Para definir uma regra para uma janela, você precisa saber o nome da sua classe, para descobrir isso, podemos usar o pacote xprop:

```sh
$ xprop | awk '/WM_CLASS/{print $4}'
```

Após rodar o comando, clique na janela que deseja saber a classe.

Tendo o nome da sua classe, podemos começar a criar nossa regra. Vamos pegar o terminal st de exemplo:

```sh
bspc rule -a st-256color desktop=‘^1’
```

No exemplo acima, o terminal st irá abrir no desktop 1.
Vamos continuar…

```sh
bspc rule -a st-256color desktop=‘^1’ follow=on focus=on
```

Uma coisa interessante do bspwm, é este “follow=on”, que se você estiver em um desktop diferente do 1, ela irá te levar até o 1.
Já o “focus=on”, irá focar na janela, caso tenha várias janelas abertas no mesmo desktop.

Também podemos adicionar “center=true”, para um programa com a regra floating abrir no centro da tela.

6.  Perguntas frequentes:
P: Após abrir o bspwm vejo apenas uma tela preta, fiz algo de errado?
R: Não. O bspwm por padrão não vem com barra, então a tela inicial é um fundo preto.
P: Quais barras posso usar?
R: Praticamente todas as barras são compatíveis com o bspwm, as que posso recomendar são: Polybar, lemonbar e tint2.

P: Não estou conseguindo abrir nada aqui, o que faço?
R: Os comandos básicos são:
super + enter = Abre o terminal
super + alt + esc = Sai do wm
super + w = Fecha a janela
super + 1,2,3,4… = Vai para os outros desktops

Você encontra todos os atalhos no arquivo sxhdrc.

Para mais detalhes:
- [https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies](https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies)
- [https://wiki.archlinux.org/index.php/Bspwm](https://wiki.archlinux.org/index.php/Bspwm)
- [https://wiki.voidlinux.eu/Bspwm](https://wiki.voidlinux.eu/Bspwm)
- [https://www.reddit.com/r/bspwm/](https://www.reddit.com/r/bspwm/)
