## Tweaks ##

### Theme ###

##### Beautiful flat theme for general usage #####

https://github.com/LinxGem33/OSX-Arc-White

### Remove pesky evolution services ###

    sudo chmod -x /usr/lib/evolution/evolution-calendar-factory
    sudo chmod -x /usr/lib/evolution/evolution-addressbook-factory
    sudo chmod -x /usr/lib/evolution/evolution-source-registry
    
### To remove existing online accounts: (Incase of continues popups) ###

    rm -rfv ~/.config/evolution/sources/*

## Install GNOME 3.22 ##

    sudo add-apt-repository ppa:gnome3-team/gnome3-staging
    sudo add-apt-repository ppa:gnome3-team/gnome3
    sudo apt update
    sudo apt dist-upgrade
    sudo apt install ubuntu-gnome-desktop

## To uninstall GNOME 3.22 from Ubuntu Systems, run the commands given below: ##

    sudo apt-get install ppa-purge
    ppa-purge ppa:gnome3-team/gnome3-staging
    sudo apt-get update
    