# Rancher and Domain Name Custimization
In this tutorial, we will introduce layer-7 load-balancing( `external-DNS` + `DNS provider(BIND9)` + `Nginx ingress controller` ).
## Environment
OS: Ubuntu 18.04.5 LTS (Bionic Beaver)

Docker:  Docker Engine - Community (or Enterprise) v19.0.13

Kubernetes: MicroK8s v1.9.3 or other kubernetes engine

## Usage
You can follow the tutorial on external-dns [official website](https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/rfc2136.md) or use the configuration files we provided in this repository.


### BIND configuration
- install bind9
```shell=
sudo apt install -y bind9
```

- use [our configuration file](https://github.com/nemslab/External-DNS/tree/master/BIND9) or wirte one for your own setting
- put `etc_bind` files to `/etc/bind`
- put `var_cache_bind` files to `/var/cache/bind`, and set owner to bind
```bash=
$ sudo chown -R bind:bind /var/cache/bind
```
- start bind9
```bash=
$ sudo service bind9 start
```
### Install External-DNS
- Download the yaml file in the [official website](https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/rfc2136.md) and apply that yaml file to microk8s or use our [yaml file](https://github.com/nemslab/External-DNS/tree/master/external-dns).

### Nginx ingress controller
- enable ingress on microk8s
```shell=
microk8s enable ingress
```

* set `--publish-status-address` to your DNS server IP address
```shell=
kubectl edit daemonset.apps/nginx-ingress-microk8s-controller -n ingress
```
- we also provide [yaml file](https://github.com/nemslab/External-DNS/tree/master/ingress) for ingress

## Contact Us
- project link: [MEC Middlebox](https://github.com/nemslab/MEC-Middlebox)
- You are very welcome to report bugs, ask questions, or/and request supports. If there are any, please contact us via nems@g2.nctu.edu.tw.
