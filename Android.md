# Android and Mobile Development Environment #

This guide will not help all but focuses those who come from an Linux and Web Application development environment. My mission is to get the android environment up and running while discussing a few options of what frameworks is available.

## Getting the basic environment up in Ubuntu 16.04 ##

The following runtime libraries will most likely be needed.

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

    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
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

### Android Studio ###

    sudo dpkg --add-architecture i386
    sudo apt-get update
    sudo apt-get install libz1 libncurses5 libbz2-1.0:i386 libstdc++6

1. [Download Studio](https://developer.android.com/studio/index.html)
2. Unzip studio to a location where you would like to run it from.
3. Look for the executable in the /bin directory.

### Android SDK ###

Once Android Studio runs it will install the SDK basics but we are not quite done, you may want to install more packages using the SDK manager UI by running the Manager from within the SDK directory:

    ./Android/Sdk/tools/android

The manager will allow you to install Android API versions and Images.

#### Creating a local Virtual Device for testing ###

Run the SDK manager with:

    ./Android/Sdk/tools/android

Download a usable image for testing, lets download a common fast one so can build a AVD (Android Virtual Device) for testing;

1. Open the Android 4.22 (API 17) dropdown and install the Intel x86 Atom System Image.
2. Click Tools -> Manage AVDs and create a AVD with the above image.
3. Now you can start the ADV

NOTE: This will not start if Virtualbox is running.

### Testing on Android Device ###

We first need some drivers and basic systems to get this going install:

    sudo apt-get install android-tools-adb android-tools-fastboot

1. Next enable Developer Mode (If no such option click in About Phone in setting multiple times until it is enabled)
2. From Developer Options enable USB Debugging
3. Plug phone into computer.

Now see if device is listed:

    adb devices

If there is an item listed you are good to go and ready to test.

### End of setting up development environment.
--------------------------------------------------------

# Development Environment #

Here is a setup of environments I found to be worthwhile putting effort in, the setup of those and how it can contribute to mobile development.

### The final list of best cross platform environments ###

## React Native ##

Build on Facebooks React framework is fast, is basically native and good for apps you start from scratch. Much steeper learning curve, to achieve a real slick native interface and eventually fast development. Code mostly in JS ES6 with a lot of new terminology.

1. Very fast.
2. Native fallback (java etc.)
3. Good documentation.
4. Harder to get running.

## Setting Up React Native ##

First of all this could be quite frustrating, but keep at it, once it is running... well that is not entirely true.

1. Was installed? If not install android studio and update android sdk via it (as above),
https://developer.android.com/studio/index.html#downloads

2. Add PATH in `~/.bashrc`

    export JAVA_HOME=/usr/lib/jvm/java-8-oracle
    export ANDROID_HOME=~/Android/Sdk
    export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools


3. Run `source ~/.bashrc` to refresh changes to .bashrc

4. Put the `local.properties` file inside of `project_name/android/` folder.

5. Edit `local.properties` then add `sdk.dir=/home/your_home_dir/Android/Sdk` in it.

6. Run `android` command to update/install required packages.
For RN 0.32, its
  * tools/sdk build tools 23.0.1
  * Android 5.1.1 (API 22)
  * Extras
    * Android Support Repository

6. Run android studio or `android avd` command to open and start an emulator
7. Now from the project folder run `react-native run-android`
8. Once you seen app's red screen in android, do `react-native start` to trigger the bridge server.

## Watchmen ##

Watchman is a tool by Facebook for watching changes in the filesystem. It is highly recommended you install it for better performance, but it's alright to skip this if you find the process to be tedious.

1. mkdir watchman
2. cd watchman
3. git clone https://github.com/facebook/watchman.git
4. cd watchman
5. git checkout v4.7.0
6. ./autogen.sh
7. ./configure
8. ./make
9. make
10. sudo checkinstall

That is about it, your live updates should now work.

NOTE: The reason why one would want to install it is because you can enable live reloading, meaning you every change to the system is seen live on the screen.


### Alternative Android Emulator ###

If you find android virtual device to be a bit unstable there is a product called [genymotion](http://www.genymotion.com) that is free for personal use. It is easier to get going with more options to chose from.

### Starting Development Environment ###

Assuming you created a React Native project and the setup steps are completed, you should now be ready to start your environment up, many times your machine might need to be rebooted.

1. Start up your android virtual machine (genymotion or avd).
2. Run `react-native start` to start the packager.
3. Browse to your RN project and run `react-native run-android`
4. You should now see a screen with your application inside the emulator. Open the menu (Ctrl + M) to view and enable the developers options.
5. Start live debugging in chrome by pressing (Ctrl + M) in the emulator and selecting Debug JS Remotely.

### Issues with remote debugging ###

I had issues with remote debugging in Chrome where the debugger would only send once and then after saving would start searching for the debugger.

**Before you go this route**

**IMPORTANT NOTE:** If you are using Chrome - at the time of testing Chrome gave issues with debugging but Chromium worked fine. Chances are good that below would not even be needed.

Here is what I did to resolve this:
1. I ended up using Genymotion.
2. In Genymotion set the Network Mode to bridge for the virtual device.
3. Start up the android emulation development environment (`emulator, react-native start, react-native run-android` last step can also be skipped if you execute the app directly from emulator).
4. From the Emulator (Ctrl + M / Shake Device) go to Dev Settings and set the Debug and Server host to your local development machines (not android) IP, eg. `10.0.0.100:8081`
5. Now in Google Chrome open the debug url manually as `http://10.0.0.100:8081/debugger-ui`
6. Now you are ready to go into the Emulator your apps settings (Ctrl + M / Shake Device) and turn on Remote JS Debugger.

### Alternative debugging ###

Inside any console for example the terminal in PHPSTorm or your machines terminal, run `react-native android-log` all console.logss etc will be output there.

#### End of React Native ####
---------------------------------------------------


## Cordova ##

Cordova from Apache is a web wrapper, a fast one. It allows really fast development and no learning curve as you develop and call native APIs through normal HTML5, Javascript (jquery etc) and CSS on the framework you chose. It comes with a host of front-end frameworks to make things look and feel great.

#### Front-end frameworks include ####

- Iconic
- Jquery Mobile
- and many more...



