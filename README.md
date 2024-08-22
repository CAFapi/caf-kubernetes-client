# caf-kubernetes-client

This project provides a Java client for Kubernetes.

To use, import the dependency into your project:

```xml
<dependency>
    <groupId>com.github.cafapi.kubernetes.client</groupId>
    <artifactId>caf-kubernetes-client</artifactId>
    <version>ENTER_VERSION_HERE</version>
</dependency>
```

Then, create a client. You have 2 options:

Option 1:

This method expects the following environment variables to be present:

- KUBERNETES_SERVICE_HOST
- KUBERNETES_SERVICE_PORT

and the following files to be present:

- /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
- /var/run/secrets/kubernetes.io/serviceaccount/token

```java
ApiClient apiClient = KubernetesClientFactory.createClientWithCertAndToken();
```

Option 2:

This method accepts the ca cert file path, token file path, host and post
as parameters, which can be useful if you are running the code locally and want
to connect to a test Kubernetes cluster.

```java
ApiClient apiClient = KubernetesClientFactory.createClientWithCertAndToken(
                "C:\\Users\\Your-Name\\Documents\\ca.crt",
                "C:\\Users\\Your-Name\\Documents\\token",
                "16.103.45.94",
                6443);
```

Once the client has been created, call the API:

```java
AppsV1Api appsV1Api = new AppsV1Api(productionApiClient);

IoK8sApiAppsV1DeploymentList deploymentList = appsV1Api.listAppsV1NamespacedDeployment(
    "private",
    null,
    null,
    null,
    null,
    null,
    null,
    null,
    null,
    null,
    0,
    null);
```