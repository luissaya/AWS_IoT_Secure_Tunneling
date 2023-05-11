# Connect a Remote IoT Device using Secure Tunneling
[![IMAGE ALT TEXT](http://img.youtube.com/vi/bRIsuWlzcgs/0.jpg)](http://www.youtube.com/watch?v=bRIsuWlzcgs "Video Title")

## Prerequisites
* AWS IoT Thing created, and the certificate, private key and root CA on the device.
* AWS IoT Device Client is built on the device([instructions](./docs/AWS_IoT_device_client.md)).

## Credentials
* AWS IoT endpoint
* Path to public PEM certificate
* Path to the private key
* Path to the ROOT CA certificate
* Thing name

## Process
* Provide the credentials  
  ```BASH
  # Setup
  cd ../
  sudo ./setup.sh # At this point you'll need to respond to prompts for information, including paths to your thing certs
  ```
* Check if the service is running
  ```BASH
  sudo service aws-iot-device-client status   
  ```
* Check the logs
  ```BASH
  sudo less aws-iot-device-client.log   
  ```
* Create the tunnel  
  ![create tunnel](./static/aws-create-tunnel.jpg)  
  Select *Create new tunnel* and *Quick setup(SSH)*  
  ![create tunnel](./static/aws-create-tunnel2.jpg)  
  Once tunnel is created, isn't needed to store the tokens. It's going to be sent through MQTT message.
* Connect through SSH  
  On Secure Shell(SSH) select *Connect* then *Use private key*.
  ![create tunnel](./static/aws-create-tunnel3.jpg)
  Upload the private key and connect.
  ![create tunnel](./static/aws-connect.jpg)
  Device Successfully connected!
  ![create tunnel](./static/aws-connect2.jpg)
