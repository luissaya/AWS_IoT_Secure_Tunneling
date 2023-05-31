# Fully build AWS IoT Secure Tunneling

## Working directory
* Go to `projects/` and create the folder `aws-iot-device-client/`
  ```BASH
  cd $HOME/projects
  mkdir aws-iot-device-client
  ```
## Process
* Go to the working directory and Download this repository zipped(right click on *Download ZIP* and copy the link)
  ```BASH
  cd aws-iot-device-client
  wget https://github.com/luissaya/AWS_IoT_Secure_Tunneling/archive/refs/heads/master.zip
  ```
* Unzip and copy the content of the folder `aws-iot-device-client/` outside
  ```BASH
  unzip master.zip
  cp -r AWS_IoT_Secure_Tunneling-master/compiled/arm64/aws-iot-device-client/* .
  ```
* Eliminate the unnecessary files
  ```BASH
  rm main.zip
  rm -r AWS_IoT_Secure_Tunneling-master
  ```

* Change permissions as follow:
  ```BASH
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
  sudo chmod 644 identity/MACaddress-certificate.pem.crt
  sudo chmod 600 identity/MACaddress-private.pem.key
  sudo chmod 644 identity/MACaddress-RootCA1.pem
  ```
* Run the setup.sh
  ```BASH
  sudo ./setup.sh
  ```
  For default configuration:
  - provide credentials (endpoint and thing name, the others verify the addresses)
  - "n" to *Advance configuration*
  - verify the configuration
  - "n" to *Configure AWS secure tunneling*
  - Press *ENTER*
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
* Example of default configuration for enable only the aws iot secure tunneling.
  ```BASH
  WARNING: Only run this setup script as root if you plan to run the AWS IoT Device Client as root,  or if you plan to run the AWS IoT Device Client as a service. Otherwise, you should run this script as  the user that will execute the client.
  Do you want to interactively generate a configuration file for the AWS IoT Device Client? y/n
  y #TYPE y
  Specify AWS IoT endpoint to use:
    #TYPE THE ENDPOINT
  Specify full path to public PEM certificate:(Press enter for default location: /home/USER/projects/aws-iot-device-client/identity/MACaddress-certificate.pem.crt)
    #TYPE ENTER if you are agree with the default file
  Specify full path to private key:(Press enter for default location: /home/USER/projects/aws-iot-device-client/identity/MACaddress-private.pem.key)
    #TYPE ENTER if you are agree with the default file
  Specify full path to ROOT CA certificate:(Press enter for default location: /home/USER/projects/aws-iot-device-client/identity/MACaddress-RootCA1.pem)
    #TYPE ENTER if you are agree with the default file
  Specify thing name (Also used as Client ID):
    #TYPE THE THING NAME
  Would you like to continue to advance configuration? y/n
  n #TYPE n
  Creating default log directory...
  Creating default SDK log directory...

      {
        "endpoint":	"endpoint.iot.us-east-1.amazonaws.com",
        "cert":	"/home/USER/projects/aws-iot-device-client/identity/MACaddress-certificate.pem.crt",
        "key":	"/home/USER/projects/aws-iot-device-client/identity/MACaddress-private.pem.key",
        "root-ca":	"/home/USER/projects/aws-iot-device-client/identity/MACaddress-RootCA1.pem",
        "thing-name":	"thig-name",
        "logging":	{
          "level":	"",
          "type":	"FILE",
          "file": "/var/log/aws-iot-device-client/aws-iot-device-client.log",
          "enable-sdk-logging":	false,
          "sdk-log-level":	"",
          "sdk-log-file": "/var/log/aws-iot-device-client/sdk.log"
        },
        "jobs":	{
          "enabled":	false,
          "handler-directory": "/etc/.aws-iot-device-client/jobs"
        },
        "tunneling":	{
          "enabled":	true
        },
        "device-defender":	{
          "enabled":	false,
          "interval": 300
        },
        "fleet-provisioning":	{
          "enabled":	false,
          "template-name": "",
          "template-parameters": "",
          "csr-file": "",
          "device-key": ""
        },
        "samples": {
          "pub-sub": {
            "enabled": false,
            "publish-topic": "",
            "publish-file": "/etc/.aws-iot-device-client/pubsub/publish-file.txt",
            "subscribe-topic": "",
            "subscribe-file": "/etc/.aws-iot-device-client/pubsub/subscribe-file.txt"
          }
        },
        "config-shadow":	{
          "enabled":	false
        },
        "sample-shadow": {
          "enabled": false,
          "shadow-name": "",
          "shadow-input-file": "",
          "shadow-output-file": ""
        }
      }
  Does the following configuration appear correct? If yes, configuration will be written to /etc/.aws-iot-device-client/aws-iot-device-client.conf: y/n
  y #TYPE y
  Configuration has been successfully written to /etc/.aws-iot-device-client/aws-iot-device-client.conf
  Creating default pubsub directory...
  Would you like to configure AWS secure tunneling? y/n (By default, AWS secure tunneling is installed as a service and valgrind disabled)
  n #TYPE n
    # PRESS ENTER
  Installing AWS IoT Device Client...
  /usr/bin/systemctl
  Failed to stop aws-iot-device-client.service: Unit aws-iot-device-client.service not loaded.
  Created symlink /etc/systemd/system/multi-user.target.wants/aws-iot-device-client.service → /etc/systemd/system/aws-iot-device-client.service.

  ● aws-iot-device-client.service - AWS IoT Device Client
      Loaded: loaded (/etc/systemd/system/aws-iot-device-client.service; enabled; vendor preset: e>
      Active: active (running) since Wed 2023-05-31 13:53:17 ADT; 32ms ago
    Main PID: 9947 (aws-iot-device-)
        Tasks: 2 (limit: 8124)
      Memory: 928.0K
      CGroup: /system.slice/aws-iot-device-client.service
              └─9947 /sbin/aws-iot-device-client --config-file /etc/.aws-iot-device-client/aws-iot>

  May 31 13:53:17 ubuntu systemd[1]: Started AWS IoT Device Client.
  AWS IoT Device Client is now running! Check /var/log/aws-iot-device-client/aws-iot-device-client.log for log output.
  ```