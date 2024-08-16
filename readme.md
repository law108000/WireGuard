## Key Generation
### generate client keys
```
wg genkey | tee client_private.key | wg pubkey > client_public.key
```

### generate server keys
```
wg genkey | tee server_private.key | wg pubkey > server_public.key
```

## WG Server
### config for server (wg0.conf)
```shell
[Interface]
# Private key for the server
PrivateKey = kBay51YlrzvA04PLfKZXrjff3KP2e3VGRgBFuntILnw=
# IP address for the server
Address = 10.0.0.1/24
# Port to listen on
ListenPort = 51820

# Save the configuration
SaveConfig = true

# PostUp and PostDown commands to configure firewall rules
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -A FORWARD -o %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -D FORWARD -o %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

[Peer]
# Public key of the client
PublicKey = Nm0byLcvM/PAweUlSnRvhVRE9FlyPg4OksZCrysglhc=
# Allowed IPs for the client
AllowedIPs = 10.0.0.2/32
```

### start the wg server
```shell
wg-quick up wg0
```

### Verify the WireGuard server is running
1. Check the status
```shell
sudo wg show
```
2. Check the network interface
```shell
ip a show wg0
```

## WG Client
### config for client (wg0-client.conf)
```shell
[Interface]
PrivateKey = 6JgVkvoI4+Yzxhy/juXod7mOmxb/VVSaczoT2JMZQ34=
Address = 10.0.0.2/24
DNS = 8.8.8.8

[Peer]
PublicKey = Nm0byLcvM/PAweUlSnRvhVRE9FlyPg4OksZCrysglhc=
Endpoint = server:51820
AllowedIPs = 0.0.0.0/0
```

### start the wg client
```shell
wg-quick up wg-client.conf
```
### Verify the connection
```shell
sudo wg show
```
