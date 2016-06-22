## KDE 5.5+ Tweaks ##
I find KDE to provide the best experience for a desktop environment. There are a few things that irk me. For instance the fact that GTK (Gnome) applications looks so much different with missing icons and ugly none universal looks. There are a few ways to fix it:

## Oxygen theme
Install the oxygen theme:  
`sudo apt-get install kdeartwork-theme-icon gtk3-engines-oxygen kde-config-gtk-style`

From here in your application style settings (KDE) you can now choose oxygen as both the kde and gnome theme.

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