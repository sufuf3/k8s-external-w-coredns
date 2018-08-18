# Deploy kubernetes externalDNS & coredns with host's etcd

## Setting
### Set cluster dns name
The cluster dns name is **`cluster.local`**

### Set IP

If your VIP is `100.67.151.8`, then do  
```sh
$ cd k8s-external-w-coredns
$ sudo sed -i "s/100.67.151.8/${LB_VIP_ADDRESS}/g" coredns/svc-lb-tcp.yml
$ sudo sed -i "s/100.67.151.8/${LB_VIP_ADDRESS}/g" coredns/svc-lb-udp.yml
```
### Set etcd-servers

If your option `--etcd-servers` of `/etc/kubernetes/manifests/apiserver.yml` is `https://100.67.151.2:2379,https://100.67.151.3:2379,https://100.67.151.4:2379`, let's do  
```sh
$ sudo sed -i "s/https://100.67.151.2:2379 https://100.67.151.3:2379 https://100.67.151.4:2379/${ETCD_SERVERS}/g" coredns/cm.yml
$ sudo sed -i "s/https://100.67.151.2:2379,https://100.67.151.3:2379,https://100.67.151.4:2379/${ETCD_SERVERS}/g" external-dns/deploy.yml
```

## Deploy
How to deploy, please refer to https://github.com/sufuf3/k8s-external-coredns
