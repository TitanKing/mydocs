## KDE 5.5+ Tweaks ##

I find KDE to provide the best experience for a desktop environment. There are a few things that irk me. For instance the fact that GTK (Gnome) applications looks so much different with missing icons and ugly none universal looks. There are a few ways to fix it:

## Font

For the default UI use [San Francisco](https://github.com/supermarin/YosemiteSanFranciscoFont)

For mono font use Monaco.

## Repo improvements

For a list of later packages than that of the default repo install:
`sudo apt-add-repository ppa:nilarimogard/webupd8`

It includes updates to [See Here](https://launchpad.net/~nilarimogard/+archive/ubuntu/webupd8)

## Media Players

I found Clementine to be the best by far, install from native repo:

`sudo add-apt-repository ppa:me-davidsansome/clementine`

## Fixes

### Vsync issues

```
export __GL_YIELD="USLEEP"
export KWIN_TRIPLE_BUFFER=0
export KWIN_USE_BUFFER_AGE=0
```

Add these lines to etc/profile.d/kwin.sh

### Latest Nvidia Drivers

[Graphics Drivers Nvidia](https://launchpad.net/~graphics-drivers/+archive/ubuntu/ppa)
[Graphics Drivers Intel](https://01.org/linuxgraphics/downloads)
