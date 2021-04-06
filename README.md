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
├── templates            # A directory of templates that, when combined with values, 
                         # will generate valid Kubernetes manifest files.
│   ├── NOTES.txt        # A plain text file containing short usage notes
│   ├── namespace.yaml   # A template to create a Kubernetes namespace
│   └── pod.yaml         # A template to create a Kubernetes pod to run Nginx
└── values.yaml          # The default configuration values for this chart
```

Refer to [Chart File Structure](https://helm.sh/docs/topics/charts/) documentation for more details.

### Testing the Helm Chart

Use the `--dry-run` flag from the `helm install` command to simulate an installation and verify potential problems.

`helm install my-nginx-chart -f my-nginx-chart/values.yaml my-nginx-chart --dry-run`

### Installing the Helm Chart

Run the `helm install` command to install Nginx using the Helm Chart.

`helm install my-nginx-chart -f my-nginx-chart/values.yaml my-nginx-chart`

Output

```text
NAME: my-nginx-chart
LAST DEPLOYED: Tue Apr  6 15:47:39 2021
NAMESPACE: default
STATUS: pending-install
REVISION: 1
TEST SUITE: None
HOOKS:
MANIFEST:
---
# Source: my-nginx-chart/templates/namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: my-nginx-chart
---
# Source: my-nginx-chart/templates/pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: "my-nginx-chart-pod"
  namespace: my-nginx-chart
  labels:
    app: nginx-app
spec:
  containers:
    - name: nginx
      image: nginx:1.19.9-alpine
  restartPolicy: Always
NOTES:
1. Get the application URL running with these commands:
export POD_NAME=$(kubectl get pods --namespace my-nginx-chart -l "app=nginx-app" -o jsonpath="{.items[0].metadata.name}")
kubectl --namespace my-nginx-chart port-forward $POD_NAME 8080:80
2. Visit http://127.0.0.1:8080 to use your application
```

Using the commands on the NOTES section you should be able to access Nginx home page.

### Uninstalling the Helm Chart

Run the `helm uninstall` command to remove all resources created using Helm from Kubernetes.

`helm uninstall my-nginx-chart`

Output

`release "my-nginx-chart" uninstalled`
