## React Native ##


## Setting Up React Native ##

    // Todo

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

### Alternative debugging ###

Inside your dev console, run `react-native android-log` all console.logs etc will be output there.

### Linking react native packages ###

React native link allows you to link native code libraries with react native. Each library could have its own linking instructions, see [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) for an example of a linked library.

    react-native link

### Cleaning up and reinstalling ###

Sometimes things goes wrong and you feel it just should work. There are many issues that could cause this, in some cases the only way to fix this is to re-install and clear the cache;

    watchman watch-del-all
    rm -rf node_modules && npm install
    react-native link
    npm start -- --reset-cache
