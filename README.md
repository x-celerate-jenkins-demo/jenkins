Jenkins and Kubernetes Setup
============================

Setup in local docker for desktop:

```
kubectl create ns build
kubectl -n build create serviceaccount tiller
kubectl -n build apply -f tiller-admin-role-binding.yml
helm init --kube-context docker-desktop --tiller-namespace build --service-account tiller
helm install --kube-context docker-desktop --tiller-namespace build --namespace build --name xcelerate -f helm-jenkins-values.yml --set master.adminPassword=admin stable/jenkins
kubectl -n build create secret generic jenkins-docker-credentials --from-file=config.json
kubectl -n build apply -f dockerhub-credentials.yaml
kubectl -n build apply -f github-credentials.yaml
```