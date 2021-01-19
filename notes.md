
kubectl create namespace metacontroller

# Create metacontroller service account and role/binding.
kubectl apply -f https://raw.githubusercontent.com/metacontroller/metacontroller/master/manifests/production/metacontroller-rbac.yaml


# Create CRDs for Metacontroller APIs, and the Metacontroller StatefulSet.
kubectl apply -f https://raw.githubusercontent.com/metacontroller/metacontroller/master/manifests/production/metacontroller.yaml


base/jitsi/jitsi-secrest.yaml ändern

nodeSelector:
  kubernetes.io/os: linux
  kubernetes.io/arch: "amd64"

nodeSelector:
    "kubernetes.io/os": linux

zu 

nodeSelector:
  beta.kubernetes.io/os: linux
  beta.kubernetes.io/arch: "amd64"

nodeSelector:
    "beta.kubernetes.io/os": linux


kubectl get all -n jitsi


kustomize build . | kubectl apply -f -
kustomize build . | kubectl delete -f -

kubectl patch statefulsets shard-1-jvb -n jitsi -p '{"metadata":{"finalizers":null}}'
kubectl patch statefulsets shard-0-jvb -n jitsi -p '{"metadata":{"finalizers":null}}'