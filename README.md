# Istio



### Traffic in any cluster 
North South traffic:
From external to Ingress controller that is protected by adding certificate at ingress or Load balancer level. An Tls certificate is attached there and the TLS is terminated at ingress level.

East West traffic:
Between the micro services inside the cluster.
If micro service 1 has to talk to micro service 2 , that traffic also should be encrypted and secured.

For that concept of mutual TLS has to be implemented, every pod of every application will have an TLS cert Attatched to that and communication internally is secured.

HOW??

Istio does that work for us....when the istio is installed it communicates with api server and gets the details of pods being deployed and also the new pods in place. For new pods also istio provide the TLS certs.

SIDECAR CONTAINER:
ENVOY PROXY ON EACH POD

it creates an SIDECAR CONTAINER on every pods and the SIDECAR container manages everything.
It eliminates the need to alter application code and requirements on developer to create the clumsiness and handle certs also.
It attachees envoy proxy onto every SIDECAR container.

MTLS :
Any traffic hitting the pod first ,goes through side car and there TLS is verified and response from that pod again goes via side car proxy.

Then from sidecar pod1 to it goes to SIDECAR pod2..and once it's authorised goes to pod2 within.

CANARY:
Istio also can handle canary or distribution of traffic weighted to new version.

ISTioD:


### Admission Controllers
It will talk to apiserver and gets info of any new pods requested to be created.
It will give info to istio and it takes care of creating SIDECAR container on new pods incoming.


Admission controllers in Kubernetes enforce policies on objects during their creation or modification. They intercept requests to the Kubernetes API server before objects are persisted and can modify or deny requests based on predefined rules.

### Sidecar Containers

In Kubernetes, sidecar containers are auxiliary containers that run alongside the main application container within the same pod. They enhance or extend the functionality of the main container, such as handling networking, logging, or monitoring tasks.

### What is a Service Mesh?

A service mesh is a dedicated infrastructure layer for handling service-to-service communication within a distributed application. It provides features like traffic management, observability, security, and resilience without requiring changes to the application code.

### Why do you need a Service Mesh?

Service meshes address challenges in managing microservices architectures by offering centralized control over communication, improving reliability through features like circuit breaking and retries, enhancing security with mutual TLS, and providing visibility into service interactions.

### Traffic Management

Traffic management in a service mesh involves controlling the flow of requests between services. This includes features such as load balancing, routing, traffic shaping, and fault tolerance mechanisms like retries and circuit breaking.

### Virtual Services

Virtual services in Istio define how incoming requests to a service should be routed to different versions or subsets of that service. They enable sophisticated traffic management strategies like A/B testing and canary deployments.

### Destination Rules

Destination rules in Istio configure the traffic policies applied to the traffic destined for a particular service version or subset. They define things like load balancing algorithms, circuit breaking settings, and TLS settings for communication between services.

### Circuit Breaking

Circuit breaking is a pattern used to prevent cascading failures in distributed systems. In Istio, it involves setting thresholds for error rates or latency, and if these thresholds are exceeded, requests to a service are automatically stopped, preventing further damage.

### mTLS (Mutual TLS)

Mutual TLS in Istio ensures secure communication between services by requiring both the client and the server to present a valid TLS certificate. It encrypts traffic and provides authentication, preventing unauthorized access or eavesdropping.

### Gateways

Gateways in Istio allow external traffic to enter the service mesh. They act as ingress and egress points for traffic, enabling communication between services inside the mesh and external clients or services outside the mesh.

### Observability

Observability in a service mesh refers to the ability to monitor, trace, and analyze the behavior and performance of services. It includes features like distributed tracing, metrics collection, and logging to provide insights into the health and operation of the system.

### Service Mesh vs Ingress

A service mesh operates at the layer of service-to-service communication within a cluster, providing features like traffic management, security, and observability. In contrast, an ingress controller manages external access to services within the cluster, typically handling tasks like load balancing, SSL termination, and routing based on HTTP/HTTPS requests.


