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

**For b827ebf379fb**
* AWS IoT endpoint: 
  ```BASH
  a35lkm5jyds64h-ats.iot.us-east-1.amazonaws.com
  ```
* Path to public PEM certificate
  ```BASH
  /home/fabricio/projects/sdk-workspace/aws-iot-device-client/identity/b827ebf379fb-certificate.pem.crt
  ```
* Path to the private key
  ```BASH
  /home/fabricio/projects/sdk-workspace/aws-iot-device-client/identity/b827ebf379fb-private.pem.key
  ```
* Path to the ROOT CA certificate
  ```BASH
  /home/fabricio/projects/sdk-workspace/aws-iot-device-client/identity/b827ebf379fb-CA1.pem
  ```
* Thing name
  ```BASH
  f2_b827ebf379fb
  ```
## Process
* Go into `/aws-iot-device-client`
  ```BASH
  mkdir /aws-iot-device-client
  ```
* Create a folder `/identity`
  ```BASH
  mkdir indentity
  ```
* place inside the credentials: PEM certificate, private key and ROOT CA certificate.
  
* Change the permissions on each certificate to 700
  ```BASH
  sudo chmod 700 ./identity
  sudo chmod 644 /identity/b827ebf379fb-certificate.pem.crt
  sudo chmod 600 /identity/b827ebf379fb-private.pem.key
  sudo chmod 644 /identity/b827ebf379fb-CA1.pem
  ```
* Execute the setup file and provide the credentials as needed.  
  ```BASH
  # Setup
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
