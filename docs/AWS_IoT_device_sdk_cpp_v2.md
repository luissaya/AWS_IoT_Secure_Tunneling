# AWS IoT Device SDK for C++ v2
[Reference](https://github.com/aws/aws-iot-device-sdk-cpp-v2)
## Minimum Requirements
* C++ 11 or higher
* Clang 3.9+ or GCC 4.8+ or MSVC 2015+
* CMake 3.1+
  [Step-by-step requirements installation](./cpp_requisites.md)
## Process
* Go into /home/USER(your ubuntu user):
  ```BASH
  cd ~
  ```
* Create the folder `/projects`:
  ```BASH
  mkdir projects
  ```
* Go into `/projects` and create a workspace directory to hold all the SDK files
  ```BASH
  cd projects
  mkdir sdk-workspace
  ```
* Go into `/sdk-workspace` and clone the repository 
  ```BASH
  cd sdk-workspace
  git clone --recursive https://github.com/aws/aws-iot-device-sdk-cpp-v2.git
  ```
* Go into the repository folder and ensure all submodules are properly updated
  ```BASH
  cd aws-iot-device-sdk-cpp-v2
  git submodule update --init --recursive
  ```
* Return to the `/sdk-workspace` and Make a build directory for the SDK(Can use any name).
  ```BASH
  cd ..
  mkdir aws-iot-device-sdk-cpp-v2-build
  cd aws-iot-device-sdk-cpp-v2-build
  ```
* Go into the build directory and generate the SDK build files
  - `-DCMAKE_INSTALL_PREFIX` needs to be the absolute/full path to the directory.(Example: "/Users/example/sdk-workspace/).
  - `-DCMAKE_BUILD_TYPE` can be "Release", "RelWithDebInfo", or "Debug"
  ```BASH
  cmake -DCMAKE_INSTALL_PREFIX="<absolute path to sdk-workspace>" -DCMAKE_BUILD_TYPE="Debug" ../aws-iot-device-sdk-cpp-v2
  ```
* Build and install the library
  ```BASH
  cmake --build . --target install
  ```