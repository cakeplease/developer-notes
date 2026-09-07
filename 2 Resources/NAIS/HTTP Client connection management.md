
## Why is this important?  

HTTP clients typically reuse TCP connections from a connection pool to avoid performing a new TCP/TLS handshake for every request. This improves performance and reduces latency. However, in a Kubernetes-based platform like NAIS, connection reuse can cause subtle reliability issues if the client is not configured correctly.

## Problem 1: Idle Connections Are Silently Dropped

Firewalls, load balancers, and NAT gateways often remove connections that have been idle for too long. The problem is that these connections are frequently dropped without sending a TCP FIN or RST signal. The client therefore believes the connection is still valid and attempts to reuse it.

This can result in errors such as:  
- `Connection reset`  
- `Unexpected end of stream`  

These failures often appear only after periods of low traffic.

### Recommended Solution  
- Configure a **Connection TTL (Time To Live)** shorter than the shortest idle timeout in the network path.  
- Enable **background eviction** so stale connections are removed proactively.  

Using a very short request timeout does **not** solve this issue. Request timeouts and connection lifecycle management are separate concerns. 

## Problem 2: DNS Caching and Pod Rotation
Services running on NAIS have a DNS TTL of approximately **30 seconds** because pod IP addresses can change whenever pods are:  
- Restarted  
- Rescheduled
- Scaled
- Redeployed  

Clients are expected to periodically re-resolve DNS names and connect to the new pod addresses. 
### Challenges  
1. The JVM caches DNS entries for a long time (indefinitely by default). 
2. Existing pooled connections remain bound to the IP address they originally connected to.  

As a result, a client may continue trying to communicate with pods that no longer exist. 

### Recommended Solution  
- Set `networkaddress.cache.ttl` to roughly **30 seconds**.  
- Configure a **Connection TTL** so connections are periodically recreated and new DNS lookups occur.  
## Special Case: On-Prem Services (FSS)  
For traffic going from GCP to on-prem FSS services, the firewall in front of `*.fss-pub.nais.io` drops idle connections after **60 minutes** without notifying either side. Applications communicating with these services should:  

- Set connection TTL below 60 minutes (55 minutes is recommended).  
- Enable background eviction.  
- 
## Key Takeaways

When developing applications on NAIS, you should:  

- Use connection pooling.  
- Set a reasonable connection TTL.  
- Enable background eviction of stale connections.  
- Respect DNS TTL values.  
- Expect pods and IP addresses to change over time.  

### Simple Rule of Thumb  
> A connection pool without TTL and eviction will eventually try to reuse dead connections.  

> Configure both connection lifetime management and DNS refresh correctly to make your application resilient in a Kubernetes/NAIS environment. 