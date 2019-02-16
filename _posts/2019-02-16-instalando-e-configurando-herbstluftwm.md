---
layout: post
title:  "Instalando e configurando o herbstluftwm"
date:   2019-02-16
description: "Herbstluftwm é um gerenciador de janelas do tipo tiling, bem completo.
Fácil de configurar, sem nenhuma complicação."
author: 'yaszu'
tags: herbstluftwm
---

Herbstluftwm é um gerenciador de janelas para X11 usando Xlib e Glib. Este tutorial assume que você já tem o X11 instalado.

Irei me basear na distro yalos para descrever os passos, já que é a distro que uso.

## Instalação

1. Instalando os pacotes necessários:

```sh
$ yap -i herbstluftwm
$ yap -i dzen2(Apenas se você quiser usar a barra padrão que vem com ele)
```

2. Copiando os arquivos de configuração.

Se você não tem o diretório .config já criado, agora é hora de criá-lo. Tenha certeza de não estar como root nesta parte. Nós também iremos copiar as configs de exemplo do bspwm e sxhkd.

```sh
$ mkdir -p ~/.config/herbstluftwm
$ cp /etc/xdg/herbstluftwm/autostart ~/.config/herbstluftwm/
```

Para usar a barra padrão que vem com o Herbstluftwm:

```sh
cp /etc/xdg/herbstluftwm/panel.sh ~/.config/herbstluftwm/
```

Agora que o herbstluftwm já está instalado, vamos fazer alguns ajustes.

3. Finalizando.

O arquivo ~/.config/herbstluftwm/autostart é onde todas as suas configurações do herbstluftwm irão ficar, desde a aparência, até os atalhos. Primeiramente iremos modificar os atalhos.

Escolha sua tecla Mod antes de tudo, na linha 17 como podemos ver está Mod=Mod1 que é o alt. Eu irei mudar para a tecla super(mais conhecida como tecla windows).

```sh
Mod=Mod4
```

Como podem ver na linha 24 Mod+Return inicia o terminal, que no caso é o xterm, mude para o terminal que você usa. Irei usar o st como exemplo por ser o que uso.

```sh
hc keybind $Mod-Return spawm ${TERMINAL:-st}
```
E para finalizar, adicione esta linha no arquivo `~/.xinitrc`.

```sh
exec herbstluftwm
```

Após isso, você já tem seu herbstluftwm pronto para uso. Quando aplicar alguma configuração, é só digitar herbstclient reload no terminal que ele recarrega e aplica as novas configurações.

## Configuração

4. Entendendo como funciona sua config:

```sh
tag_names=( {1..9} ) (Nome dos workspaces, pode colocar o nome que quiser.)

hc attr theme.border_width 3
hc attr theme.active.color '#9fbc00'
hc attr theme.normal.color '#454535'
hc set window_gap 0
(Configurações de bordas e gap entre janelas)
```

Podemos adicionar algumas configurações extras, como:

```sh
hc pad 0 60 60 60 60
(Espaço morto entre as janelas e os cantos da tela)
```

6.  Perguntas frequentes:
P: Após abrir o herbstluft vejo apenas uma tela sólida, fiz algo de errado?
R: Se não está usando a bar padrão dele, não.
P: Quais barras posso usar?
R: Praticamente todas as barras são compatíveis, as que posso recomendar são: dzen, lemonbar e tint2.

P: Não estou conseguindo abrir nada aqui, o que faço?
R: Os comandos básicos são:
Mod + return = Abre o terminal
Mod + shift + c = Fecha a janela
Mod + 1,2,3,4… = Vai para os outros desktops

Você encontra todos os atalhos no ~/.config/herbstluftwm/autostart.

Para mais detalhes:
- [https://herbstluftwm.org/tutorial.html](https://herbstluftwm.org/tutorial.html)
- [https://herbstluftwm.org/herbstluftwm.html](https://herbstluftwm.org/herbstluftwm.html)
- [https://herbstluftwm.org/herbstclient.html](https://herbstluftwm.org/herbstclient.html)
- [https://herbstluftwm.org/faq.html](https://herbstluftwm.org/faq.html)
- [https://wiki.archlinux.org/index.php/Herbstluftwm](https://wiki.archlinux.org/index.php/Herbstluftwm)
