# Kubernetes Exam Tasks 

This repository contains Kubernetes YAML configurations for three practical tasks involving ConfigMaps, Deployments, shared volumes, Services, and Ingress.

---
##  Task 1 – ConfigMap + Alpine Deployment

###  Objective
- Create a ConfigMap with the value: `name = tauhid`.
- Create a Deployment with:
  - 1 replica.
  - Alpine image.
  - A container that runs a custom command:
    - Infinite loop
    - Echo the ConfigMap value (`$NAME`)
    - Sleep 5 seconds

###  Files:
- `task1/configmap.yaml`
- `task1/deployment.yaml`

# Kubernetes Exam Tasks 

This repository contains Kubernetes YAML configurations for three practical tasks involving ConfigMaps, Deployments, shared volumes, Services, and Ingress.

---
## Task 1 – ConfigMap + Alpine Deployment

### Objective
- Create a ConfigMap with the value: name = tauhid.
- Create a Deployment with:
  - 1 replica.
  - Alpine image.
  - A container that runs a custom command:
    - Infinite loop
    - Echo the ConfigMap value ($NAME)
    - Sleep 5 seconds

### Files:
- task1/configmap.yaml
- task1/deployment.yaml
---

## Task 2 – Shared EmptyDir Volume between Containers

### Objective
- Create a Pod with two containers sharing an EmptyDir volume.
- Demonstrate that one container can write data to the shared volume and the other container can read it.

### Files:
- task2/shared-empty-dir.yaml

---
## Task 3 – Deployment + Service + Ingress

### Objective
- Create a Deployment with your application pods.
- Expose the pods via a Service.
- Create an Ingress resource to route external traffic to the Service.

### Files:
- task3/deployment.yaml
- task3/service.yaml
- task3/ingress.yaml

###  Test Steps:
##  Task 1:
kubectl apply -f task1/configmap.yaml
kubectl apply -f task1/deployment.yaml
kubectl get pods
kubectl logs -f <pod-name>

##  Task 2:
kubectl apply -f task2/shared-empty-dir.yaml
kubectl get pods
kubectl describe pod <pod-name>

# Check shared volume
kubectl exec -it <pod-name> -c container1 -- sh
echo "Hello from container1" > /shared/data.txt
exit

kubectl exec -it <pod-name> -c container2 -- sh
cat /shared/data.txt  # Should display "Hello from container1"

##  Task 3:
kubectl apply -f task3/deployment.yaml
kubectl apply -f task3/service.yaml
kubectl apply -f task3/ingress.yaml

# (Optional - for local testing)
echo "127.0.0.1 example.com" | sudo tee -a /etc/hosts

# Verify via curl
curl http://example.com

Md Tauhidul Islam
GitHub: QALeadTauhid
