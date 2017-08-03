# Android and Mobile Development Environment #

Setup local android and emulation environment running on Ubuntu.

The following runtime libraries will most likely be needed;

1. Oracle Java
2. Node.js
3. NPM
4. Android Studio
5. Android SDK (Android Studio Installs this...)

### Oracle JDK ###

You may first need to remove the open source version of java (OpenJDK):

    sudo apt-get purge openjdk*

Now we are ready to install;

    sudo apt-get install python-software-properties
    sudo add-apt-repository ppa:webupd8team/java
    sudo apt-get update

We will install latest Oracle Java JDK

    sudo apt-get install oracle-java8-installer

Setup the JAVA_HOME var:

    export JAVA_HOME=/usr/lib/jvm/java-8-oracle

Reboot and check with with `java -version` if the correct version of Java is now running.

### Node.js ###

    curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
    sudo apt-get install -y nodejs
    sudo apt-get install -y build-essential

### NPM ###

(Node Package Manager)

    sudo apt-get install -y npm

Check for outdated packages with:

    sudo npm outdated -g --depth=0


### See if everything is installed so far ###

    java -version
    node -v
    npm -v

### npm-check ###

Nice module to check all dependencies and newer versions of packages in your local npm package file.

// Some other useful commands:

    npm-check // Identify unused and dated packages.
    npm uninstall <module> --save
    npm install <module> --save
    npm install <module> --save // for development dependencies
    npm outdated // Will check for for outdated packages
    npm update --save <module>@1.0.0 // for latest...

### Android Studio ###

    sudo dpkg --add-architecture i386
    sudo apt-get update
    sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 libbz2-1.0:i386

1. [Download Studio](https://developer.android.com/studio/index.html)
2. Unzip studio to a location where you would like to run it from eg. ~/Applications/android-studio.
3. Look for the executable in the /bin directory.

### Android SDK ###

Once Android Studio runs it will install the SDK basics but we are not quite done, you may want to install more packages using the SDK manager UI by running the Manager from within within Android Studio.

The manager will allow you to install Android API versions and Images, however you need to install SDK tools. Install the following tools as bare minimum from Android Update Manager; 

1. Android SDK Build Tools
2. Android SDK Platform Tools
3. Android SDK Tools

Note that you do not have to download a android image as we will be running an image downloaded from the genymotion repo.

# Continued Development Configuration #

Here are the final touches to the android and java environments to make it run as expected;

1. Was Android Studio installed? If not install Android Studio and update android sdk via it (as above),
https://developer.android.com/studio/index.html#downloads

2. Add PATH in `~/.bashrc`

    export JAVA_HOME=/usr/lib/jvm/java-8-oracle
    export ANDROID_HOME=~/Android/Sdk
    export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools


3. Run `source ~/.bashrc` to refresh changes to .bashrc

4. Put the `local.properties` file inside of `project_name/android/` folder.

5. Edit `local.properties` then add `sdk.dir=/home/your_home_dir/Android/Sdk` in it.

## Watchmen ##

Watchman is a tool by Facebook for watching changes in the filesystem. It is highly recommended you install it for better performance, but it's alright to skip this if you find the process to be tedious.

[Installing Watchman](https://facebook.github.io/watchman/docs/install.html)

That is about it, your live updates should now work.

NOTE: The reason why one would want to install it is because you can enable live reloading, meaning you every change to the system is seen live on the screen.

# Android Emulator #

If you find your android virtual machine to be a bit unstable or complext to get running, there is a product called [genymotion](https://www.genymotion.com/download/) that is free for personal use. It is easier to get going with more options to chose from.

# Testing directly on Android device #

We first need some drivers and basic systems to get this going install:

    sudo apt-get install android-tools-adb android-tools-fastboot

1. Next enable Developer Mode (If no such option click in About Phone in setting multiple times until it is enabled)
2. From Developer Options enable USB Debugging
3. Plug phone into computer.

Now see if device is listed:

    adb devices

If there is an item listed you are good to go and ready to test.

# Hack Android #

## Bootloader ##
Assuming your device adheres to some Android standards, you'd want to run `fastboot oem device-info`.

Often you can also run `fastboot reboot-bootloader` to get into the bootloader which often says right there on screen whether it's locked or not.

## Alternative ##
Check if bootloader is unlocked:
An alternative method that may have mixed results:

Open your device’s dialer
Dial `*#*#7378423#*#*` and it will automatically open a new window if it works
Now in that window go to Service Info > Configuration
You ought to see one of these:

Bootloader unlock allowed - Yes (Bootloader is Locked)

Bootloader Unlocked - Yes (Bootloader is unlocked)

