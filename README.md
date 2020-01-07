## Overview
The goal of this is to produce a native crash that gets captured / sent as event to Sentry.

This project is a demo implementation of **sentry-native**, the Sentry SDK for Native Crash Reporting which you can download here https://github.com/getsentry/sentry-native as a distribution zip for use in Production. This project uses it in its pakcaged release form - it is referenced as a submodule.

**Official Sentry Documentation**  
Use https://github.com/getsentry/sentry-native when ready to implement this in your real code.

## Setup
### Versions
*sentry-native v0.1.4*  
*sentry-cli 1.49.0z*  
*macOS Mojave 10.14.4*  
*See windows.txt for Windows*


#### sentry-cli
1. `yarn global add @sentry/cli`. You can also get it from https://github.com/getsentry/sentry-cli/releases/ or https://docs.sentry.io/cli/installation/


#### Mac
1. `git clone --recurse-submodules git@github.com:sentry-demos/sentry-native.git`
2. `make bin/example`
3. `make setup_release`
4. `make upload_debug_files`
5. `make run_crash` or `make run_message`

You can also run all of them at once sequentially:  
`make clean bin/example setup_release upload_debug_files run_crash`

`make clean` if you need to re-run `make bin/example` and upload new debug files.

## Technical Notes
### What's Happening
`make bin/example` creates debug symbols and executables  

`make setup_release` creates a Sentry Release and associates git commits

`make upload_debug_files` uploads your symbols to Project Settings > Debug Files https://sentry.io/settings/${YOUR_ORG}/projects/${PROJECT}/debug-symbols/  

`make run_crash` causes a native crash in *src/example.c*. It sends one event to Sentry

`make run_message` causes a Sentry Message to get sent as an event to Sentry.

`make clean` is for re-generating debug symbols and executables


### Updating sentry-native
WARNING - this demo app was tested with sentry-native v0.1.4. It is only intended to work with v0.1.4. If you leave v0.1.4 it is not guaranteed to work. 
```
git submodule update
```

## Troubleshooting
If your events are not symbolicated then run `make clean` and re-run commands from step 1

Try running the `make` commands one-by-one because if you run all at once and one of them has a problem, it won't halt execution of the following commands.

You need to always run `bin/example` before `setup_release`

If the standalone distribution package doesn't fit your needs, then go to https://github.com/getsentry/sentry-native#development

sentry-native in the news https://blog.sentry.io/2019/09/26/fixing-native-apps-with-sentry

## Gif
![gif](screenshots/sentry-native-2-events-150.gif)
