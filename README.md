# metallb installation

öncelikle kube-proxy de stric arp true yapılır.

kubectl edit configmap -n kube-system kube-proxy

komutu sonrası stricARP tru yapılır ve kaydedilir.

## install metallb

```
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.12.0/manifests/namespace.yaml

kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.12.0/manifests/metallb.yaml
```

## metallb için config map

```
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - 172.30.2.200-172.30.2.250
```

## example

```deployment => kubectl create deployment web --image=nginx```

```expose svc => kubectl expose deployment web --port 80 --type LoadBalancer```
