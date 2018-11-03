**Error when installing package in R on macOS**
```
make: gfortran: No such file or directory
...
Warning in install.packages :
  installation of package 'fpp2' had non-zero exit status
```
1. In terminal, `brew install gcc` (Check `MacOS.md` if failed)
2. In R, `install.packages("forecast")`  

`make: /usr/local/clang4/bin/clang: No such file or directory` in MacOS
1. Go to https://github.com/coatless/r-macos-clang
2. Download `clang4-r-1.3.1.pkg`
3. In terminal, `xcode-select --install` to install CLI. (If there is some issue when install through terminal, can go to apple developer website to download `.pkg` to install)

`/usr/local/clang4/bin/../include/c++/v1/math.h:301:15: fatal error: 'math.h' file not found`
For Xcode >= 10 and MacOS >=10.14, in terminal, `open /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg` 
