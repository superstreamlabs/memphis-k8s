## Memphis.dev
**[Memphis{dev}](https://memphis.dev)** is an open-source real-time data processing platform<br>
that provides end-to-end support for in-app streaming use cases using Memphis distributed message broker.<br>
Memphis' platform requires zero ops, enables rapid development, extreme cost reduction, <br>
eliminates coding barriers, and saves a great amount of dev time for data-oriented developers and data engineers.

## ⭐️ Why
Working with data streaming is HARD.<br>

As a developer, you need to build a dedicated pipeline for each data source,<br>
work with schemas, formats, serializations, analyze each source individually,<br>
enrich the data with other sources, constantly change APIs, and scale for better performance 🥵.<br>
Besides that, it constantly crashes and requires adaptation to different rate limits.<br>
**It takes time and resources that you probably don't have.**<br>

Message broker acts as the middleman and supports streaming architecture,<br>
but then you encounter Apache Kafka and its documentation and run back to the monolith and batch jobs.<br>
**Give memphis{dev} a spin before.**

## 👉 Use-cases
- Async task management
- Real-time streaming pipelines
- Data ingestion
- Cloud Messaging
  - Services (microservices, service mesh)
  - Event/Data Streaming (observability, analytics, ML/AI)
- Queuing
- N:N communication patterns

## ✨ Features

[**Roadmap**](https://github.com/orgs/memphisdev/projects/2/views/1)


## 🚀 Getting Started
[Sandbox](https://sandbox.memphis.dev)<br>
[Installation videos](https://www.youtube.com/playlist?list=PL_7iYjqhtXpWpZT2U0zDYo2eGOoGmg2mm)<br><br>
Helm for Kubernetes☸
```shell
helm repo add memphis https://k8s.memphis.dev/charts/ --force-update && \
helm install my-memphis memphis/memphis --create-namespace --namespace memphis
```
Docker🐳 Compose
```shell
curl -s https://memphisdev.github.io/memphis-docker/docker-compose.yml -o docker-compose.yml && \
docker compose -f docker-compose.yml -p memphis up
```

## Local access
### Via Kubernetes
```shell
To access Memphis using UI/CLI/SDK from localhost, run the below commands:

  - kubectl port-forward service/memphis-cluster 6666:6666 9000:9000 7770:7770 --namespace memphis > /dev/null &

For interacting with the broker via HTTP:

  - kubectl port-forward service/memphis-rest-gateway 4444:4444 --namespace memphis > /dev/null &

Dashboard/CLI: http://localhost:9000
Broker: localhost:6666 (Client Connections)
REST Gateway: localhost:4444 (Data + Mgmt)
```

**For Production Environments**
Please expose the UI, Cluster, and Control-plane via k8s ingress / load balancer / nodeport

### Via Docker
```shell
Dashboard/CLI: http://localhost:9000
Broker: localhost:6666
```

## Beta
Memphis{dev} is currently in Beta version. This means that we are still working on essential features like real-time messages tracing, schema registry and inline processing as well as making more SDKs and supporting materials.

How does it affect you? Well... mostly it doesn't.<br>
(a) The core of memphis broker is highly stable<br>
(b) We learn and fix fast<br><br>
But we need your love, and any help we can get by stars, PR, feedback, issues, and enhancements.<br>
Read more on [Memphis{dev} Documentation 📃](https://memphis.dev/docs).

## Support 🙋‍♂️🤝

### Ask a question ❓ about Memphis{dev} or something related to us:

We welcome you to our discord server with your questions, doubts and feedback.

<a href="https://discord.gg/WZpysvAeTf"><img src="https://amplication.com/images/discord_banner_purple.svg"/></a>

### Create a bug 🐞 report

If you see an error message or run into an issue, please [create bug report](https://github.com/memphisdev/memphis-broker/issues/new?assignees=&labels=type%3A%20bug&template=bug_report.md&title=). This effort is valued and it will help all Memphis{dev} users.


### Submit a feature 💡 request 

If you have an idea, or you think that we're missing a capability that would make development easier and more robust, please [Submit feature request](https://github.com/memphisdev/memphis-broker/issues/new?assignees=&labels=type%3A%20feature%20request).

If an issue❗with similar feature request already exists, don't forget to leave a "+1".
If you add some more information such as your thoughts and vision about the feature, your comments will be embraced warmly :)

## Contributing

Memphis{dev} is an open-source project.<br>
We are committed to a fully transparent development process and appreciate highly any contributions.<br>
Whether you are helping us fix bugs, proposing new features, improving our documentation or spreading the word - we would love to have you as part of the Memphis{dev} community.

Please refer to our [Contribution Guidelines](./CONTRIBUTING.md) and [Code of Conduct](./CODE_OF_CONDUCT.md).

## License 📃
Memphis is open-sourced and operates under the "Memphis Business Source License 1.0" license
Built out of Apache 2.0, the main difference between the licenses is:
"You may make use of the Licensed Work (i) only as part of your own product or service, provided it is not a message broker or a message queue product or service; and (ii) provided that you do not use, provide, distribute, or make available the Licensed Work as a Service. A “Service” is a commercial offering, product, hosted, or managed service, that allows third parties (other than your own employees and contractors acting on your behalf) to access and/or use the Licensed Work or a substantial set of the features or functionality of the Licensed Work to third parties as a software-as-a-service, platform-as-a-service, infrastructure-as-a-service or other similar services that compete with Licensor products or services."
Please check out [License](./LICENSE) to read the full text.
