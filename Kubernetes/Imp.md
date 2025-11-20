**Kubernetes SIG Network and the Security Response Committee announced they’re retiring the Ingress NGINX controller by March 2026.**

After that time, there will be no further releases, no bugfixes, and no updates to resolve any security vulnerabilities that may be discovered. The GitHub repositories will be made read-only and left available for reference.

What’s being retired is the Ingress NGINX controller. This is one specific Kubernetes project that uses NGINX under the hood to route external traffic into your cluster.

When you deploy an Ingress resource in Kubernetes, the Ingress NGINX controller reads that configuration and configures NGINX to handle the actual routing.

It’s the controller that’s retiring. The layer that sits between Kubernetes and NGINX. Not NGINX itself. Not the same thing.

Existing deployments of Ingress NGINX will not be broken. Existing project artifacts such as Helm charts and container images will remain available.

In most cases, you can check whether you use Ingress NGINX by running kubectl get pods \--all-namespaces \--selector app.kubernetes.io/name=ingress-nginx with cluster administrator permissions.

