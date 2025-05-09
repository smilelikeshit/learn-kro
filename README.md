# learn-kro
# Kro 

Kro is a framework for creating and managing Kubernetes resources using **ResourceGraphDefinition (RGD)**. It allows users to define and manage Kubernetes resources declaratively with a simple and flexible schema. With Kro, you can easily define and manage complex applications in Kubernetes using a single configuration file.

---

## Installation

Follow the steps below to install **Kro CLI** and the **Kro controller** on your Kubernetes cluster.

### 1. Install Kro CLI

Kro CLI allows you to create and manage **ResourceGraphDefinition (RGD)** in your Kubernetes cluster.

#### 1.1. Install Kro via `curl` (Linux/macOS)

```bash
curl -sSL https://github.com/kro-cl/kro/releases/latest/download/kro-linux-amd64 -o /usr/local/bin/kro
chmod +x /usr/local/bin/kro
```


#### 1.2. Install Kro via `helm` 
```bash
export KRO_VERSION=$(curl -sL \
    https://api.github.com/repos/kro-run/kro/releases/latest | \
    jq -r '.tag_name | ltrimstr("v")'
  )

helm install kro oci://ghcr.io/kro-run/kro/kro \
  --namespace kro \
  --create-namespace \
  --version=${KRO_VERSION}

helm ls
NAME	NAMESPACE	REVISION	UPDATED                             	STATUS  	CHART    	APP VERSION
kro 	kro      	1       	2025-05-09 20:27:44.358305 +0700 WIB	deployed	kro-0.2.3	0.2.3
```

## Getting Started 
### Deploy RGD Postgres and Create StatefulSet Postgres
```bash 
kubectl apply -f rgd/postgresql.yaml
kubectl apply -f postgresql.yaml

kubectl get rgd
NAME                APIVERSION   KIND         STATE    AGE
imm.db.mysql        v1alpha1     Mysql        Active   25m

kubectl get crd
postgresqls.kro.run                2025-05-09T13:58:38Z

kubectl get postgresql
NAME     STATE    SYNCED   AGE
pg-one   ACTIVE   True     53m

# postgresql statefulset should be created successfully


```


### Deploy RGD Mysql  and Create Statefulset Mysql
```bash
kubectl apply -f rgd/mysql.yaml
kubectl apply -f mysql.yaml


kubectl get rgd
NAME                APIVERSION   KIND         STATE    AGE
imm.db.mysql        v1alpha1     Mysql        Active   25m

kubectl get crd
NAME                               CREATED AT
mysqls.kro.run                     2025-05-09T14:31:37Z

kubectl get mysql
NAME        STATE    SYNCED   AGE
mysql-one   ACTIVE   True     15m

# mysql statefulset should be created successfully

```


## Reference
- https://kro.run/