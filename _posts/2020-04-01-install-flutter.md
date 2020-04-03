---
layout: post
title:  "Install and Setting up Flutter Devel"
date:   2020-04-01 19:18:00
categories: Flutter
published: true
comments: true
---

# Installing Flutter to write APPs on Linux

![Flutter logo](/assets/flutter_logo.png "Flutter logo")

## Do you know how to use flutter on Linux?

- If your answer is I don't, no problem. More details about Flutter at https://flutter.dev 

- In the future, I'll present some examples, but for now, let's set up our devel environment on Linux

- In this post we'll learn how to install all basic requirements to write your APPs using Flutter on Linux, this include:
    - Install Flutter SDK
    - Install Android SDK
    - How to use sdkmanager tool to install Android platforms-tools
    - Setting up Visual Code to Flutter and Dart that is the programming language

## STEP 0: Install Flutter

- Install flutter from the website, in this case, go to https://flutter.dev/docs/get-started/install/linux , there you find all system requirements, e.g., disk space 600 MB, but personally I rather 2 GB, this because of the additional libraries and IDE. Thus, let's start.

- Create a directory to save the files to install Flutter:

```console
foo@bar:~$ mkdir ~/development
foo@bar:~$ cd ~/development
foo@bar:development/$ wget https://storage.googleapis.com/flutter_infra/releases/stable/linux/flutter_linux_v1.12.13+hotfix.7-stable.tar.xz 
foo@bar:development/$ tar xf flutter_linux_v1.12.13+hotfix.9-stable.tar.xz
# In this point we have
foo@bar:development/$ ls
flutter
```

### Update your path

You can update your PATH variable for the current session at the command line, but You’ll probably want to update this variable permanently, so you can run flutter commands in any terminal session, this way try:

- Determine the directory where you placed the Flutter SDK
```console
foo@bar:development/$ cd flutter
foo@bar:development/flutter/$ pwd
/home/foo/development/flutter/
```

- Open (or create) the rc file for your shell. For example, Linux uses the Bash shell by default, so edit $HOME/.bashrc. If you are using a different shell, the file path and filename will be different on your machine.

- Add the following line in your $HOME/.bashrc:
```console
export PATH="$PATH:/home/foo/development/flutter/bin"
```

**NOTE:** the PATH **/home/foo/development/flutter/** should be replaced by your path, so in this case **foo** is your Linux user.

- Run source $HOME/.<rc file> to refresh the current window or open a new terminal window to automatically source the file.

- Verify that the flutter/bin directory is now in your PATH by running:

```console
foo@bar:~$ cd ~/development
foo@bar:development/$ echo $PATH
# Verify that the flutter command is available by running:
foo@bar:development/$ which flutter
```

- If every it's OKAY, let's try some commands with Flutter SDK:

```console
foo@bar:~$ cd ~/development
foo@bar:development/$ flutter precache
foo@bar:development/$ flutter doctor
[-] Android toolchain - develop for Android devices
    • Android SDK at /Users/obiwan/Library/Android/sdk
    ✗ Android SDK is missing command line tools; download from https://goo.gl/XxQghQ
    • Try re-installing or updating your Android SDK,
      visit https://flutter.dev/setup/#android-setup for detailed instructions.

```

- Run the last command to see if there are any dependencies you need to install to complete the setup (for verbose output, add the -v flag). 

## STEP 1: Install JAVA

- In case you have Java already installed on your computer, I would suggest you jump to the next step, in other cases let's install Java 8. 

- Why Java 8, the new java version, e.g., 10 and 11 has some issues with Flutter checkout https://github.com/flutter/flutter/issues/25811

- Install on Ubuntu:
```console
foo@bar:development/$ sudo apt install openjdk-8-jdk
```

- Install on Fedora:
```console
# JRE
foo@bar:development/$ sudo dnf install java-1.8.0-openjdk
# JDK
foo@bar:development/$ sudo dnf install java-1.8.0-openjdk-devel
```

### Managing Java

In case, you have other java versions installed, in another way you can jump to the next step. You can configure which version is the default for use on the command line by using the update-alternatives command.

```console
foo@bar:development/$ sudo update-alternatives --config java
```

- You can do this for other Java commands, such as the compiler (javac):

```console
foo@bar:development/$ sudo update-alternatives --config javac
```

## STEP 2: Install Android SDK 

- One easy way to install the Android SDK is to install Android Studio, see https://developer.android.com/studio , but in this post, our focus is to adopt the Visual Code to write our Flutter APPs.

- Therefore, we choose to install only the Android SDK, this way you can go to https://developer.android.com/studio in the section Command line tools only and get the Linux version. **Unfortunately**, we have noted some issues with the latest versions. This way, adopt a specific version of the Android SDK from Google repo:

```console
# NOTE: at this moment, we are inside the development directory
foo@bar:development/$ wget https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip
foo@bar:development/$ unzip sdk-tools-linux-4333796.zip 
foo@bar:development/$ cd tools/bin/ 
foo@bar:development/tools/bin/$ 
```

- Now we'll install some tools to run our Flutter APPs on Android, e.g., the emulator, OS version and libraries. Thus, we'll use the sdkmanager tool. This step can take a little time according to your internet speed.

```console
foo@bar:development/tools/bin/$ ./sdkmanager "tools" "build-tools;29.0.3" "emulator" "platform-tools" "platforms;android-29" "system-images;android-29;google_apis_playstore;x86_64"
```

**NOTE:** At this moment, it's possible to get some issues to break the Android SDK installation, one example of common issues and solution, you can try and repeat the install:

- No space left on device, details at https://bytefreaks.net/applications/android-studio-no-space-left-on-device , **SOLUTION**:

```console
foo@bar:development/tools/bin/$ sudo mount -o remount,size=8G,noatime /tmp;
```

- **OPTIONAL:** This is optional, but highly recommended, to confirm all licenses from Android SDK.

```console
foo@bar:development/tools/bin/$ ./sdkmanager --licenses
```

### Install Android Debug Bridge (adb)

- Android Debug Bridge (adb) is a versatile command-line tool that lets you communicate with a device. The adb command facilitates a variety of device actions, such as installing and debugging apps, and it provides access to a Unix shell that you can use to run a variety of commands on a device. More details at https://developer.android.com/studio/command-line/adb

- Install on Ubuntu:

```console
foo@bar:development/tools/bin/$ sudo apt-get install android-tools-adb 
```

- Install on Fedora:

```console
foo@bar:development/tools/bin/$ sudo dnf install adb 
```

## STEP 3: Update your path with the Android SDK 

- Add the following line in your $HOME/.bashrc:

```console
ANDROID_HOME=/home/foo/development/tools

export PATH=$PATH:$ANDROID_HOME:$ANDROID_HOME:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools
```

- Now to check if Flutter see Android SDK
```console
foo@bar:development/tools/bin/$ flutter doctor -v
```

## STEP 4: Install Flutter plugin on Visual Code

- Opening Visual Code and go to "Extensions" or Ctrl+Shift+X, then in Search look for Flutter and click and install, as follows:

![Flutter plugin VS](/assets/flutter_plugin_vs.png "Flutter plugin VS")

- Install Dart plugin on VS still in "Extensions" on Visual Code, for Dart and click and install, as follows:

![Dart plugin VS](/assets/dart_plugin_vs.png "Dart plugin VS")

- We are all ready to write our Flutter APPs using Visual Code on Linux

## STEP 5: Create a Hello World APP in Flutter

- In the future, I'll explain in detail the code but for now, we focus on how to run a Flutter APP in our devel environment.

- Let's create a directory (inside development) to organize our APP

```console
foo@bar:development/tools/bin/$ cd ../../
foo@bar:development/$ mkdir hello_app 
foo@bar:development/$ cd hello_app
foo@bar:development/$ flutter create .
Creating project .... androidx: true
  android/build.gradle (created)
  android/app/build.gradle (created)
  android/app/src/main/kotlin/com/example/hello_app/MainActivity.kt (created)
  android/hello_app_android.iml (created)
  lib/main.dart (created)
  ...
  ios/Runner.xcodeproj/project.xcworkspace/contents.xcworkspacedata (created)
  .metadata (created)
  hello_app.iml (created)
Running "flutter pub get" in hello_app...                           4.0s
Wrote 77 files.
...

In order to run your application, type:

  $ cd .
  $ flutter run

Your application code is in ./lib/main.dart.
```

- Opening the source code in the Visual Code, you need to go in the menu File -> Open Folder

**That's all folks**.