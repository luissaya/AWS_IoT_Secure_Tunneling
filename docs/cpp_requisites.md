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
2. (optional) Run the next line to get latest package updates.
  ```BASH
  sudo apt-get update
  ```
3. (optional) Run the next line to install latest package updates.
  ```BASH
  sudo apt-get upgrade
  ```
4. Installation. 
  * To install GCC run the following:
    ```BASH
    sudo apt-get install build-essential
    ```
  * To install Clang run the following
    ```BASH
    sudo apt-get install clang
    ```
5. Once the install is finished, close the terminal and reopen it.
6. Confirm the installation by running:
  * for GCC 
    ```BASH
    gcc --version
    ```
  * for Clang
    ```BASH
    clang --version
    ```
## Linux CMake
There are several ways to install CMake depending on the Linux operating system. Several Linux operating systems include CMake in their software repository applications, like the Ubuntu Software Center for example, so you may want to check there first.

**Install CMake on Ubuntu**
1. Open a new terminal
2. Run it to install CMake from the snap store
  ```BASH
  sudo snap install cmake
  ```
  if there is an error execute:
  ```BASH
  sudo snap install cmake --classic
  ```
3. After CMake has installed, close the terminal and reopen it
4. Type the following to confirm CMake is installed
  ```BASH
  cmake --version;l
  ```

[//]: #https://www.linode.com/docs/guides/how-to-install-selinux-on-ubuntu-22-04/