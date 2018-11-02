Install Specific Package Version using Brew
1. Search available versions
`brew search <package name>`
2. Install the selected version
`brew install <package name>@<version>`
3. If you already have the other version of package, unlink the package.
`brew unlink <package name>`
4. Link the selected version
`brew link <package name>@<version>`


ImportError: MagickWand shared library not found. 
```
$ brew install imagemagick@6
$ export MAGICK_HOME=/usr/local/opt/imagemagick@6
```
Safari.app cannot be updated because its extensions are in use by Spotlight.app. 
In terminal, `killall Spotlight` to terminate spotlight application

The notification ceneter did not work. In terminal,
`launchctl load -w /System/Library/LaunchAgents/com.apple.notificationcenterui.plist killall NotificationCenter`

Error when install gcc using brew
`brew install gcc`
```
xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
Error: Failure while executing; `git config --local --replace-all homebrew.analyticsmessage true` exited with 1.
xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
Error: Failure while executing; `git config --local --replace-all homebrew.private true` exited with 1.
```
`sudo xcode-select --install`
`sudo xcode-select --switch /Applications/Xcode.app`