# AWS IoT Device Client
[Reference](https://github.com/awslabs/aws-iot-device-client#installation)

## Minimum Requirements
- [aws-iot-device-sdk-cpp-v2](./AWS_IoT_device_sdk_cpp_v2.md) commit hash located in `CMakeLists.txt.awssdk`
- OpenSSL version 3 and libssl-dev([installation process](./OpenSSL_3.md)).
## Quick Start
```BASH
# Building
git clone https://github.com/awslabs/aws-iot-device-client
cd aws-iot-device-client
mkdir build
cd build
cmake ../
cmake --build . --target aws-iot-device-client
```