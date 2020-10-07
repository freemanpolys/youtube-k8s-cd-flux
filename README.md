# Install fluxctl
brew install fluxctl

# Configuration de flux
fluxctl install \
--git-user=freemanpolys \
--git-email=gaglo.kokou@orange-sonatel.com \
--git-url=git@github.com:freemanpolys/youtube-k8s-cd-flux \
--git-path=devtest2020-ns,devtest2020-workload \
--namespace=flux | kubectl apply -f -

kubectl -n flux rollout status deployment/flux

# Récupérer et ajouter la clé ssh sur git
fluxctl identity --k8s-fwd-ns flux

# Forcer flux
fluxctl sync --k8s-fwd-ns flux

# Manips
kubectl create deployment web --image=gcr.io/google-samples/hello-app:1.0.1

cd docker-image

docker build -t registry.labs:5000/hello-app:2.0.0 .

docker push registry.labs:5000/hello-app:2.0.0


