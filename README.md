# Helm Chart Repository

[Helm](https://helm.sh) is a package manager for Kubernetes.

[Helm Charts](https://helm.sh/docs/topics/charts/) help you define, install, and upgrade even the most complex Kubernetes application.

This repository is a location where packaged charts can be stored and shared.

> This repository was designed to support the [Medium Article](https://medium.com/) created to demonstrate how to create and use Helm Charts.

## Managing applications using charts

### Prerequisites

- `Helm 3` - Refer to the [Helm Installation Guide](https://helm.sh/docs/intro/install/) for instructions.
- Active `Kubernetes` installation

The charts in this repository were created using `helm 3.2.4` on `macOS` with a local [Minikube](https://minikube.sigs.k8s.io/docs/) installation.

### Helm Chart file structure

```text
my-nginx-chart
├── Chart.yaml           # A YAML file containing information about the chart
├── templates            # A directory of templates that, when combined with values, will generate valid Kubernetes manifest files.
│   ├── NOTES.txt        # A plain text file containing short usage notes
│   ├── namespace.yaml   # A template to create a Kubernetes namespace
│   └── pod.yaml         # A template to create a Kubernetes pod to run Nginx
└── values.yaml          # The default configuration values for this chart
```
