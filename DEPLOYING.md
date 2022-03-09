## Building and deploying to a Kubernetes cluster using a TAP workload

> NOTE: This workload is currently deploy using an embedded database. It will be enhanced in the future to use a PostgreSQL database using the service-binding support.

### Deploying to Kubernetes as a TAP workload with Tanzu CLI

If you make modifications to the source and push to your own Git repository, then you can update the `spec.source.git` information in the `config/workload.yaml` file.

When you are done developing your database app, you can simply deploy it using:

```
tanzu apps workload apply -f config/workload.yaml
```

If you would like deploy the code from your local working directory you can use the following command:

```
tanzu apps workload create spring-sql-jpa -f config/workload.yaml \
  --local-path . \
  --source-image <REPOSITORY-PREFIX>/spring-sql-jpa-source \
  --type web
```

### Accessing the app deployed to your cluster

If you don't have `curl` installed it can be installed using downloads here: https://curl.se/download.html

> Note: This depends on the TAP installation having DNS configured for the Knative ingress.

Determine the URL to use for accessing the app by running:

```
tanzu apps workload get spring-sql-jpa
```

To view the users run:

```
curl -w'\n' <URL>/demo/all
```

To add a user run:

```
curl -w'\n' <URL>/demo/add \
 -d name=First \
 -d email=someemail@someemailprovider.com
```
