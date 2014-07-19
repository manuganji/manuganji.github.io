---
layout: post
title: Signing Phonegap apps for Google Play
description: ""
categories: phonegap
tags: [phonegap, google play, signing, build]
---
* Run `phonegap build android` from the folder containing `www` folder
* `cd` to this path `platforms/android/`
* Make sure `ant.properties` in this folder contains these keys and right values
> key.store=<absolute_path_to_keystore_file_on_disk>
>
> key.alias=<alias_value>
>
> key.store.password=<store_password>
>
> key.alias.password=<alias_password>
* increment the `versionCode` in `AndroidManifest.xml` in this folder
* `cd` to `ant-build` folder from this folder
* run `./build --release` in this folder. 

Now you have a bunch of .apk files in this folder. The one with the name `<Project_Name>-release.apk` is what you can upload to Google play.

References:

1. [Stack Overflow answer about how to build a release from a phonegap app](http://stackoverflow.com/a/20792218/1218897)
2. [Stack Overflow answer about how to specify your developer signature in a properties file](http://stackoverflow.com/a/14765511/1218897)
3. [About versionCode param in PhoneGap community forums](http://community.phonegap.com/nitobi/topics/my_version_code_for_android_isnt_changing_when_i_update_my_phonegap_app)
