# Liqo Resources Dashboard

*Liqo peering dashboard* is an open-source, web-based dashboard that exposes the status of the peerings established with the current cluster, and the number of resources (i.e., in terms of vCPUs and Memory) used by each liqo peer.

![Preview](./doc/images/screenshot.png)

## Prerequisites

Since the dashboard shows data related to Liqo you must have it installed in your cluster. If you want to start using Liqo, you can check the [official documentation](https://docs.liqo.io/en/stable/) and the [quick start tutorial](https://docs.liqo.io/en/stable/examples/quick-start.html).

To install this dashboard you should have helm installed on your machine. You can find more about helm on the [official site](https://helm.sh/). You can also decide to avoid helm but in this case, you need to write down all the required YAML manifests.

Additionally, this dashboard needs to be deployed in a cluster that has an ingress controller installed. To learn more about ingress controller you can read the [official Kubernetes documentation](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/).

## Deployment

The dashboard is divided into two components, a *frontend* and a *backend*, which are executed as separate pods. You can deploy them through helm, once you cloned the current repository:

```bash
helm install liqo-dashboard ./chart
```

The command above deploys a few resources into the cluster in the `liqo-dashboard` namespace.

When the dashboard is deployed on a production environment, you shall configure the appropriate ingress hostname, rather than using the default catch-all wildcard:

```bash
helm install liqo-dashboard --set host=<<host_here>> ./chart --namespace <<namespace_name>> --create-namespace
```

Additionally, if you want to use TLS encryption to enable HTTPS you should set tls.secretName as follows

```bash
helm install liqo-dashboard --set host=<<host_here>> --tls.secretName=<<certificate_secret_here>> ./chart --namespace <<namespace_name>> --create-namespace
```

Note that the secret should already exist or cert-manager shall be present (and consequently the annotation must be declared for the ingress).

You can find the complete list of additional values [here](./chart/README.md).

## Contributing

All contributors are excitedly welcome. If you notice a bug you can open an issue to let us know or you can figure out how to fix it and open a pull request.
