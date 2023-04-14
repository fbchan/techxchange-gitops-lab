# Infrastructure Application Services

When a cluster is provisioned, there is usually a desire to install services that can be used cluster-wide by one or more user applications. These "infrastructure apps" can vary from security services, traffic shapers/routers, deployment operators, security vaults, dashboards, telemetry providers, etc.

Typically a platform operations engineer will ensure these services are available in a cluster based on the needs of *their* customers, the application owners, or developers. With the power of XC's Managed Kubernetes offering, platform engineers can automate the deployment of a fleet of clusters worldwide, all interconnected with our best-in-class network.

We will introduce and deploy a few of these "infrastructure apps".

Note: For learning purposes, in this lab we are manually creating the configurations that instruct Argo CD to deploy applications one at a time. In a real-world scenario, we should automate both the creation of the AppStack Managed Kubernetes cluster, the installation of Argo CD, complete with all application configurations to be installed once the cluster is available without requiring any additional intervention.

## Metrics and Visibility

Grafana is a multi-platform open source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources.

The NGINX Ingress Controller (used later in this lab) provides a Grafana dashboard to provide analytical data related to the performance and behavior of the controller's underlying NGINX metrics. The NGINX Ingress Controller has been installed with support for providing these metrics in the Prometheus format, and we will leverage Grafana to consume these metrics, and provide a visual representation of this data.

You will install both Grafana and Prometheus into your Kubernetes cluster.

## Grafana Installation

We will leverage Argo CD to install NGINX Ingress Controller for us, leveraging Helm Charts.

[Helm](https://helm.sh/) helps you manage Kubernetes applications — Helm Charts help you define, install, and upgrade even the most complex Kubernetes application with minimal, declarative configuration.

TODO: add grafana installation steps

1. Verify the installation was successful by logging into Argo CD. Ensure that an application called `grafana` has been installed, and is in sync and healthy.

## Grafana Login

1. In your browser, open a new tab and log into Grafana by navigating to <TODO: what is this url>

1. When presented for login credentials, enter `admin` as the username. To acquire the password, you must interrogate k8s for the secret containing the password from a terminal in the Ubuntu desktop:

    ```bash
    kubectl get secret --namespace <TODO: your namespace> grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
    ```

1. For now, you are just confirming that you can log in to Grafana; we will use it later in this lab so keep this tab open.

## Prometheus Installation

TODO: add Prometheus installation steps

1. Verify the installation was successful by logging into Argo CD. Ensure that an application called `prometheus` has been installed, and is in sync and healthy.

Although Prometheus has a user interface to query data, we will not be using it in this lab. Grafana will be querying Prometheus for the metrics data it fetched from NGINX Ingress Controller.

## XC Ingress Controller

The Ingress Controller manages external access to HTTP services in a Kubernetes cluster using the F5 Distributed Cloud Services Platform. The ingress controller is a K8s deployment that configures the HTTP Load Balancer using the K8s ingress manifest file. The Ingress Controller automates the creation of load balancer and other required objects such as VIP, Layer 7 routes (path-based routing), advertise policy, certificate creation(k8s secrets or automatic custom certificate), etc.

Though the XC Ingress Controller has some application routing features, we will be utilizing NGINX Ingress Controller for this. The value that XC Ingress Controller provides is its capability to create the necessary Load Balancer and Origin pool objects for the applications we expose - automatically, without having to spawn any custom workflows.

TODO: XC Ingress installation instructions

1. Verify the installation was successful by logging into Argo CD. Ensure that an application called `volterra-ingress-controller` has been installed, and is in sync and healthy.

## NGINX Ingress Controller

The NGINX Ingress Controller an implementation of a Kubernetes Ingress Controller for NGINX and NGINX Plus.

### What is the Ingress Controller?

The Ingress Controller is an application that runs in a cluster and configures an HTTP load balancer according to Ingress resources. The load balancer can be a software load balancer running in the cluster or a hardware or cloud load balancer running externally. Different load balancers require different Ingress Controller implementations.

In the case of NGINX, the Ingress Controller is deployed in a pod along with the load balancer.

### NGINX Ingress Controller Installation

We will again leverage Argo CD to install NGINX Ingress Controller for us, leveraging Helm charts.

TODO: NGINX Ingress Controller installation instructions

1. Verify the installation was successful by logging into Argo CD. Ensure that an application called `nic` has been installed, and is in sync and healthy.

[Continue to next step...](brewz-application.md)