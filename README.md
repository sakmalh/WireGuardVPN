# WireGuardVPN
Deploying a VPN Pod in the kubernetes Cluster.

- Deploying a VPN as a Pod in a kubernetes cluster
- Client config can be found in /config/peer_user/peer_user.conf
- Check the Logs of the Pod to obtain the QR for the client connection
- Instead of NodePort. Loadbalancer or an Ingress can be used
- Using PV will retain the client conf when container restarts
- If the client does not connect to the internet after connecting. Please try this on the server '''sysctl -w net.ipv4.ip_forward=1'''
- Clients can be easily added with the env variable PEERS

```
# Exec inside the pod
kubectl exec -n example -it deployment/wireguard -- bash

#Check current peers and interface
wg show
```

# Client

Install Wireguard for linux
```
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install wireguard
```

Change config file 
```
sudo nano /etc/wireguard/wg0.conf
```

Starting up VPN
```
sudo wg-quick up wg0
```

Shutting down VPN
```
sudo wg-quick down wg0
```
