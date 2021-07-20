What I learned today
=======================
# 15.07.2021
It's better to use [distroless](https://github.com/GoogleContainerTools/distroless) docker image instead of alpine because of security reasons (no shell as it is for alpine/ubuntu/general linux image)

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
