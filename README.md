<div align="center">
  
  ![Banner- Memphis dev streaming  (2)](https://github.com/memphisdev/memphis-k8s/assets/107035359/ab72eb91-2589-4c2b-aa54-3bc1b120bcac)

  
</div>

<div align="center">

  <h4>

**[Memphis](https://memphis.dev)** is a next-generation alternative to traditional message brokers.

  </h4>
  
  <a href="https://landscape.cncf.io/?selected=memphis"><img width="200" alt="CNCF Silver Member" src="https://github.com/cncf/artwork/raw/master/other/cncf-member/silver/white/cncf-member-silver-white.svg#gh-dark-mode-only"></a>
  
</div>

<div align="center">
  
  <img width="200" alt="CNCF Silver Member" src="https://github.com/cncf/artwork/raw/master/other/cncf-member/silver/color/cncf-member-silver-color.svg#gh-light-mode-only">
  
</div>
 
 <p align="center">
  <a href="https://memphis.dev/docs/">Docs</a> - <a href="https://twitter.com/Memphis_Dev">Twitter</a> - <a href="https://www.youtube.com/channel/UCVdMDLCSxXOqtgrBaRUHKKg">YouTube</a>
</p>

<p align="center">
<a href="https://discord.gg/WZpysvAeTf"><img src="https://img.shields.io/discord/963333392844328961?color=6557ff&label=discord" alt="Discord"></a>
<a href="https://github.com/memphisdev/memphis/issues?q=is%3Aissue+is%3Aclosed"><img src="https://img.shields.io/github/issues-closed/memphisdev/memphis?color=6557ff"></a> 
  <img src="https://img.shields.io/npm/dw/memphis-dev?color=ffc633&label=installations">
<a href="https://github.com/memphisdev/memphis/blob/master/CODE_OF_CONDUCT.md"><img src="https://img.shields.io/badge/Code%20of%20Conduct-v1.0-ff69b4.svg?color=ffc633" alt="Code Of Conduct"></a> 
<a href="https://docs.memphis.dev/memphis/release-notes/releases/v0.4.2-beta"><img alt="GitHub release (latest by date)" src="https://img.shields.io/github/v/release/memphisdev/memphis?color=61dfc6"></a>
<img src="https://img.shields.io/github/last-commit/memphisdev/memphis?color=61dfc6&label=last%20commit">
</p>

A simple, robust, and durable cloud-native message broker wrapped with<br>
an entire ecosystem that enables cost-effective, fast, and reliable development of modern queue-based use cases.<br><br>
Memphis enables the building of modern queue-based applications that require<br>
large volumes of streamed and enriched data, modern protocols, zero ops, rapid development,<br>
extreme cost reduction, and a significantly lower amount of dev time for data-oriented developers and data engineers.

# Memphis Kubernetes Deployment

If you prefer using **Terraform**, head [here](https://github.com/memphisdev/memphis-terraform)

Helm is a k8s package manager that allows users to deploy apps in a single, configurable command.<br>
More information about Helm can be found [here](https://helm.sh/docs/topics/charts/).

Memphis is cloud-native and cloud-agnostic to any Kubernetes on **any cloud**.

## Requirements

**Minimum Requirements (Without high availability)**

<table><thead><tr><th>Resource</th><th>Quantity</th><th data-hidden></th></tr></thead><tbody><tr><td>Minimum Kubernetes version</td><td>1.20 and above</td><td></td></tr><tr><td>K8S Nodes</td><td>1</td><td></td></tr><tr><td>CPU</td><td>2 CPU</td><td></td></tr><tr><td>Memory</td><td>4GB RAM</td><td></td></tr><tr><td>Storage</td><td>12GB PVC</td><td></td></tr></tbody></table>

***

**Recommended Requirements (With high availability)**

| Resource                   | Minimum Quantity  |
| -------------------------- | ----------------- |
| Minimum Kubernetes version | 1.20 and above    |
| K8S Nodes                  | 3                 |
| CPU                        | 4 CPU             |
| Memory                     | 8GB RAM           |
| Storage                    | 12GB PVC Per node |

## Installation

<details>

<summary>Production</summary>

Production-grade Memphis with three memphis brokers configured in cluster-mode

```bash
helm repo add memphis https://k8s.memphis.dev/charts/ --force-update && helm install memphis memphis/memphis --set global.cluster.enabled="true" --create-namespace --namespace memphis --wait
```

</details>

<details>

<summary>Dev</summary>

Standard installation of Memphis with a single broker

```bash
helm repo add memphis https://k8s.memphis.dev/charts/ --force-update && 
helm install memphis memphis/memphis --create-namespace --namespace memphis --wait
```

</details>

#### \* Optional \* Helm deployment options

| Option                    | Description                                                                                                                     | Default Value | Example                       |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------- | ----------------------------- |
| rootPwd                   | Root password for the dashboard                                                                                                 | `"memphis"`   | `"memphis"`                   |
| user\_pass\_based\_auth          | <p>Authentication method selector.<br><code>true = User + pass</code><br><code>false = User + connection token</code></p>       | `"true"`      | `"true"`                      |
| connectionToken           | Token for connecting an app to the Memphis Message Queue. Auto generated                                                        | `""`          | `"memphis"`                   |
| dashboard.port            | Dashboard's (GUI) port                                                                                                          | 9000          | 9000                          |
| global.cluster.enabled    | Cluster mode for HA and Performance                                                                                             | `"false"`     | `"false"`                     |
| exporter.enabled          | Prometheus exporter                                                                                                             | `"false"`     | `"false"`                     |
| analytics                 | Collection of anonymous metadata                                                                                                | `"true"`      | `"true"`                      |
| websocket.tls.secret.name | <p><strong>*Optional*</strong> Memphis GUI using websockets for live rendering.<br>K8S secret name for the certs</p>            | ""            | `"memphis-ws-tls-secret"`     |
| websocket.tls.cert        | <p><strong>*Optional*</strong><br>Memphis GUI using websockets for live rendering.<br>.pem file to use</p>                      | ""            | `"memphis_local.pem"`         |
| websocket.tls.key         | <p><strong>*Optional*</strong><br>Memphis GUI using websockets for live rendering.<br>key file</p>                              | ""            | `"memphis-key_local.pem"`     |
| memphis.tls.verify        | <p><strong>*Optional*</strong><br>For encrypted client-memphis communication. Verification for the CA autority. SSL.</p>        | ""            | `"true"`                      |
| memphis.tls.secret.name   | <p><strong>*Optional*</strong><br>For encrypted client-memphis communication.<br>K8S secret name that holds the certs. SSL.</p> | ""            | `"memphis-client-tls-secret"` |
| memphis.tls.cert          | <p><strong>*Optional*</strong><br>For encrypted client-memphis communication.<br>.pem file to use. SSL.</p>                     | ""            | `"memphis_client.pem"`        |
| memphis.tls.key           | <p><strong>*Optional*</strong><br>For encrypted client-memphis communication.<br>Private key file to use. SSL.</p>              | ""            | `"memphis-key_client.pem"`    |
| memphis.tls.ca            | <p><strong>*Optional*</strong><br>For encrypted client-memphis communication.<br>CA file to use. SSL.</p>                       | ""            | `"rootCA.pem"`                |

Here is how to run an installation command with additional options -&#x20;

```
helm install memphis --set cluster.replicas=3,rootPwd="rootpassword" memphis/memphis --create-namespace --namespace memphis
```

### Deployed pods

- **memphis.** Memphis broker.
- **memphis-rest-gateway.** Memphis REST Gateway.
- **memphis-metadata.** Metadata store.

For more information on each component, please head to the [architecture section](../../memphis/architecture.md#key-components).

## Deploy Memphis with TLS (encrypted communication via SSL)

### 0. Optional: Create self-signed certificates

a) Generate a self-signed certificate using `mkcert`

```bash
$ mkcert -client \
-cert-file memphis_client.pem \
-key-file memphis-key_client.pem  \
"127.0.0.1" "localhost" "*.memphis.dev" ::1 \
email@localhost valera@Valeras-MBP-2.lan
```

b) Find the `rootCA`

```
$ mkcert -CAROOT
```

c) Create self-signed certificates for client

```bash
$ mkcert -client -cert-file client.pem -key-file key-client.pem  localhost ::1 
```

### 1. Create namespace + secret for the TLS certs

a) Create a dedicated namespace for memphis

```bash
kubectl create namespace memphis
```

b) Create a k8s secret with the required certs


```bash
kubectl create secret generic memphis-client-tls-secret \
--from-file=memphis_client.pem \
--from-file=memphis-key_client.pem \
--from-file=rootCA.pem -n memphis
```

```yaml
tls:
  secret:
    name: memphis-client-tls-secret
  ca: "rootCA.pem"
  cert: "memphis_client.pem"
  key: "memphis-key_client.pem"
```

### 2. Deploy Memphis with the generated certificate

```bash
helm install memphis memphis \
--create-namespace --namespace memphis --wait \
--set \
cluster.enabled="true",\
memphis.tls.verify="true",\
memphis.tls.cert="memphis_client.pem",\
memphis.tls.key="memphis-key_client.pem",\
memphis.tls.secret.name="memphis-client-tls-secret",\
memphis.tls.ca="rootCA.pem"
```

## Upgrade existing deployment

### For adding TLS support

1. Create a k8s secret with the provided TLS certs

```
kubectl create secret generic memphis-client-tls-secret \
--from-file=memphis_client.pem \
--from-file=memphis-key_client.pem \
--from-file=rootCA.pem -n memphis
```

2. Upgrade Memphis to use the TLS certs

```bash
helm upgrade memphis memphis -n memphis --reuse-values \
--set \
memphis.tls.verify="true",\
memphis.tls.cert="memphis_client.pem",\
memphis.tls.key="memphis-key_client.pem",\
memphis.tls.secret.name="tls-client-secret",\
memphis.tls.ca="rootCA.pem"
```

## Deployment diagram

![Memphis Architecture (1)](https://user-images.githubusercontent.com/70286779/229374721-963cd3e6-e425-44cd-8467-233e6fc5e680.jpeg)

