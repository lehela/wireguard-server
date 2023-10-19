# Wireguard Server

The server is using the linuxserver.io docker container:
https://github.com/linuxserver/docker-wireguard

## Updates to docker-compose

### environment
1. `SERVERURL=wireguard.lehela.com`
2. `PEERS=leifs8,leifiphone,leifmbp,jjflip`

### volumes
3. `${PWD}/config:/config`

## FritzBox NAT Port forwarding
I forwarded the available external port 7540 on my FritzBox to the port 51820 on my goo2sg host for the UDP protocol. Note, that this host port is in turn forwarded to the 51820 port inside the docker container by default in the docker-compose `ports` section.

## Usage

### Start the WireGuard server
```shell
docker-compose up -d
```
The `PEERS` variable is now generating a client profile with QR code for each peer in the list. The client profiles are available as a QR code png in the `${PWD}/config/peer_[..]` folders.
If you add another peer to the list, you must first execute `docker-compose down`, and then start the server again in order for the new profiles to appear.

### Connect a WireGuard client 

#### iPhone/Samsung
1. I installed the official WireGuard client from the respective App Store
2. I clicked on adding a tunnel using `Create from QR Code`
3. I scanned the QR code from the designated iphone `${PWD}/config/peer_[..]` folder
4. Under the `PEER` section I had to update the `Endpoint` to `wireguard.lehela.com:7540` in order to reflect my NAT Port Forwarding. Note that that port in the `INTERFACE` section had to remain on 51820!
5. Toggle on the tunnel.. 
> You don't see any error messages in the client UI directly. Via the app settings you can view the logs which contain errors such as failed handshakes..



