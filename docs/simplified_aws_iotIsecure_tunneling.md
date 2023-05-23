# Fully build AWS IoT Secure Tunneling

* Create `projects`
  ```BASH
  cd ~
  mkdir projects
  ```
* Go to projects and Download this repository zipped
  ```BASH
  cd projects
  wget zip-link
  ```
* Unzip and copy the folder `aws-iot-device-client` outside
  ```BASH
  unzip main.zip
  cp -r AWS_IoT_Secure_Tunneling/compiled/arm64/aws-iot-device-client .
  ```
* Eliminate the unnecessary files
  ```BASH
  rm main.zip
  cp -r AWS_IoT_Secure_Tunneling/compiled/arm64/aws-iot-device-client .
  ```

* Go to `aws-iot-device-client/` and Change permissions as follow:
  ```BASH
  cd aws-iot-device-client
  sudo chmod 755 ./build/aws-iot-device-client
  sudo chmod 755 ./setup.sh
  ```
* Create a folder `/identity` and change permission.
  ```BASH
  mkdir identity
  sudo chmod 700 ./identity
  ```
* Place inside the folder `identity` the credentials: 
  - PEM certificate(`*.pem.crt`).
  - Private key(`*.pem.key`). 
  - ROOT CA certificate(`*.pem`).
* Change the permissions on each certificate as follow
  ```BASH
  sudo chmod 644 /identity/certificate.pem.crt
  sudo chmod 600 /identity/private.pem.key
  sudo chmod 644 /identity/ROOT_CA1.pem
  ```
* Run the setup.sh
  ```BASH
  sudo ./setup.sh
  ```
  - provide credentials (endpoint and thing name, the others verify the addresses)
  - "n" to *Advance configuration*
  - verify the configuration
  - "n" to *Configure AWS secure tunneling* 
* Check if the service is up
  ```BASH
  sudo service aws-iot-device-client status   
  ```
* Restart the service
  ```BASH
  sudo service aws-iot-device-client restart   
  ```
* Check the logs
  ```BASH
  sudo less /var/log/aws-iot-device-client/aws-iot-device-client.log  
  ```
* Go to [**AWS Configuration**](../README.md#aws-configuration)