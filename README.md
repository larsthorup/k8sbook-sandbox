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
    minikube stop

## Deploy

    kubectl apply -f hello.pod.yml
    kubectl wait --for=condition=Ready pod/hello-pod
    kybectl delete -f hello.pod.yml

## Monitor

    kubectl get pods --watch
    kubectl get pods -o wide
    kubectl get pods -o yaml
    kubectl get pods -o json
    kubectl describe pod/hello-pod
    kubectl logs pod/hello-pod
    kubectl exec pod/hello-pod ps aux
    kubectl exec -it pod/hello-pod sh       # in cmd.exe
    
