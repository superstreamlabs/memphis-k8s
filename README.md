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

| Option | Description | Default Value | Example |
| --- | --- | --- | --- |
| global.cluster.enabled | Cluster mode for HA and Performance | `"false"` | `"false"` |
| exporter.enabled | Prometheus exporter | `"false"` | `"false"` |
| cluster.enabled | Enables Memphis cluster deployment. For fully HA configuration use global.cluster.enabled | `"false"` | `"true"` |
| cluster.replicas | Memphis broker replicas | `"3"` | `"5"` |
| memphis.image | Memphis image name | "memphisos/memphis:x.x.x-stable" | "memphisos/memphis:latest" |
| memphis.ui.port | Dashboard's (GUI) port | 9000 | 9000 |
| memphis.hosts.uiHostName | Which URL should be seen as the "UI hostname" | ""  | `"https://memphis.example.com"` |
| memphis.hosts.restgwHostName | Which URL should be seen as the "REST Gateway hostname" | ""  | `"https://restgw.memphis.example.com"` |
| memphis.hosts.brokerHostName | Which URL should be seen as the "broker hostname" | ""  | `"memphis.example.com"` |
| memphis.configFile.logsRetentionInDays | Amount of days to retain system logs | 3   | 3   |
| memphis.configFile.gcProducerConsumerRetentionInHours | Amount of hours to retain producer/consumer in system | 3  | 3  |
| memphis.configFile.tieredStorageUploadIntervalSeconds | Interval in seconds between uploads to tiered storage | 8  | 8  |
| memphis.configFile.dlsRetentionHours | Amount of hours to retain messages in DLS | 3  | 3  |
| memphis.configFile.userPassBasedAuth | Authentication method selector.  <br>`true = User + pass`  <br>`false = User + connection token` | `"true"` | `"true"` |
| memphis.creds.rootPwd | Root password for the dashboard. Randomly generated. | ""  | "superpass" |
| memphis.creds.connectionToken | Token for connecting an app to the Memphis Message Queue. Auto generated.Randomly generated. | ""  | "connectionToken |
| memphis.creds.jwtSecret | For internal traffic. Randomly generated. | ""  | "&lt;JWT_TOKEN&gt;" |
| memphis.creds.refreshJwtSecret | For internal traffic. Randomly generated. | ""  | "&lt;JWT_TOKEN&gt;" |
| memphis.creds.encryptionSecretKey | Encryption secret key for internal encryption. Randomly generated. | ""  | ""  |
| memphis.customConfigSecret.enabled | **\*Optional\***  <br>Can be configured for external secret that contains all memphis credentials | "false" | "true" |
| memphis.customConfigSecret.secret.name | **\*Optional\***  <br>Name of the external secret | ""  | "external-secret-name" |
| memphis.customConfigSecret.rootPwd_key | **\*Optional\***  <br>Name of the key in secret | ""  | "rootPwd" |
| memphis.customConfigSecret.connectionToken_key | **\*Optional\***  <br>Name of the key in secret | ""  | "connectionToken" |
| memphis.customConfigSecret.jwtSecret_key | **\*Optional\***  <br>Name of the key in secret | ""  | "jwtSecret" |
| memphis.customConfigSecret.refreshJwtSecret_key | **\*Optional\***  <br>Name of the key in secret | ""  | "refreshJwtSecret" |
| memphis.customConfigSecret.encryptionSecretKey_key | **\*Optional\***  <br>Name of the key in secret | ""  | "encryptionSecretKey" |
| memphis.extraEnvironmentVars.enabled | **\*Optional\***  <br>List of additional environment variables for memphis. | ""  | vars:  <br>\- name: KEY  <br>\- valye: value |
| memphis.tls.verify | **\*Optional\***  <br>For encrypted client-memphis communication. Verification for the CA autority. SSL. | ""  | `"true"` |
| memphis.tls.secret.name | **\*Optional\***  <br>For encrypted client-memphis communication.  <br>K8S secret name that holds the certs. SSL. | ""  | `"memphis-client-tls-secret"` |
| memphis.tls.cert | **\*Optional\***  <br>For encrypted client-memphis communication.  <br>.pem file to use. SSL. | ""  | `"memphis_client.pem"` |
| memphis.tls.key | **\*Optional\***  <br>For encrypted client-memphis communication.  <br>Private key file to use. SSL. | ""  | `"memphis-key_client.pem"` |
| memphis.tls.ca | **\*Optional\***  <br>For encrypted client-memphis communication.  <br>CA file to use. SSL. | ""  | `"rootCA.pem"` |
| websocket.tls.secret.name | **\*Optional\*** Memphis GUI using websockets for live rendering.  <br>K8S secret name for the certs | ""  | `"memphis-ws-tls-secret"` |
| websocket.tls.cert | **\*Optional\***  <br>Memphis GUI using websockets for live rendering.  <br>.pem file to use | ""  | `"memphis_local.pem"` |
| websocket.tls.key | **\*Optional\***  <br>Memphis GUI using websockets for live rendering.  <br>key file | ""  | `"memphis-key_local.pem"` |
| metadata.postgresql.username | **\*Optional\***  <br>Username for postgres db | "postgres" | "postgres" |
| metadata.pgpool.tls.enabled | **\*Optional\***  <br>Enabling TLS-based communication with PG | "false" | "false" |
| metadata.pgpool.tls.certificatesSecret | **\*Optional\***  <br>PG TLS cert secret to be used | ""  | "tls-secret" |
| metadata.pgpool.tls.certFilename | **\*Optional\***  <br>PG TLS cert file to be used | ""  | "tls.crt" |
| metadata.pgpool.tls.certKeyFilename | **\*Optional\***  <br>PG TLS key to be used | ""  | "tls.key" |
| metadata.pgpool.tls.certCAFilename | **\*Optional\***  <br>PG TLS cert CA to be used | ""  | "ca.crt" |
| metadata.external.enabled | **\*Optional\***  <br>For using external PG instead of deploying dedicated one for Memphis | "false" | "true" |
| metadata.external.dbTlsMutual | **\*Optional\***  <br>External PG TLS-basec communication | "true" | "true" |
| metadata.external.dbName | **\*Optional\***  <br>External PG db name | ""  | "memphis" |
| metadata.external.dbHost | **\*Optional\***  <br>External PG db hostname | ""  | "metadata.example.url" |
| metadata.external.dbPort | **\*Optional\***  <br>External PG db port | ""  | 5432 |
| metadata.external.dbUser | **\*Optional\***  <br>External PG db user | ""  | "postgres" |
| metadata.external.dbPass | **\*Optional\***  <br>External PG db password | ""  | "12345678" |
| metadata.external.secret.enabled | **\*Optional\***  <br>Enable an option to use secret for password store | "false" | "true" |
| metadata.external.secret.name | **\*Optional\***  <br>Secret name | ""  | "metadata-secret" |
| metadata.external.secret.dbPass_key | **\*Optional\***  <br>Name of the key in the secret | ""  | "dbPass" |
| restGateway.enabled | **\*Optional\***  <br>Memphis Rest Gateway can be disabled if not in use | "true" | "false" |
| restGateway.jwtSecret | **\*Optional\***  <br>Manual Jwt Token configurtion | ""  | ""  |
| restGateway.refreshJwtSecret | **\*Optional\***  <br>Manual Refresh Jwt Token configurtion | ""  | ""  |

Here is how to run an installation command with additional options -&#x20;

```
helm install memphis --set cluster.replicas=3,memphis.creds.rootPwd=rootpassword" memphis/memphis --create-namespace --namespace memphis
```

### Deployed pods

- **memphis.** Memphis broker.
- **memphis-rest-gateway.** Memphis REST Gateway.
- **memphis-metadata.** Metadata store.
- **memphis-metadata-coordinator.** Metadata coordinator

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
global.cluster.enabled="true",\
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

