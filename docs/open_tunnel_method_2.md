# Open a tunnel using manual setup and connect to remote device
This tutorial shows how to open a tunnel using the manual setup method and configure and start the local proxy to connect to the remote device.
## Prerequisites for manual setup method
* The firewalls that the remote device is behind must allow outbound traffic on port 443. The tunnel that you create will use this port to connect to the remote device.
* You have an IoT device agent (see IoT agent snippet) running on the remote device that connects to the AWS IoT device gateway and is configured with an MQTT topic subscription.
* You must have an SSH daemon running on the remote device.
* You have downloaded the local proxy source code from [GitHub](https://github.com/aws-samples/aws-iot-securetunneling-localproxy) and built it for the platform of your choice.

## Open a tunnel
Refer to [Open a tunnel and use browser-based SSH to access remote device](./open_tunnel_method_1.md)

## Resend tunnel access tokens
The tokens that you obtained when creating a tunnel can only be used once to connect to the tunnel. If you misplace the access token or the tunnel gets disconnected, you can resend new access tokens to the remote device using MQTT at no additional charge. AWS IoT secure tunneling will revoke the current tokens and return new access tokens for reconnecting to the tunnel.
**To rotate the tokens from the console**
1. Go to the Tunnels hub of the AWS IoT console and choose the tunnel that you created.
2. In the tunnel details page, choose Generate new access tokens and then choose Next.
3. Download the new access tokens for your tunnel and choose Done. These tokens can be used only once.
![image](https://docs.aws.amazon.com/images/iot/latest/developerguide/images/tunnel-token-rotated.PNG)
**To rotate access tokens using the API**
To rotate the tunnel access tokens, you can use the RotateTunnelAccessToken API operation to revoke the current tokens and return new access tokens for reconnecting to the tunnel. For example, the following command rotates the access tokens for the destination device, `RemoteThing1`.
```BASH
aws iotsecuretunneling rotate-tunnel-access-token \ 
    --tunnel-id <tunnel-id> \ 
    --client-mode DESTINATION \ 
    --destination-config thingName=<RemoteThing1>,services=SSH \ 
    --region <region>
```
Running this command generates the new access token as shown in the following example. The token is then delivered to the device using MQTT to connect to the tunnel, if the device agent is set up correctly.
```BASH
{
    "destinationAccessToken": "destination-access-token", 
    "tunnelArn": "arn:aws:iot:region:account-id:tunnel/tunnel-id"
}
```
## Configure and start the local proxy
To connect to the remote device, open a terminal on your laptop and configure and start the local proxy. The local proxy transmits data sent by the application running on the source device by using secure tunneling over a WebSocket secure connection. You can download the local proxy source from [GitHub.](https://github.com/aws-samples/aws-iot-securetunneling-localproxy)

After you configure the local proxy, copy the source client access token, and use it to start the local proxy in source mode. Following shows an example command to start the local proxy. In the following command, the local proxy is configured to listen for new connections on port 5555. In this command:
* `-r` specifies the AWS Region, which must be the same Region where your tunnel was created.
* `-s` specifies the port to which the proxy should connect.
* `-t` specifies the client token text.
```BASH
./localproxy -r us-east-1 -s 5555 -t source-client-access-token
```
Running this command will start the local proxy in source mode. If you receive the following error after running the command, set up the CA path. For information, see Secure tunneling local proxy on GitHub.
```BASH
Could not perform SSL handshake with proxy server: certificate verify failed
```
The following shows a sample output of running the local proxy in `source` mode.
```BASH
...
...

Starting proxy in source mode
Attempting to establish web socket connection with endpoint wss://data.tunneling.iot.us-east-1.amazonaws.com:443
Resolved proxy  server IP: 10.10.0.11
Connected successfully with proxy server
Performing SSL handshake with proxy server	
Successfully completed SSL handshake with proxy server
HTTP/1.1 101 Switching Protocols

...

Connection: upgrade
channel-id: 01234567890abc23-00001234-0005678a-b1234c5de677a001-2bc3d456
upgrade: websocket

...

Web socket session ID: 01234567890abc23-00001234-0005678a-b1234c5de677a001-2bc3d456
Web socket subprotocol selected: aws.iot.securetunneling-2.0
Successfully established websocket connection with proxy server: wss://data.tunneling.iot.us-east-1.amazonaws.com:443
Setting up web socket pings for every 5000 milliseconds
Scheduled next read:

...

Starting web socket read loop continue reading...
Resolved bind IP: 127.0.0.1
Listening for new connection on port 5555
```
## Start an SSH session
Open another terminal and use the following command to start a new SSH session by connecting to the local proxy on port 5555.
```BASH
ssh username@localhost -p 5555
```
You might be prompted for a password for the SSH session. When you are done with the SSH session, type exit to close the session.
## Cleaning up
Refer to [Open a tunnel and use browser-based SSH to access remote device](./open_tunnel_method_1.md)
