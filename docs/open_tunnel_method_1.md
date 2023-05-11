# Open a tunnel and use browser-based SSH to access remote device
[Reference](https://docs.aws.amazon.com/iot/latest/developerguide/tunneling-tutorial-quick-setup.html)
## Prerequisites for quick setup method
* The firewalls that the remote device is behind must allow outbound traffic on port 443. The tunnel that you create will use this port to connect to the remote device.
* You have an IoT device agent (see [IoT agent snippet](https://docs.aws.amazon.com/iot/latest/developerguide/configure-remote-device.html#agent-snippet)) running on the remote device that connects to the AWS IoT device gateway and is configured with an MQTT topic subscription. For more information, see [connect a device to the AWS IoT device gateway.](https://docs.aws.amazon.com/iot/latest/developerguide/sdk-tutorials.html)
* You must have an SSH daemon running on the remote device.
## Open a tunnel
### **To open a tunnel using the console**
1. Go to the [Tunnels hub of the AWS IoT console](https://console.aws.amazon.com/iot/home#/tunnels) and choose Create tunnel.
![image-aws1](https://docs.aws.amazon.com/images/iot/latest/developerguide/images/tunnels-page.png)
2. Choose Quick setup as the tunnel creation method and then choose Next.
![image-aws2](https://docs.aws.amazon.com/images/iot/latest/developerguide/images/tunnels-choose-quick.PNG)
3. Review and confirm the tunnel configuration details. To create a tunnel, choose Confirm and create.  
*Note: When using quick setup, the service name can't be edited. You must use SSH as the Service.*
4. To create the tunnel, choose Done.  
For this tutorial, you don't have to download the source or destination access tokens. *These tokens can only be used once to connect to the tunnel*. If your tunnel gets disconnected, you can generate and send new tokens to your remote device for reconnecting to the tunnel.
![image-aws3](https://docs.aws.amazon.com/images/iot/latest/developerguide/images/tunnel-success.png)

### **To open a tunnel using the API**
The following shows an example of how to run this API operation. Optionally, if you want to specify the thing name and the destination service, use the `DestinationConfig` parameter. For more information: [how to use this parameter.](https://docs.aws.amazon.com/iot/latest/developerguide/tunneling-tutorial-existing-tunnel.html#tunneling-tutorial-existing-open-tunnel)
```BASH
aws iotsecuretunneling open-tunnel
```
Running this command creates a new tunnel and provides you the source and destination access tokens.
```BASH
{
    "tunnelId": "01234567-89ab-0123-4c56-789a01234bcd",
    "tunnelArn": "arn:aws:iot:us-east-1:123456789012:tunnel/01234567-89ab-0123-4c56-789a01234bcd",
    "sourceAccessToken": "<SOURCE_ACCESS_TOKEN>",
    "destinationAccessToken": "<DESTINATION_ACCESS_TOKEN>"
}
```
## Using the browser-based SSH
After you create a tunnel using the quick setup method, and your destination device has connected to the tunnel, you can access the remote device using a browser-based SSH. 
1. Go to the Tunnels hub of the AWS IoT console and choose the tunnel that you created to view its details.
2. Expand the Secure Shell (SSH) section and then choose Connect.
3. Choose whether you want to authenticate into the SSH connection by providing your username and password, or, for more secure authentication, you can use your device's private key. If you're authenticating using the private key, you can use RSA, DSA, ECDSA (nistp-*) and ED25519 key types, in PEM (PKCS#1, PKCS#8) and OpenSSH formats.
  * To connect using your username and password, choose Use password. You can then enter your username and password and start using the in-browser CLI.
  * To connect using your destination device's private key, choose Use private key. Specify your username and upload the device's private key file, and then choose Connect to start using the in-browser CLI.
  ![image-5](https://docs.aws.amazon.com/images/iot/latest/developerguide/images/tunnel-browser-private-key.png)


After you've authenticated into the SSH connection, you can quickly get started with entering commands and interact with the device using the browser CLI, as the local proxy has already been configured for you.
![image-6](https://docs.aws.amazon.com/images/iot/latest/developerguide/images/tunnel-browser-cli.PNG)

If the browser CLI stays open after the tunnel duration, it might time out, causing the command line interface to get disconnected. You can duplicate the tunnel and start another session to interact with the remote device within the console itself.

## Cleaning up
**Close tunnel**
We recommend that you close the tunnel after you've finished using it. A tunnel can also become closed if it stayed open for longer than the specified tunnel duration. A tunnel cannot be reopened once closed. You can still duplicate a tunnel by choosing the closed tunnel and then choosing Duplicate tunnel. Specify the tunnel duration that you want to use and then create the new tunnel.
* To close an individual tunnel or multiple tunnels from the AWS IoT console, go to the Tunnels hub, choose the tunnels that you want to close, and then choose Close tunnel.
* To close an individual tunnel or multiple tunnels using the AWS IoT API Reference API, use the CloseTunnel API.
```BASH
aws iotsecuretunneling close-tunnel \ 
    --tunnel-id "01234567-89ab-0123-4c56-789a01234bcd"
```
**Delete tunnel**
You can delete a tunnel permanently from your AWS account.
* To delete an individual tunnel or multiple tunnels from the AWS IoT console, go to the Tunnels hub, choose the tunnels that you want to delete, and then choose Delete tunnel.

* To delete an individual tunnel or multiple tunnels using the AWS IoT API Reference API, use the CloseTunnel API. When using the API, set the delete flag to true.
```BASH
aws iotsecuretunneling close-tunnel \ 
    --tunnel-id "01234567-89ab-0123-4c56-789a01234bcd"
    --delete true
```