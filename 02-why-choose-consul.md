# Why Choose Consul

---

## Overview

HashiCorp Consul is a service networking platform that encompasses multiple capabilities to secure and simplify network service management. These capabilities include service mesh, service discovery, configuration management, and API gateway functionality. While competing products offer a few of these core capabilities, Consul is developed to address all four. The topics in this section provide a general overview of how Consul’s capabilities compare to some other tools on the market. Visit the following pages to read more about how:

- [Consul compares with other service meshes](https://developer.hashicorp.com/consul/docs/consul-vs-other/service-mesh-compare)
- [Consul compares with other DNS tools](https://developer.hashicorp.com/consul/docs/consul-vs-other/dns-tools-compare)
- [Consul compares with other configuration management tools](https://developer.hashicorp.com/consul/docs/consul-vs-other/config-management-compare)
- [Consul compares with other API Gateways](https://developer.hashicorp.com/consul/docs/consul-vs-other/api-gateway-compare)

## Consul compared to other service mesh software

**Examples**: Istio, Solo Gloo Mesh, Linkerd, Kong/Kuma, AWS App Mesh

Consul’s service mesh allows organizations to securely connect and manage their network services across multiple different environments. Using Envoy as the sidecar proxy attached to every service, Consul ensures that all service-to-service communication is authorized, authenticated, and encrypted. Consul includes traffic management capabilities like load balancing and traffic splitting, which help developers perform canary testing, A/B tests, and blue/green deployments. Consul also includes health check and observability features.

Consul is platform agnostic — it supports any runtime (Kubernetes, EKS, AKS, GKE, VMs, ECS, Lambda, Nomad) and any cloud provider (AWS, Microsoft Azure, GCP, private clouds). This makes it one of the most flexible service discovery and service mesh platforms. While other service mesh software provides support for multiple runtimes for the data plane, they require you to run the control plane solely on Kubernetes. With Consul, you can run both the control plane and data plane in different runtimes.

Consul also has several unique integrations with Vault, an industry standard for secrets management. Operators have the option to use Consul’s built-in certificate authority, or leverage Vault’s PKI engine to generate and store TLS certificates for both the data plane and control plane. In addition, Consul can automatically rotate the TLS certificates on both the data plane and control plane without requiring any type of restarts. This lets you rotate the certificates more frequently without incurring additional management burden on operators. When deploying Consul on Kubernetes, you can store sensitive data including licenses, ACL tokens, and TLS certificates centrally in Vault instead of Kubernetes secrets. Vault is much more secure than Kubernetes secrets because it automatically encrypts all data, provides advanced access controls to secrets, and provides centralized governance for all secrets.

---

## Consul Compared to Other DNS Tools

**Examples**: NS1, AWS Route53, AzureDNS, Cloudflare DNS

Consul was originally designed as a centralized service registry for any cloud environment that dynamically tracks services as they are added, changed, or removed within a compute infrastructure. Consul maintains a catalog of these registered services and their attributes, such as IP addresses or service name. For more information, refer to [What is Service Discovery?](https://developer.hashicorp.com/consul/docs/concepts/service-discovery).

As a result, Consul can also provide basic DNS functionality, including [lookups, alternate domains, and access controls](https://developer.hashicorp.com/consul/docs/services/discovery/dns-overview). Since Consul is platform agnostic, you can retrieve service information across both cloud and on-premises data centers. Consul does not natively support some advanced DNS capabilities, such as filters or advanced routing logic. However, you can integrate Consul with existing DNS solutions, such as [NS1](https://help.ns1.com/hc/en-us/articles/360039417093-NS1-Consul-Integration-Overview) and [DNSimple](https://blog.dnsimple.com/2022/05/consul-integration/), to support these advanced capabilities.

---

## Consul Compared to Other Configuration Management Tools

**Examples**: Chef, Puppet

There are many configuration management tools, however, they typically focus on static provisioning. Consul enables you to dynamically configure your services based on service and node state. Both static and dynamic configuration are important and work well together. Since Consul offers a number of different capabilities, there are times when its functionality overlaps with other configuration management tools.

For example, Chef and Puppet are configuration management tools that can build service discovery mechanisms. However, they only support configuration information that is static. As a result, the time it takes to implement updates depends on the frequency of conversion runs (several minutes to hours). Additionally, these tools do not let you incorporate the system state in the configuration. This could lead to load balancers sending traffic to unhealthy nodes, further exacerbating issues. Supporting multiple datacenters is also challenging with these tools, since a central group of servers must manage all datacenters.

Consul's service discovery layer is specifically designed to dynamically track and respond to your service's state. By using the integrated health checking, Consul can route traffic away from unhealthy nodes, allowing systems and services to gracefully recover. In addition, Consul’s service discovery layer works with Terraform. Consul-Terraform-Sync (CTS) automates updates to network infrastructure based on dynamic changes to each service. For example, as services scale up or down, CTS can trigger Terraform to update firewalls or load balancers to reflect the latest changes. Also, since each datacenter runs independently, supporting multiple datacenters is no different than supporting a single datacenter.

Consul is not a replacement for other configuration management tools. These tools are still critical for setting up applications, including Consul. Static provisioning is best managed by existing tools, while Consul enables you to leverage dynamic configuration and service discovery.

By separating configuration management and cluster management tools, you can take advantage of simpler workflows:

- Periodic runs are no longer required for service or configuration changes.
- Chef recipes and Puppet manifests are simpler because they do not require a global state.
- Infrastructure can become immutable because configuration management runs do not require global state.

---

## Consul Compared to Other API Gateways

**Examples**: Kong Gateway, Apigee, Mulesoft, Gravitee

The [Consul API Gateway](https://developer.hashicorp.com/consul/docs/api-gateway) is an implementation of the [Kubernetes Gateway API](https://gateway-api.sigs.k8s.io/). Traditionally, API gateways are used for two things: _client traffic management_ and _API lifecycle management_.

Client traffic management refers to an API gateway's role in controlling the point of entry for public traffic into a given environment, also known as _managing north-south traffic_. The Consul API Gateway is deployed alongside Consul service mesh and is responsible for routing inbound client requests to the mesh based on defined routes. For a full list of supported traffic management features, refer to the [Consul API Gateway documentation](https://developer.hashicorp.com/consul/docs/api-gateway).

API lifecycle management refers to how application developers use an API gateway to deploy, iterate, and manage versions of an API. At this time, the Consul API Gateway does not support API lifecycle management.
