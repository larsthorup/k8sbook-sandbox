# k8sbook-sandbox

## Local cluster on Windows

* On Windows: Enable Hyper V in Windows Features
* Install kubectl
  * https://kubernetes.io/docs/tasks/tools/install-kubectl/
* Install minikube
  * https://kubernetes.io/docs/setup/learning-environment/minikube/
* Install helm
  * https://helm.sh/docs/intro/install/
* Run terminal as administrator


    minikube start --vm-driver=hyperv
    minikube status
    minikube ip # 172.17.246.214
    minikube dashboard
    minikube tunnel # exposes nodePort externally
    minikube stop

## Cluster managed by DigitalOcean

    * create cluster at https://cloud.digitalocean.com/kubernetes/clusters
    * record ip # 
    * download cluster config file
    * set `KUBECONFIG` to `<config-path-1>;<config-path-2>;...`
    * TODO: https

## Getting started

    kubectl config view    
    kubectl config use-context minikube         # Specify which cluster to use
    kubectl apply -f hello.deploy.yml           # Deploy application
    kubectl apply -f hello.svc.yml              # Deploy service
    kubectl rollout status deploy hello-deploy  # Wait for rollout
    open http://172.17.246.214:30001/           # Access application through service
    kubectl delete -f hello.svc.yml             # Clean-up
    kubectl delete -f hello.pod.yml
    kubectl delete pod,svc -l release=hello             


## Contexts

    kubectl config view
    kubectl config current-context
    kubectl config use-context minikube

## Nodes

    kubectl get nodes

## Pods

    kubectl apply -f hello.pod.yml
    kubectl wait --for=condition=Ready pod/hello-pod
    kubectl delete -f hello.pod.yml

    kubectl get pods --watch
    kubectl get pods -o wide
    kubectl get pods -o yaml
    kubectl get pods -o json
    kubectl describe pod/hello-pod
    kubectl logs pod/hello-pod
    kubectl logs pod/hello-pod -c hello-ctr
    kubectl exec pod/hello-pod ps aux
    kubectl exec -it pod/hello-pod sh       # in cmd.exe
    
## Deployments

    kubectl apply -f hello.deploy.yml
    kubectl apply -f hello-edge.deploy.yml --record

    kubectl get deploy hello-deploy
    kubectl describe deploy hello-deploy
    kubectl get rs --selector=app=hello-world
    kubectl describe rs --selector=app=hello-world
    kubectl rollout status deployment hello-deploy

    kubectl rollout history deployment hello-deploy
    kubectl rollout undo deployment hello-deploy --to-revision=1

## Services

    kubectl apply -f hello.svc.yml
    kubectl get service hello-svc
    kubectl get svc hello-svc -o=jsonpath='{.status.loadBalancer.ingress[0].ip}'
    kubectl describe service hello-svc

## Helm

    cd helm
    helm create dummy
    
    cd helm
    helm install hello ./hello
    helm status hello
    helm uninstall hello
    helm install hello ./hello --wait --debug
