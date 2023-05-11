# PREREQUISITES
## Linux C++ Compilers
Many Linux operating systems have C++ compilers installed by default, so you might already clang or gcc preinstalled. To test, try running the following in a new terminal:
```BASH
clang --version
```
```BASH
gcc --version
```
If these commands fail, then please follow the instructions below for installing a C++ compiler on your Linux operating system.

If your Linux operating system is not in the list, please use a search engine to find out how to install either `clang` or `gcc` on your Linux operating system.

**Install GCC or Clang on Ubuntu**
1. Open a new terminal
2. (optional) Run s`udo apt-get update` to get latest package updates.
3. (optional) Run `sudo apt-get upgrade` to install latest package updates.
4. Run `sudo apt-get install build-essential` to install GCC or `sudo apt-get install clang` to install Clang.
5. Once the install is finished, close the terminal and reopen it.
6. Confirm GCC is installed by running `gcc --version` or Clang is installed by running `clang --version`.

## Linux CMake
There are several ways to install CMake depending on the Linux operating system. Several Linux operating systems include CMake in their software repository applications, like the Ubuntu Software Center for example, so you may want to check there first.

**Install CMake on Ubuntu**
1. Open a new terminal
2. Run `sudo snap install cmake` to install CMake from the snap store
3. After CMake has installed, close the terminal and reopen it
4. Type `cmake --version` to confirm CMake is installed