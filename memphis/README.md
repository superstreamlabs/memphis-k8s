### Probably the easiest message broker in the world.

**[Memphis{dev}](https://memphis.dev)** is a modern replacement for Apache Kafka.<br>A message broker for developers made out of devs' struggles with using message brokers,<br>building complex data/event-driven apps, and troubleshooting them.<br><br>Allowing developers to achieve all other message brokers' benefits in a fraction of the time.<br>

# Features
**Current**
- Fully optimized message broker in under 3 minutes
- Easy-to-use UI, CLI, and SDKs
- Data-level observability
- Runs on your Docker or Kubernetes

**Coming soon**
- Embedded schema registry using dbt
- Message Journey - Real-time messages tracing
- More SDKs
- Inline processing
- Ready-to-use connectors and analysis functions

# Getting Started
[Watch this installation videos](https://www.youtube.com/playlist?list=PL_7iYjqhtXpWpZT2U0zDYo2eGOoGmg2mm)<br><br>
Helm for Kubernetes
```shell
helm repo add memphis https://k8s.memphis.dev/charts/ && \
helm install my-memphis memphis/memphis --create-namespace --namespace memphis
```
Docker Compose
```shell
curl -s https://memphisdev.github.io/memphis-docker/docker-compose.yml -o docker-compose.yml && \
docker compose -f docker-compose.yml -p memphis up
```

[Connect your 1st app here](https://medium.com/memphis-dev/how-to-build-your-own-wolt-app-b220d738bb71)

# High-Level Architecture
<img alt="memphis.dev-logo" height="500" alt="memphis.dev Architecture" src="https://memphis-public-files.s3.eu-central-1.amazonaws.com/graphics+for+github/Architecture.png">

# Local access
### Via Kubernetes
```shell
To access Memphis UI from localhost, run the below commands:
  1. kubectl port-forward service/memphis-ui 9000:80 --namespace memphis > /dev/null &

To access Memphis using CLI or SDK from localhost, run the below commands:
  2. kubectl port-forward service/memphis-cluster 7766:7766 6666:6666 5555:5555 --namespace memphis > /dev/null &

Dashboard: http://localhost:9000
Memphis broker: localhost:5555 (Management Port) / 7766 (Data Port) / 6666 (TCP Port)
```
**For Production Environments**
Please expose the UI, Cluster, and Control-plane via k8s ingress / load balancer / nodeport

### Via Docker
Dashboard - http://localhost:9000<br>
Broker - localhost:7766<br>
Control-Plane - localhost:5555/6666<br>

# Beta
Memphis{dev} is currently in Beta version. This means that we are still working on essential features like real-time messages tracing,<br>
Schema registry, and inline processing, as well as making more SDKs and supporting materials.

How does it affect you? Well... mostly it doesn't.<br>
(a) The core of memphis broker is highly stable<br>
(b) We learn&fix fast<br><br>
But we need your love, and any help we can get by stars, PR, feedback, issues, and enhancments.<br>
Read more on https://memphis.dev/docs

# Support

## Ask a question about Memphis{dev} or related

You can ask questions, and participate in discussions about Memphis{dev}-related topics in the Memphis Discord channel.

<a href="https://discord.gg/WZpysvAeTf"><img src="https://amplication.com/images/discord_banner_purple.svg" /></a>

## Create a bug report

If you see an error message or run into an issue, please [create bug report](https://github.com/memphisdev/memphis-broker/issues/new?assignees=&labels=type%3A%20bug&template=bug_report.md&title=). This effort is valued and it will help all Memphis{dev} users.


## Submit a feature request

If you have an idea, or you're missing a capability that would make development easier and more robust, please [Submit feature request](https://github.com/memphisdev/memphis-broker/issues/new?assignees=&labels=type%3A%20feature%20request).

If a similar feature request already exists, don't forget to leave a "+1".
If you add some more information such as your thoughts and vision about the feature, your comments will be embraced warmly :)

# Contributing

Memphis{dev} is an open-source project.<br>
We are committed to a fully transparent development process and appreciate highly any contributions.<br>
Whether you are helping us fix bugs, proposing new features, improving our documentation or spreading the word - <br>we would love to have you as part of the Memphis{dev} community.

Please refer to our [Contribution Guidelines](./CONTRIBUTING.md) and [Code of Conduct](./code_of_conduct.md).
