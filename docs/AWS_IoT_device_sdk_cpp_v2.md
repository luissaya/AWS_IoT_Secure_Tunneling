# AWS IoT Device SDK for C++ v2
## Minimum Requirements
* C++ 11 or higher
* Clang 3.9+ or GCC 4.8+ or MSVC 2015+
* CMake 3.1+
  [Step-by-step requirements installation](./cpp_requisites.md)
## Process
```BASH
# Create a workspace directory to hold all the SDK files
mkdir sdk-workspace
cd sdk-workspace
# Clone the repository
git clone --recursive https://github.com/aws/aws-iot-device-sdk-cpp-v2.git
# Ensure all submodules are properly updated
cd aws-iot-device-sdk-cpp-v2
git submodule update --init --recursive
cd ..
# Make a build directory for the SDK. Can use any name.
# If working with multiple SDKs, using a SDK-specific name is helpful.
mkdir aws-iot-device-sdk-cpp-v2-build
cd aws-iot-device-sdk-cpp-v2-build
# Generate the SDK build files.
# -DCMAKE_INSTALL_PREFIX needs to be the absolute/full path to the directory.
#     (Example: "/Users/example/sdk-workspace/).
# -DCMAKE_BUILD_TYPE can be "Release", "RelWithDebInfo", or "Debug"
cmake -DCMAKE_INSTALL_PREFIX="<absolute path to sdk-workspace>" -DCMAKE_BUILD_TYPE="Debug" ../aws-iot-device-sdk-cpp-v2
# Build and install the library. Once installed, you can develop with the SDK and run the samples
cmake --build . --target install
```