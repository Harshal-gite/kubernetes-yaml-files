📌 1. Pod
Purpose

Creates a single Pod that runs one container.

Commands
kubectl apply -f pod.yaml
kubectl get pods
kubectl get pods -o wide
kubectl describe pod pod-coffee
kubectl logs pod-coffee
kubectl delete -f pod.yaml

📌 2. Replication Controller
Purpose

Maintains the desired number of Pod replicas. If one Pod fails, Kubernetes automatically creates a new one.

Commands
kubectl apply -f replication-controller.yaml
kubectl get rc
kubectl describe rc replicationcontroller
kubectl get pods
kubectl delete -f replication-controller.yaml

📌 3. Service
Purpose

Exposes Pods so that users or other applications can access them.

Commands
kubectl apply -f service.yaml
kubectl get svc
kubectl describe svc svc-rc
kubectl get endpoints
kubectl delete -f service.yaml

📌 Useful Commands
kubectl cluster-info

kubectl version

kubectl get nodes

kubectl get all

kubectl get events

kubectl get pods --show-labels

kubectl logs <pod-name>

kubectl describe pod <pod-name>

kubectl exec -it <pod-name> -- sh

kubectl delete pod <pod-name>

kubectl explain pod

kubectl explain service

kubectl explain replicationcontroller

📄 pod.yaml

apiVersion: v1
kind: Pod

metadata:
  name: pod-coffee
  labels:
    env: dev

spec:
  containers:
  - name: coffee
    image: harshu-gite/coffie:latest
    ports:
    - containerPort: 80

    📄 replication-controller.yaml
    apiVersion: v1
kind: ReplicationController

metadata:
  name: replicationcontroller

spec:
  replicas: 3

  selector:
    env: dev

  template:
    metadata:
      labels:
        env: dev

    spec:
      containers:
      - name: coffee
        image: harshu-gite/coffie:latest
        ports:
        - containerPort: 80

        📄 service.yaml
        apiVersion: v1
kind: Service

metadata:
  name: svc-rc

spec:
  selector:
    env: dev

  ports:
  - protocol: TCP
    port: 80
    targetPort: 80

  type: NodePort
  
