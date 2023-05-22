# AWS IoT Device Client
[Reference](https://github.com/awslabs/aws-iot-device-client#installation)

## Method 1: Docker fully compiled image
* Download and install [docker](https://www.docker.com/products/docker-desktop/)
* Check docker installation : `docker --version`
* Download the docker image from [here](https://gallery.ecr.aws/aws-iot-device-client/aws-iot-device-client) based on your architecture.
  ```BASH
  docker pull  public.ecr.aws/aws-iot-device-client/aws-iot-device-client:arm64-ubuntu-latest
  ```
* Copy the *IMAGE ID* from the output of the following command:
  ```BASH
  docker images
  ```
* Run a container named `aws-iot`, based on the *IMAGE_ID*, and enter into `bash`.
  ```BASH
  docker run -it --name aws-iot --entrypoint /bin/bash IMAGE_ID
  ```
* Open another console and Go to `/home/USER` and create the folder `projects`
  ```BASH
  cd ~
  mkdir projects
  ```
* Inside `projects`, download the zip of the official repository and unzip.
  ```BASH
  cd projects
  wget https://github.com/awslabs/aws-iot-device-client/archive/refs/heads/main.zip
  unzip main.zip
  rm main.zip
  ```
* Go into `aws-iot-device-client` and create the folder `build`
  ```BASH
  cd aws-iot-device-client
  mkdir build
  ```
* Copy the `aws-iot-device-client` compiled executable from the docker container to the `build` folder. Also change the permission of the file.
  ```BASH
  docker cp aws-i:/aws-iot-device-client build/
  chmod 755 build/aws-iot-device-client
  ```
* Finally, stop the container and eliminate all.
  ```BASH
  docker stop aws-iot
  docker container rm aws-iot
  docker images rm IMAGE_ID
  ```

## Method 2: Local compiling

### Minimum Requirements
- [aws-iot-device-sdk-cpp-v2](./AWS_IoT_device_sdk_cpp_v2.md) commit hash located in `CMakeLists.txt.awssdk`
- OpenSSL and libssl-dev([installation process](./OpenSSL_and_libssl-dev.md)).
### Process
* Go to `/home/USER` and create the folder `projects`
  ```BASH
  cd ~
  mkdir projects
  ```
* Go into `projects` and clone the official github
  ```BASH
  mkdir projects
  git clone https://github.com/awslabs/aws-iot-device-client
  ```
* Go into `aws-iot-device-client` and create `build`
  ```BASH
  cd aws-iot-device-client
  mkdir build
  ```
* Inside `build` run the compilation
  ```BASH
  cd build
  cmake ../
  cmake --build . --target aws-iot-device-client
  ```