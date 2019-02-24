# cminer

Now can only mine using CPU.

## Usage

The **cminer** is a command line program. This means you launch it
from a Windows/Linux/Macos console, or create shortcuts to
predefined command lines using a Linux/Macos Bash script or Windows batch/cmd file.
For a full list of available command, please run:

```sh
cminer --help
```

### How to connecting to pools

./cminer -P http://user[.workername][:password]@hostname:port[/ADDRESS/HOST_ID]


## Build

### Building from source

- #### Common

1. [CMake] >= 3.5
2. [Git](https://git-scm.com/downloads)
3. [Perl](https://www.perl.org/get.html), needed to build OpenSSL

- #### Linux

   1. GCC version >= 4.9

- #### macOS

1. GCC version >= TBF

- #### Windows

1. [Visual Studio 2017](https://www.visualstudio.com/downloads/); Community Edition works fine. **Make sure you install MSVC 2015 toolkit (v140).**

### Instructions

1. Create a build directory:

    ```shell
    mkdir build
    cd build
    ```

2. Configure the project with CMake. Check out the additional [configuration options](#cmake-configuration-options).

    ```shell
    cmake ..
    ```

    **Note:** On Windows, it's possible to have issues with VS 2017 default compilers.

    ```shell
    cmake .. -G "Visual Studio 15 2017 Win64"
    ```

4. Build the project using [CMake Build Tool Mode]. This is a portable variant of `make`.

    ```shell
    cmake --build .
    ```

    Note: On Windows, it is possible to have compiler issues if you don't specify the build config. In that case use:

    ```shell
    cmake --build . --config Release
    ```

5. _(Optional, Linux only)_ Install the built executable:

    ```shell
    sudo make install
    ```

#### Windows-specific script

Complete sample Windows batch file - **adapt it to your system**. Assumes that:

* it's placed one folder up from the cminer source folder
* you have CMake installed
* you have Perl installed

```bat
@echo off
setlocal

rem add MSVC in PATH
call "%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Community\Common7\Tools\VsMSBuildCmd.bat"

rem add Perl in PATH; it's needed for OpenSSL build
set "PERL_PATH=C:\Perl\perl\bin"
set "PATH=%PERL_PATH%;%PATH%"
set "CMAKE_PATH=C:\Program Files\CMake\bin"
set "PATH=%PERL_PATH%;%CMAKE_PATH%;%PATH%"


if not exist "build\" mkdir "build\"

cmake -G "Visual Studio 15 2017 Win64" -H. -Bbuild -DETHASHCL=ON -DETHASHCUDA=ON -DAPICORE=ON ..
cd build
cmake --build . --config Release --target cminer

endlocal
pause
```

### Disable Hunter

If you want to install dependencies yourself or use system package manager you can disable Hunter by adding
[`-DHUNTER_ENABLED=OFF`](https://docs.hunter.sh/en/latest/reference/user-variables.html#hunter-enabled)
to the configuration options.



## License

This source is forked from https://github.com/ethereum-mining/ethminer

Licensed under the [GNU General Public License, Version 3](LICENSE).

