<div align="center">
  
  ![Banner- Memphis dev streaming  (2)](https://github.com/memphisdev/memphis-k8s/assets/107035359/ab72eb91-2589-4c2b-aa54-3bc1b120bcac)

  
</div>

<div align="center">

  <h4>

**[Memphis](https://memphis.dev)** is an intelligent, frictionless message broker.<br>Made to enable developers to build real-time and streaming apps fast.

  </h4>
  
  <a href="https://landscape.cncf.io/?selected=memphis"><img width="200" alt="CNCF Silver Member" src="https://github.com/cncf/artwork/raw/master/other/cncf-member/silver/white/cncf-member-silver-white.svg#gh-dark-mode-only"></a>
  
</div>

<div align="center">
  
  <img width="200" alt="CNCF Silver Member" src="https://github.com/cncf/artwork/raw/master/other/cncf-member/silver/color/cncf-member-silver-color.svg#gh-light-mode-only">
  
</div>
 
 <p align="center">
  <a href="https://memphis.dev/pricing/">Cloud - </a><a href="https://memphis.dev/docs/">Docs</a> - <a href="https://twitter.com/Memphis_Dev">Twitter</a> - <a href="https://www.youtube.com/channel/UCVdMDLCSxXOqtgrBaRUHKKg">YouTube</a>
</p>

<p align="center">
<a href="https://discord.gg/WZpysvAeTf"><img src="https://img.shields.io/discord/963333392844328961?color=6557ff&label=discord" alt="Discord"></a>
<a href="https://github.com/memphisdev/memphis/issues?q=is%3Aissue+is%3Aclosed"><img src="https://img.shields.io/github/issues-closed/memphisdev/memphis?color=6557ff"></a> 
  <img src="https://img.shields.io/npm/dw/memphis-dev?color=ffc633&label=installations">
<a href="https://github.com/memphisdev/memphis/blob/master/CODE_OF_CONDUCT.md"><img src="https://img.shields.io/badge/Code%20of%20Conduct-v1.0-ff69b4.svg?color=ffc633" alt="Code Of Conduct"></a> 
<img alt="GitHub release (latest by date)" src="https://img.shields.io/github/v/release/memphisdev/memphis?color=61dfc6">
<img src="https://img.shields.io/github/last-commit/memphisdev/memphis?color=61dfc6&label=last%20commit">
</p>

Memphis.dev is more than a broker. It's a new streaming stack.<br><br>
It significantly accelerates the development of real-time applications that require a streaming platform with<br>
high throughput, low latency, easy troubleshooting, fast time-to-value,<br>minimal platform operations, and all the observability you can think of.<br>

# Memphis Kubernetes Deployment

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

<table><thead><tr><th width="265.3333333333333">Option</th><th>Description</th><th>Default Value</th><th>Example</th></tr></thead><tbody><tr><td>user_pass_based_auth</td><td>Authentication method selector.<br><code>true = User + pass</code><br><code>false = User + connection token</code></td><td><code>"true"</code></td><td><code>"true"</code></td></tr><tr><td>logsRetentionInDays</td><td>Amount of days to retain system logs</td><td>3</td><td>3</td></tr><tr><td>global.cluster.enabled</td><td>Cluster mode for HA and Performance</td><td><code>"false"</code></td><td><code>"false"</code></td></tr><tr><td>exporter.enabled</td><td>Prometheus exporter</td><td><code>"false"</code></td><td><code>"false"</code></td></tr><tr><td>cluster.enabled</td><td>Enables Memphis cluster deployment. For fully HA configuration use global.cluster.enabled</td><td><code>"false"</code></td><td><code>"true"</code></td></tr><tr><td>cluster.replicas</td><td>Memphis broker replicas</td><td><code>"3"</code></td><td><code>"5"</code></td></tr><tr><td>websocket.tls.secret.name</td><td><strong>*Optional*</strong> Memphis GUI using websockets for live rendering.<br>K8S secret name for the certs</td><td>""</td><td><code>"memphis-ws-tls-secret"</code></td></tr><tr><td>websocket.tls.cert</td><td><strong>*Optional*</strong><br>Memphis GUI using websockets for live rendering.<br>.pem file to use</td><td>""</td><td><code>"memphis_local.pem"</code></td></tr><tr><td>websocket.tls.key</td><td><strong>*Optional*</strong><br>Memphis GUI using websockets for live rendering.<br>key file</td><td>""</td><td><code>"memphis-key_local.pem"</code></td></tr><tr><td>memphis.image</td><td>Memphis image name</td><td>"memphisos/memphis:x.x.x-stable"</td><td>"memphisos/memphis:latest"</td></tr><tr><td>memphis.ui.port</td><td>Dashboard's (GUI) port</td><td>9000</td><td>9000</td></tr><tr><td>memphis.hosts.uiHostName</td><td>Which URL should be seen as the "UI hostname"</td><td>""</td><td><code>"https://memphis.example.com"</code></td></tr><tr><td>memphis.hosts.restgwHostName</td><td>Which URL should be seen as the "REST Gateway hostname"</td><td>""</td><td><code>"https://restgw.memphis.example.com"</code></td></tr><tr><td>memphis.hosts.brokerHostName</td><td>Which URL should be seen as the "broker hostname"</td><td>""</td><td><code>"memphis.example.com"</code></td></tr><tr><td>memphis.creds.rootPwd</td><td>Root password for the dashboard. Randomly generated.</td><td>""</td><td>"superpass"</td></tr><tr><td>memphis.creds.connectionToken</td><td>Token for connecting an app to the Memphis Message Queue. Auto generated.Randomly generated.</td><td>""</td><td>"connectionToken</td></tr><tr><td>memphis.creds.jwtSecret</td><td>For internal traffic. Randomly generated.</td><td>""</td><td>"&#x3C;JWT_TOKEN>"</td></tr><tr><td>memphis.creds.refreshJwtSecret</td><td>For internal traffic. Randomly generated.</td><td>""</td><td>"&#x3C;JWT_TOKEN>"</td></tr><tr><td>memphis.creds.encryptionSecretKey</td><td>Encryption secret key for internal encryption. Randomly generated.</td><td>""</td><td>""</td></tr><tr><td>memphis.customConfigSecret.enabled</td><td><strong>*Optional*</strong><br>Can be configured for external secret that contains all memphis credentials</td><td>"false"</td><td>"true"</td></tr><tr><td>memphis.customConfigSecret.secret.name</td><td><strong>*Optional*</strong><br>Name of the external secret</td><td>""</td><td>"external-secret-name"</td></tr><tr><td>memphis.customConfigSecret.rootPwd_key</td><td><strong>*Optional*</strong><br>Name of the key in secret</td><td>""</td><td>"rootPwd"</td></tr><tr><td>memphis.customConfigSecret.connectionToken_key</td><td><strong>*Optional*</strong><br>Name of the key in secret</td><td>""</td><td>"connectionToken"</td></tr><tr><td>memphis.customConfigSecret.jwtSecret_key</td><td><strong>*Optional*</strong><br>Name of the key in secret</td><td>""</td><td>"jwtSecret"</td></tr><tr><td>memphis.customConfigSecret.refreshJwtSecret_key</td><td><strong>*Optional*</strong><br>Name of the key in secret</td><td>""</td><td>"refreshJwtSecret"</td></tr><tr><td>memphis.customConfigSecret.encryptionSecretKey_key</td><td><strong>*Optional*</strong><br>Name of the key in secret</td><td>""</td><td>"encryptionSecretKey"</td></tr><tr><td>memphis.extraEnvironmentVars.enabled</td><td><strong>*Optional*</strong><br>List of additional environment variables for memphis.</td><td>""</td><td>vars:<br>  - name: KEY<br>  - valye: value</td></tr><tr><td>memphis.tls.verify</td><td><strong>*Optional*</strong><br>For encrypted client-memphis communication. Verification for the CA autority. SSL.</td><td>""</td><td><code>"true"</code></td></tr><tr><td>memphis.tls.secret.name</td><td><strong>*Optional*</strong><br>For encrypted client-memphis communication.<br>K8S secret name that holds the certs. SSL.</td><td>""</td><td><code>"memphis-client-tls-secret"</code></td></tr><tr><td>memphis.tls.cert</td><td><strong>*Optional*</strong><br>For encrypted client-memphis communication.<br>.pem file to use. SSL.</td><td>""</td><td><code>"memphis_client.pem"</code></td></tr><tr><td>memphis.tls.key</td><td><strong>*Optional*</strong><br>For encrypted client-memphis communication.<br>Private key file to use. SSL.</td><td>""</td><td><code>"memphis-key_client.pem"</code></td></tr><tr><td>memphis.tls.ca</td><td><strong>*Optional*</strong><br>For encrypted client-memphis communication.<br>CA file to use. SSL.</td><td>""</td><td><code>"rootCA.pem"</code></td></tr><tr><td>metadata.postgresql.username</td><td><strong>*Optional*</strong><br>Username for postgres db</td><td>"postgres"</td><td>"postgres"</td></tr><tr><td>metadata.pgpool.tls.enabled</td><td><strong>*Optional*</strong><br>Enabling TLS-based communication with PG</td><td>"false"</td><td>"false"</td></tr><tr><td>metadata.pgpool.tls.certificatesSecret</td><td><strong>*Optional*</strong><br>PG TLS cert secret to be used</td><td>""</td><td>"tls-secret"</td></tr><tr><td>metadata.pgpool.tls.certFilename</td><td><strong>*Optional*</strong><br>PG TLS cert file to be used</td><td>""</td><td>"tls.crt"</td></tr><tr><td>metadata.pgpool.tls.certKeyFilename</td><td><strong>*Optional*</strong><br>PG TLS key to be used</td><td>""</td><td>"tls.key"</td></tr><tr><td>metadata.pgpool.tls.certCAFilename</td><td><strong>*Optional*</strong><br>PG TLS cert CA to be used</td><td>""</td><td>"ca.crt"</td></tr><tr><td>metadata.external.enabled</td><td><strong>*Optional*</strong><br>For using external PG instead of deploying dedicated one for Memphis</td><td>"false"</td><td>"true"</td></tr><tr><td>metadata.external.dbTlsMutual</td><td><strong>*Optional*</strong><br>External PG TLS-basec communication</td><td>"true"</td><td>"true"</td></tr><tr><td>metadata.external.dbName</td><td><strong>*Optional*</strong><br>External PG db name</td><td>""</td><td>"memphis"</td></tr><tr><td>metadata.external.dbHost</td><td><strong>*Optional*</strong><br>External PG db hostname</td><td>""</td><td>"metadata.example.url"</td></tr><tr><td>metadata.external.dbPort</td><td><strong>*Optional*</strong><br>External PG db port</td><td>""</td><td>5432</td></tr><tr><td>metadata.external.dbUser</td><td><strong>*Optional*</strong><br>External PG db user</td><td>""</td><td>"postgres"</td></tr><tr><td>metadata.external.dbPass</td><td><strong>*Optional*</strong><br>External PG db password</td><td>""</td><td>"12345678"</td></tr><tr><td>restGateway.enabled</td><td><strong>*Optional*</strong><br>Memphis Rest Gateway can be disabled if not in use</td><td>"true"</td><td>"false"</td></tr><tr><td>restGateway.jwtSecret</td><td><strong>*Optional*</strong><br>Manual Jwt Token configurtion</td><td>""</td><td>""</td></tr><tr><td>restGateway.refreshJwtSecret</td><td><strong>*Optional*</strong><br>Manual Refresh Jwt Token configurtion</td><td>""</td><td>""</td></tr></tbody></table>

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

