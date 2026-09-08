<!-- llm-readme-management spec=1 commit=69e45d6ea8e7f93045991c273c7a1a5dc8df66b3 template=helm model=qwen3.6-35b-a3b digest=5b6cfbe96d9f generated=2026-09-08T21:28:22Z -->
<a href="https://hauke.cloud" target="_blank"><img src="https://img.shields.io/badge/home-hauke.cloud-brightgreen" alt="hauke.cloud" style="display: block;" /></a>
<a href="https://github.com/hauke-cloud" target="_blank"><img src="https://img.shields.io/badge/github-hauke.cloud-blue" alt="hauke.cloud Github Organisation" style="display: block;" /></a>
<a href="https://github.com/hauke-cloud/llm-readme-management" target="_blank"><img src="https://img.shields.io/badge/template-helm-orange" alt="Repository type - helm" style="display: block;" /></a>


# Logging


<img src="https://raw.githubusercontent.com/hauke-cloud/.github/main/resources/img/organisation-logo-small.png" alt="hauke.cloud logo" width="109" height="123" align="right">


<llm header hint="Name the chart and what it deploys.">

This repository contains a Helm chart named `template-helm-chart` that renders standard Kubernetes manifests, including Deployments, Services, and Ingresses, for an nginx container by default. It is intended for Kubernetes operators managing application infrastructure. You can install the chart from the public registry or modify its values to suit your cluster requirements.

</llm>


## :book: Description

<llm description>

Kubernetes operators often need a consistent method to deploy and manage containerized workloads across clusters. This repository provides a Helm chart that renders generic Kubernetes manifests for deployments, services, ingress routes, service accounts, and horizontal pod autoscalers. You can pull the chart directly from GitHub Container Registry as an OCI artifact and configure it through standard values parameters such as replica counts, container images, resource limits, and autoscaling thresholds.

The repository is part of the `hauke-cloud` ecosystem. CI automatically computes semantic versions on every push to `main`, packages the chart, and publishes it to `ghcr.io/hauke-cloud/charts/logging`.

Currently, the chart provides:
- Deployment, Service, Ingress, ServiceAccount, and HorizontalPodAutoscaler templates
- Configurable container images, ports, and resource requests/limits
- HTTP liveness and readiness probes
- Autoscaling controls with CPU utilization targets
- Node selection, tolerations, and affinity rules

</llm>


## :clipboard: Requirements

<llm requirements hint="Give the Kubernetes version constraint from Chart.yaml, the Helm version, and any dependency charts or CRDs that must already be present.">

- Helm 3.x client
- A Kubernetes cluster (no explicit version constraint is declared in `Chart.yaml`)
- Network access to `ghcr.io/hauke-cloud/charts/logging` for pulling the public OCI artifact
- No credentials are required for pulling the chart
- No additional dependency charts or CRDs are required before installation

</llm>


## 🚀 Getting started

<llm getting_started hint="helm repo add, helm install and helm upgrade with the real repository URL and chart name. Show a values override only if the chart needs one to start.">

1. Clone the repository and enter its directory.
```bash
git clone https://github.com/hauke-cloud/logging.git
cd logging
```
2. Render the chart to verify the generated Kubernetes manifests.
```bash
helm template oci://ghcr.io/hauke-cloud/charts/logging
```
3. Deploy the chart to your cluster using a specific version tag.
```bash
helm install logging oci://ghcr.io/hauke-cloud/charts/logging --version 1.0.0
```

</llm>


## :airplane: Usage

<llm usage hint="Show installing with a values file, and how to reach or verify the deployed workload.">

You consume this chart by pulling it from the GitHub Container Registry and deploying it to your cluster. Create a local values file to override defaults, such as adjusting the replica count or enabling ingress routing:

```yaml
replicaCount: 2
image.repository: nginx
service.type: ClusterIP
ingress.enabled: true
ingress.className: nginx
ingress.hosts:
  - host: logging.example.com
    paths:
      - path: /
        pathType: Prefix
```

Install the chart using your chosen values file. The registry publishes artifacts dynamically, so you can omit a specific version tag to pull the latest release:

```bash
helm install logging oci://ghcr.io/hauke-cloud/charts/logging -f my-values.yaml
```

After deployment, verify that the workload is running and accessible. Check pod status and service endpoints with standard Kubernetes commands:

```bash
kubectl get pods
kubectl get svc logging
```

If you enabled ingress routing, confirm the ingress controller has provisioned an external IP or hostname to reach the stack. You can also render the manifests locally before applying them by running `helm template oci://ghcr.io/hauke-cloud/charts/logging`.

</llm>


## :wrench: Configuration

<llm configuration hint="A table of the top-level values from values.yaml: key, default, description. Point at values.yaml for the full set.">

You configure the chart by overriding values in `values.yaml`. The repository exposes a standard set of Helm parameters for managing the underlying Kubernetes resources. The table below covers the primary configuration keys; you can find the complete list, including scheduling constraints and volume mounts, in `values.yaml`.

| name | default | description |
|---|---|---|
| `replicaCount` | `1` | Number of Deployment replicas when autoscaling is disabled. |
| `image.repository` | `"nginx"` | Container image repository. |
| `image.tag` | `""` | Container image tag; falls back to Chart.appVersion. |
| `image.pullPolicy` | `"IfNotPresent"` | Image pull policy. |
| `service.type` | `"ClusterIP"` | Service type. |
| `service.port` | `80` | Service port. |
| `ingress.enabled` | `false` | Enable Ingress resource creation. |
| `ingress.className` | `""` | Ingress class name. |
| `autoscaling.enabled` | `false` | Enable HorizontalPodAutoscaler. |
| `resources` | `empty` | Kubernetes resource requests and limits. |

Note that while the project documentation references ELK stack controls, Openstack integration, SSO security, alerting, and ingest pipelines, these configuration inputs are not currently implemented in the chart templates or values.

</llm>


## 📄 License

This Project is licensed under the GNU General Public License v3.0

- see the [LICENSE](LICENSE) file for details.


## :coffee: Contributing

To become a contributor, please check out the [CONTRIBUTING](CONTRIBUTING.md) file.


## :email: Contact

For any inquiries or support requests, please open an issue in this
repository or contact us at [contact@hauke.cloud](mailto:contact@hauke.cloud).
