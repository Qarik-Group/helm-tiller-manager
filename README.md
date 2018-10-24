# Helm/Tiller Manager

I found the multi-step instructions for deploying Tiller (the API server for Helm) were not going to be rememberable. Creating certificates, running the correct `helm init` command, etc. So this project includes a `helm-manager up` and `helm-manager down` command to do it all for us.

To generate certificates and install Tiller into your current Kubernetes context:

```console
export PATH=$PATH:$PWD/bin
helm-manager up
```

The output might look like:

```output
Creating certificates...
Generating RSA private key, 4096 bit long modulus
.....................................................++
..................................................++
e is 65537 (0x10001)
Generating RSA private key, 4096 bit long modulus
......................++
..............................................................++
e is 65537 (0x10001)
Signature ok
subject=/O=Tiller Server/CN=tiller-server
Getting CA Private Key
Installing helm into current Kuberenetes context...
serviceaccount/helm created
clusterrolebinding.rbac.authorization.k8s.io/helm created
Creating /Users/drnic/.helm
Creating /Users/drnic/.helm/repository
Creating /Users/drnic/.helm/repository/cache
Creating /Users/drnic/.helm/repository/local
Creating /Users/drnic/.helm/plugins
Creating /Users/drnic/.helm/starters
Creating /Users/drnic/.helm/cache/archive
Creating /Users/drnic/.helm/repository/repositories.yaml
Adding stable repo with URL: https://kubernetes-charts.storage.googleapis.com
Adding local repo with URL: http://127.0.0.1:8879/charts
$HELM_HOME has been configured at /Users/drnic/.helm.

Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster.
Happy Helming!
Installing helm client certificates...
When Tiller is ready, test connection and certificates:
  helm ls --tls && echo working
```

Confirm `helm` and Tiller server are working:

```console
$ helm ls --tls && echo working
working
```

## Tear down

To tear down Tiller and local Helm files:

```console
export PATH=$PATH:$PWD/bin
helm-manager down
```

To cleanup/regenerate the certificates:

```console
helm-manager clean
```