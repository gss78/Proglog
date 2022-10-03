# Simple destributed storage service

It saves produced records to the file system and lets you consume them as tracking your offsets.


## The concepts and technologies:

* **Protobuf and gRPC** API definitions and communication with RPC.
* **SSL/TLS, mutual-TLS**  for encrypted data transfer, authentication, and authorization; securing the service from a zero-trust security perspective. Using Cloudflare CFSSL toolkit for signing, verifying, and bundling TLS certificates.
* **Observability** OpenCensus for metrics and traces, Uber Zap for structured logging
* **Server-to-Server service discovery** by HashiCorp Serf makes the distributed service instances aware of each other; it’s for building and managing a cluster membership.
* **Consensus** the distributed service is in a leader-follower structure. The leader accepts writes and replicate them to followers, which are used for reading. HashiCorp Raft implementation is used.
* **Load-balancing** Implementation of custom gRPC client-side load balancing. Clients discovers server instances and know which is the leader and followers.
* **Deployment** the service to a local Kubernetes cluster. Kind(Kubernetes in Docker), Kubernetes StatefulSets, and Helm are used.
