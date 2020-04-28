---
layout: post
title:  "Project Flutter A to Z"
date:   2020-04-27 18:00:00
categories: Flutter
published: true
comments: true
---

# Project Flutter A to Z

![Flutter logo](/assets/flutter_logo.png "Flutter logo")

## Keep Watching

I've been writing some APPs examples using **Flutter CI/CD** adopting GitHub actions. The steps of the main flow of the project are: 
- Adopting GitHub as version control from the source code project, thus each commit on branch master is analyzed using flutter analyze
- Running the tests, including widget tests and unit testing
- The results of the tests are then sent to CodeCov (https://codecov.io/) service to analyze the code coverage
- All previously items are done, then the App APK is built in the GitHub repository generating the draft release
- Finally, adopting the GitHub actions, the App is deployed in the GitHub pages using Flutter Web

**Checking out the project**: https://github.com/hbgit/flutter_a_z


![Flutter Project](/assets/flutter_pub.png "Flutter Project")