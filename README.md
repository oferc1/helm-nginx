# helm-nginx
Run local nginx server with helm and minikube

# Prerequisites

* Install minikube
* Install helm
* Start minikube - make sure kubernates version is max 1.15.4 ( as latest is not supported with helm )
You can do it with ```minikube start --kubernetes-version=1.15.4```

# Setup instructions
* Clone the repository
* Initialize helm with 
```
helm init
```
* Install app with
```
helm install --name my-cherry-chart helm-nginx/ --values helm-nginx/values.yaml  
```
Then installation instructions will be displayed in terminalcop, for example: 
```
export POD_NAME=$(kubectl get pods -l "app.kubernetes.io/name=buildachart,app.kubernetes.io/instance=my-cherry-chart" -o jsonpath="{.items[0].metadata.name}")
export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services cherry-chart)
export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
echo http://$NODE_IP:$NODE_PORT
```
Follow and copy paste lines in terminal

Visit http://$NODE_IP:$NODE_PORT
