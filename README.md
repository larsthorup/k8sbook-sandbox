# k8sbook-sandbox

## Prerequisites

* On Windows: Enable Hyper V in Windows Features
* Install kubectl
  * https://kubernetes.io/docs/tasks/tools/install-kubectl/
* Install minikube
  * https://kubernetes.io/docs/setup/learning-environment/minikube/
* Run terminal as administrator


    minikube start --vm-driver=hyperv
    minikube status
    minikube ip # 172.17.246.214
    minikube stop

## Getting started

    kubectl config use-context minikube     # Specify which cluster to use
    kubectl apply -f hello.deploy.yml       # Deploy application
    kubectl apply -f hello.svc.yml          # Deploy service
    open http://172.17.246.214:30001/       # Access application through service
    kubectl delete -f hello.svc.yml         # Clean-up
    kybectl delete -f hello.pod.yml

## Contexts

    kubectl config view
    kubectl config current-context
    kubectl config use-context minikube

## Nodes

    kubectl get nodes

## Pods

    kubectl apply -f hello.pod.yml
    kubectl wait --for=condition=Ready pod/hello-pod
    kybectl delete -f hello.pod.yml

    kubectl get pods --watch
    kubectl get pods -o wide
    kubectl get pods -o yaml
    kubectl get pods -o json
    kubectl describe pod/hello-pod
    kubectl logs pod/hello-pod
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
