# k3s-install

Alpine requirements:
- sudo
- curl
- https://rancher.com/docs/k3s/latest/en/advanced/#additional-preparation-for-alpine-linux-setup


Cluster Init
```
k3sup install --ip 192.168.2.231 --user root --cluster --k3s-version v1.21.0+k3s1
```
Join other masters
```
k3sup join --ip 192.168.2.232 --user root --k3s-version v1.21.0+k3s1 --server-user root --server-ip 192.168.2.231 --server
k3sup join --ip 192.168.2.233 --user root --k3s-version v1.21.0+k3s1 --server-user root --server-ip 192.168.2.231 --server
```

Admin Dashboard
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
```

Dashboard admin user
```
kubectl apply -f dashboard-admin.yml
```

Dashboard admin user token
```
kubectl get secret -n kubernetes-dashboard $(kubectl get serviceaccount admin-user -n kubernetes-dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode
```
