kubectl create deployment web --image=gcr.io/google-samples/hello-app:1.0.1
docker tag bitnami/nginx registry.labs:5000/hello-app:1.0.1
docker push registry.labs:5000/hello-app:1.0.1

fluxctl sync --k8s-fwd-ns flux

