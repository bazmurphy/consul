# Core Concepts

---

## What is service discovery?

_Service discovery_ helps you discover, track, and monitor the health of services within a network. Service discovery registers and maintains a record of all your services in a _service catalog_ . This service catalog acts as a single source of truth that allows your services to query and communicate with each other.

## Benefits of service discovery

Service discovery provides benefits for all organizations, ranging from simplified scalability to improved application resiliency. Some of the benefits of service discovery include:

- Dynamic IP address and port discovery
- Simplified horizontal service scaling
- Abstracts discovery logic away from applications
- Reliable service communication ensured by health checks
- Load balances requests across healthy service instances
- Faster deployment times achieved by high-speed discovery
- Automated service registration and de-registration

## How does service discovery work?

Service discovery uses a service's identity instead of traditional access information (IP address and port). This allows you to dynamically map services and track any changes within a service catalog. Service consumers (users or other services) then use DNS to dynamically retrieve other service's access information from the service catalog. The lifecycle of a service may look like the following:

A service consumer communicates with the "Web" service via a unique Consul DNS entry provided by the service catalog.

![Example diagram of how service consumers query for services](images/service-discovery-01.avif)

A new instance of the "Web" service registers itself to the service catalog with its IP address and port. As new instances of your services are registered to the service catalog, they will participate in the load balancing pool for handling service consumer requests.

![Example diagram of how a service is registered to the service catalog](images/service-discovery-02.avif)

The service catalog is dynamically updated as new instances of the service are added and legacy or unhealthy service instances are removed. Removed services will no longer participate in the load balancing pool for handling service consumer requests.

![Example diagram of how unhealthy services are removed from the service catalog](images/service-discovery-03.avif)

## What is service discovery in microservices?

In a microservices application, the set of active service instances changes frequently across a large, dynamic environment. These service instances rely on a service catalog to retrieve the most up-to-date access information from the respective services. A reliable service catalog is especially important for service discovery in microservices to ensure healthy, scalable, and highly responsive application operation.

## What are the two main types of service discovery?

There are two main service‑discovery patterns: _client-side_ discovery and _server-side_ discovery.

In systems that use client‑side discovery, the service consumer is responsible for determining the access information of available service instances and load balancing requests between them.

1.  The service consumer queries the service catalog
2.  The service catalog retrieves and returns all access information
3.  The service consumer selects a healthy downstream service and makes requests directly to it

![Example diagram of client-side discovery concept](images/service-discovery-04.avif)

In systems that use server‑side discovery, the service consumer uses an intermediary to query the service catalog and make requests to them.

1.  The service consumer queries an intermediary (Consul)
2.  The intermediary queries the service catalog and routes requests to the available service instances.

![Example diagram of server-side discovery concept](images/service-discovery-05.avif)

For modern applications, this discovery method is advantageous because developers can make their applications faster and more lightweight by decoupling and centralizing service discovery logic.

## Service discovery vs load balancing

Service discovery and load balancing share a similarity in distributing requests to back end services, but differ in many important ways.

Traditional load balancers are not designed for rapid registration and de-registration of services, nor are they designed for high-availability. By contrast, service discovery systems use multiple nodes that maintain the service registry state and a peer-to-peer state management system for increased resilience across any type of infrastructure.

For modern, cloud-based applications, service discovery is the preferred method for directing traffic to the right service provider due to its ability to scale and remain resilient, independent of infrastructure.

## How do you implement service discovery?

You can implement service discovery systems across any type of infrastructure, whether it is on-premise or in the cloud. Service discovery is a native feature of many container orchestrators such as Kubernetes or Nomad. There are also platform-agnostic service discovery methods available for non-container workloads such as VMs and serverless technologies. Implementing a resilient service discovery system involves creating a set of servers that maintain and facilitate service registry operations. You can achieve this by installing a service discovery system or using a managed service discovery service.

## What is Consul?

Consul is a service networking solution that lets you automate network configurations, discover services, and enable secure connectivity across any cloud or runtime. With these features, Consul helps you solve the complex networking and security challenges of operating microservices and cloud infrastructure (multi-cloud and hybrid cloud). You can use these features independently or together to achieve [zero trust](https://www.hashicorp.com/solutions/zero-trust-security) security.

Consul's service discovery capabilities help you discover, track, and monitor the health of services within a network. Consul acts as a single source of truth that allows your services to query and communicate with each other.

You can use Consul with virtual machines (VMs), containers, serverless technologies, or with container orchestration platforms, such as [Nomad](https://www.nomadproject.io/) and Kubernetes. Consul is platform agnostic which makes it a great fit for all environments, including legacy platforms.

Consul is available as a [self-managed](https://developer.hashicorp.com/consul/downloads) project or as a fully managed service mesh solution ([HCP Consul Dedicated](https://portal.cloud.hashicorp.com/sign-in?utm_source=consul_docs)). HCP Consul Dedicated enables users to discover and securely connect services without the added operational burden of maintaining a service mesh on their own.

## Next steps

Get started with service discovery today by leveraging Consul on HCP, Consul on Kubernetes, or Consul on VMs. Prepare your organization for the future of multi-cloud and embrace a [zero-trust](https://www.hashicorp.com/solutions/zero-trust-security) architecture.

Feel free to get started with Consul by exploring one of these Consul tutorials:

- [Get Started with Consul on VMs](https://developer.hashicorp.com/consul/tutorials/get-started-vms)
- [Get Started with Consul on HCP](https://developer.hashicorp.com/consul/tutorials/get-started-hcp)
- [Get Started with Consul on Kubernetes](https://developer.hashicorp.com/consul/tutorials/get-started-kubernetes)

---

## What is a service mesh?

A _service mesh_ is a dedicated network layer that provides secure service-to-service communication within and across infrastructure, including on-premises and cloud environments. Service meshes are often used with a microservice architectural pattern, but can provide value in any scenario where complex networking is involved.

## Benefits of a service mesh

A service mesh provides benefits for all organizations, ranging from security to improved application resiliency. Some of the benefits of a service mesh include;

- service discovery
- application health monitoring
- load balancing
- automatic failover
- traffic management
- encryption
- observability and traceability
- authentication and authorization
- network automation

A common use case for leveraging a service mesh is to achieve a [_zero trust_ model](https://www.consul.io/use-cases/zero-trust-networking). In a zero trust model, applications require identity-based access to ensure all communication within the service mesh is authenticated with TLS certificates and encrypted in transit.

In traditional security strategies, protection is primarily focused at the perimeter of a network. In cloud environments, the surface area for network access is much wider than the traditional on-premises networks. In addition, traditional security practices overlook the fact that many bad actors can originate from within the network walls. A zero trust model addresses these concerns while allowing organizations to scale as needed.

## How does a service mesh work?

A service mesh typically consist of a control plane and a data plane. The control plane maintains a central registry that keeps track of all services and their respective IP addresses. This activity is called [service discovery](https://www.hashicorp.com/products/consul/service-discovery-and-health-checking). As long as the application is registered with the control plane, the control plane will be able to share with other members of the mesh how to communicate with the application and enforce rules for who can communicate with each other.

The control plane is responsible for securing the mesh, facilitating service discovery, health checking, policy enforcement, and other similar operational concerns.

The data plane handles communication between services. Many service mesh solutions employ a sidecar proxy to handle data plane communications, and thus limit the level of awareness the services need to have about the network environment.

![Overview of a service mesh](images/what-is-service-mesh.avif)

## API gateway vs service mesh

An API gateway is a centralized access point for handling incoming client requests and delivering them to services. The API gateway acts as a control plane that allows operators and developers to manage incoming client requests and apply different handling logic depending on the request. The API gateway will route the incoming requests to the respective service. The primary function of an API gateway is to handle requests and return the reply from the service back to the client.

A service mesh specializes in the network management of services and the communication between services. The mesh is responsible for keeping track of services and their health status, IP address, and traffic routing and ensuring all traffic between services is authenticated and encrypted. Unlike some API gateways, a service mesh will track all registered services' lifecycle and ensure requests are routed to healthy instances of the service. API gateways are frequently deployed alongside a load balancer to ensure traffic is directed to healthy and available instances of the service. The mesh reduces the load balancer footprint as routing responsibilities are handled in a decentralized manner.

API gateways can be used with a service mesh to bridge external networks (non-mesh) with a service mesh.

**API gateways and traffic direction:** API gateways are often used to accept north-south traffic. North-south traffic is networking traffic that either enters or exits a datacenter or a virtual private network (VPC). You can connect API gateways to a service mesh and provide access to it from outside the mesh. A service mesh is primarily used for handling east-west traffic. East-west traffic traditionally remains inside a data center or a VPC. A service mesh can be connected to another service mesh in another data center or VPC to form a federated mesh.

## What problems does a service mesh solve?

Modern infrastructure is transitioning from being primarily static to dynamic in nature (ephemeral). This dynamic infrastructure has a short life cycle, meaning virtual machines (VM) and containers are frequently recycled. It's difficult for an organization to manage and keep track of application services that live on short-lived resources. A service mesh solves this problem by acting as a central registry of all registered services. As instances of a service (e.g., VM, container, serverless functions) come up and down, the mesh is aware of their state and availability. The ability to conduct _service discovery_ is the foundation to the other problems a service mesh solves.

As a service mesh is aware of the state of a service and its instances, the mesh can implement more intelligent and dynamic network routing. Many service meshes offer L7 traffic management capabilities. As a result, operators and developers can create powerful rules to direct network traffic as needed, such as load balancing, traffic splitting, dynamic failover, and custom resolvers. A service mesh's dynamic network behavior allows application owners to improve application resiliency and availability with no application changes.

Implementing dynamic network behavior is critical as more and more applications are deployed across different cloud providers (multi-cloud) and private data centers. Organizations may need to route network traffic to other infrastructure environments. Ensuring this traffic is secure is on top of mind for all organizations. Service meshes offer the ability to enforce network traffic encryption (mTLS) and authentication between all services. The service mesh can automatically generate an SSL certificate for each service and its instances. The certificate authenticates with other services inside the mesh and encrypts the TCP/UDP/gRPC connection with SSL.

Fine-grained policies that dictate what services are allowed to communicate with each other is another benefit of a service mesh. Traditionally, services are permitted to communicate with other services through firewall rules. The traditional firewall (IP-based) model is difficult to enforce with dynamic infrastructure resources with a short lifecycle and frequently recycling IP addresses. As a result, network administrators have to open up network ranges to permit network traffic between services without differentiating the services generating the network traffic. However, a service mesh allows operators and developers to shift away from an IP-based model and focus more on service to service permissions. An operator defines a policy that only allows _service A_ to communicate with _service B_. Otherwise, the default action is to deny the traffic. This shift from an IP address-based security model to a service-focused model reduces the overhead of securing network traffic and allows an organization to take advantage of multi-cloud environments without sacrificing security due to complexity.

## How do you implement a service mesh?

Service meshes are commonly installed in Kubernetes clusters. There are also platform-agnostic service meshes available for non-Kubernetes-based workloads. For Kubernetes, most service meshes can be installed by operators through a [Helm chart](https://helm.sh/). Additionally, the service mesh may offer a CLI tool that supports the installation and maintenance of the service mesh. Non-Kubernetes based service meshes can be installed through infrastructure as code (IaC) products such as [Terraform](https://www.terraform.io/), CloudFormation, ARM Templates, Puppet, Chef, etc.

## What is a multi platform service mesh?

A multi-platform service mesh is capable of supporting various infrastructure environments. This can range from having the service mesh support Kubernetes and non-Kubernetes workloads, to having a service mesh span across various cloud environments (multi-cloud and hybrid cloud).

## What is Consul?

Consul is a multi-networking tool that offers a fully-featured service mesh solution that solves the networking and security challenges of operating microservices and cloud infrastructure (multi-cloud and hybrid cloud). Consul offers a software-driven approach to routing and segmentation. It also brings additional benefits such as failure handling, retries, and network observability. Each of these features can be used individually as needed or they can be used together to build a full service mesh and achieve [zero trust](https://www.hashicorp.com/solutions/zero-trust-security) security. In simple terms, Consul is the control plane of the service mesh. The data plane is supported by Consul through its first class support of [Envoy](https://www.envoyproxy.io/) as a proxy.

You can use Consul with virtual machines (VMs), containers, or with container orchestration platforms, such as [Nomad](https://www.nomadproject.io/) and Kubernetes. Consul is platform agnostic which makes it a great fit for all environments, including legacy platforms.

Consul is available as a [self-install](https://developer.hashicorp.com/consul/downloads) project or as a fully managed service mesh solution called [HCP Consul Dedicated](https://portal.cloud.hashicorp.com/sign-in?utm_source=consul_docs). HCP Consul Dedicated enables users to discover and securely connect services without the added operational burden of maintaining a service mesh on their own.

You can learn more about Consul by visiting the Consul [tutorials](https://developer.hashicorp.com/consul/tutorials).

## Next

Get started today with a service mesh by leveraging [HCP Consul Dedicated](https://portal.cloud.hashicorp.com/sign-in?utm_source=consul_docs). Prepare your organization for the future of multi-cloud and embrace a [zero-trust](https://www.hashicorp.com/solutions/zero-trust-security) architecture.
