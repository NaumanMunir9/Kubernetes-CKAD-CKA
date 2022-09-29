# ReplicaSet

- A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.

## How a ReplicaSet works

- A ReplicaSet is defined with fields, including a selector that specifies how to identify Pods it can acquire, a number of replicas indicating how many Pods it should be maintaining, and a pod template specifying the data of new Pods it should create to meet the number of replicas criteria.
- A ReplicaSet then fulfills its purpose by creating and deleting Pods as needed to reach the desired number.
- When a ReplicaSet needs to create new Pods, it uses its Pod template.

- A ReplicaSet is linked to its Pods via the Pods' metadata.ownerReferences field, which specifies what resource the current object is owned by.
- All Pods acquired by a ReplicaSet have their owning ReplicaSet's identifying information within their ownerReferences field.
- It's through this link that the ReplicaSet knows of the state of the Pods it is maintaining and plans accordingly.

- A ReplicaSet identifies new Pods to acquire by using its selector.
- If there is a Pod that has no OwnerReference or the OwnerReference is not a Controller and it matches a ReplicaSet's selector, it will be immediately acquired by said ReplicaSet.

## When to use a ReplicaSet

- A ReplicaSet ensures that a specified number of pod replicas are running at any given time.
- However, a Deployment is a higher-level concept that manages ReplicaSets and provides declarative updates to Pods along with a lot of other useful features.
- Therefore, it is recommended to use Deployments instead of directly using ReplicaSets, unless you require custom update orchestration or don't require updates at all.

- This actually means that you may never need to manipulate ReplicaSet objects: use a Deployment instead, and define your application in the spec section.

## Desired State and Current State

### Desired State

- The state of pods which is desired.

### Current State

- The actual state of pods which are running.

## Commands

```shell

kubectl apply -f rs-1.yaml

kubectl get pods
kubectl get rs

# we can also invoke kube-apiserver thought the below command:
kubectl get all

# Now destroy one of the pods - k8s will launch one more pod to match the number of desired replicas
kubectl delete pod pod/web-5rssf

```
