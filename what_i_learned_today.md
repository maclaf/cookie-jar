What I learned today
=======================
# 15.07.2021
It's better to use [distroless](https://github.com/GoogleContainerTools/distroless) docker image instead of alpine because of security reasons (no shell as it is for alpine/ubuntu/general linux image)

# 16.07.2021
Removing annotation or label on some resource is done by following syntax:
```kubectl annotate <resource> <resource-name> myannotation-```
For example:
```
$ POD=nginx-68dc96bdb6-xrrxk
$ kubectl annotate pod $POD myannotation='123'
$ kubectl get pod $POD -o custom-columns=myannotation:{.metadata.annotations.myannotation}
myannotation
123
$ kubectl annotate pod $POD myannotation-
pod/nginx-68dc96bdb6-xrrxk annotated
$ kubectl get pod $POD -o custom-columns=myannotation:{.metadata.annotations.myannotation}
```

# 19.07.2021
When trying to modify kubernetes deployment, you can find possible values for given field by invoking ```kubectl explain <api-resource>...``` 
```
$ kubectl api-resources
$ kubectl explain pod.spec.imagePullSecrets      
KIND:     Pod
VERSION:  v1

RESOURCE: imagePullSecrets <[]Object>

DESCRIPTION:
     ImagePullSecrets is an optional list of references to secrets in the same
     namespace to use for pulling any of the images used by this PodSpec. If
     specified, these secrets will be passed to individual puller
     implementations for them to use. For example, in the case of docker, only
     DockerConfig type secrets are honored. More info:
     https://kubernetes.io/docs/concepts/containers/images#specifying-imagepullsecrets-on-a-pod

     LocalObjectReference contains enough information to let you locate the
     referenced object inside the same namespace.

FIELDS:
   name	<string>
     Name of the referent. More info:
     https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#names


```
# 20.07.2021
In bash you can create read only names by using following syntax:
```
$ readonly MY_VARIABLE=123
$ MY_VARIABLE=1234
bash: MY_VARIABLE: readonly variable
$ echo $MY_VARIABLE
123
```
# 31.08.2021
Azure container registry does not show helm repository content from web console properly. This is misleading, as you might think ecr repository is empty. 
To list available charts in such repository you can do following:
```
helm repo add yourecr 'https://yourecr.azurecr.io/helm/v1/repo' --password <password> --username <username>
helm search repo yourecr
```

# 01.09.2021
When trying to apply terraform resource on minikube: 
```
"helm_release" "my-release"{
..
}
```
./terraform-0.14.11 apply -var-file tfvars.tfvars 

and you get following error:
```
Error: Kubernetes cluster unreachable: invalid configuration: no configuration has been provided, try setting KUBERNETES_MASTER environment variable
```
if could be fixed by invoking:
```
export KUBE_CONFIG_PATH=~/.kube/config
```

# 24.09.2021

Minikube caches docker images somwhere else than docker itself. So if you develop docker image locally and and push changes to remote server, you could do not have latest version as kubectl events reports "container image <image-name> already present on machine". Removing docker image by:
```
docker image rm <hash>
```
does not affect minikube.
To get rid of minikube cached image you need to invoke:
```
minikube image rm <image-name>
```

# 10.05.2022
Most usefull security related websites 
- CWE - Common Weeknes Enumeration
- CAPEC - Common Attack Pattern Enumeration and Classification
- ATT&CK 
- NVD - National Vulnerability Database

# 14.07.2022
test docker with pgsql:
1. run docker with pgsql:
     ```docker run -e POSTGRES_PASSWORD=qqq -e POSTGRES_USER=qqq postgres```
2. connect psql to that docker:
     ```docker inspect --format='{{json .NetworkSettings.Networks}}' 3442a07ff11f
{"bridge":{"IPAMConfig":null,"Links":null,"Aliases":null,"NetworkID":"06c38a8d5d2a22d6836a9a221581904bd75a799f737501aa4424539a1fcfa0b3","EndpointID":"322b1eea628768b6e459924e72b61158a9c2c464c9cf8a8d828a08a680bb3687","Gateway":"172.17.0.1","IPAddress":"172.17.0.3","IPPrefixLen":16,"IPv6Gateway":"","GlobalIPv6Address":"","GlobalIPv6PrefixLen":0,"MacAddress":"02:42:ac:11:00:03","DriverOpts":null}}
     docker run -it --rm --network bridge postgres psql -h 172.17.0.3 -U qqq```
     
     
