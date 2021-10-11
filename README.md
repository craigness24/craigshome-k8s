# craigshome-k8s

kubectl apply -f default/volumes/pvc.yaml
kubectl describe pvc homeassistant
kubectl describe pv pvc-77baf6c6-1e23-44e1-bd35-5715d8884340

helm install traefik -n kube-system stable/traefik

helm install mosquitto -f default/mosquitto.yaml k8s-at-home/mosquitto
helm install frigate -f default/frigate.yaml k8s-at-home/frigate
helm uninstall frigate

helm upgrade frigate -f default/frigate.yaml k8s-at-home/frigate
helm install home-assistant -f default/homeassistant.yaml k8s-at-home/home-assistant

helm install esphome -f default/esphome.yaml k8s-at-home/esphome

helm list


# update k3os config
sudo mount -o remount,rw /k3os/system
sudo vi /k3os/system/config.yaml

--resolve-conf "/etc/resolv.conf"

kubectl rollout restart deployment coredns -n kube-system


# kustomize container
docker run --rm -v ~/.kube:/root/.kube:ro -v ~/Development/craigshome-k8s:/home/app:ro -ti line/kubectl-kustomize:latest

docker run --rm -v `pwd`:/home/app:ro -ti ubuntu:latest


# troubleshooting
 2102  kubectl patch crd/applications.argoproj.io -p '{"metadata":{"finalizers":[]}}' --type=merge
 2103  kubectl get crd applications.argoproj.io -o yaml | grep -i terminating
 2104  kubectl get crds -n argocd
 2105  kubectl get crd applications.argoproj.io -o yaml | grep -i terminating
 2106  kubectl get crds -n argocd
 2107* kubectl logs -n argocd argocd-applicationset-controller-5558c458d5-z8lpq | less
 2108* history | grep delete
 2109  history |grep kustomize
 2110  kubectl api-resources --verbs=list --namespaced -o name | xargs -n 1 kubectl get --show-kind --ignore-not-found -n argocd 
 2111  kubectl get crd applications.argoproj.io -o yaml | grep -i terminating
 2112  history | grep json
 2113  kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
 2114* kubectl port-forward service/argocd-server -n argocd 8080:80
 2115  kubectl get crd applications.argoproj.io -o yaml | grep -i terminatingtroubleshooting


# clear argo redis 
kubectl get pods -n argocd 
kubectl exec argocd-redis-74d8c6db65-x6zsl -n argocd -- redis-cli flushall
