# deploying-vuejs-kubernetes

> To continue make sure you have installed and properly setup, [Docker](https://www.docker.com), [cloud SDK](https://cloud.google.com/sdk/install) and [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). This includes generating an endpoint to your GCP kubernetes cluster.

## deployment

Git clone this repository.
```sh
git clone https://github.com/Manuhmutua/deploying-vuejs-kubernetes.git
```

Build docker image and tag it to push to GCR(google container registry) like:
```sh
docker build . -t gcr.io/PROJECT_ID/IMAGE_NAME
```

Configure docker with gcloud like:
```sh
gcloud auth configure-docker
```

Push the image to GCR like:
```sh
docker push gcr.io/PROJECT_ID/IMAGE_NAME
```

Then create an IP address for Ingress like:
```sh
gcloud compute addresses create IP_NAME --global
```

Then get the created IP address details like:
```sh
gcloud compute addresses describe IP_NAME --global
```

Then apply deployments like:
```sh
kubectl apply -f vuejs-certificate.yaml,vuejs-deployment.yaml,vuejs-ingress.yaml,vuejs-service.yaml
```

In this example we are using Google managed certificate. Find the example app [here](https://vuejs.gleestop.com/)