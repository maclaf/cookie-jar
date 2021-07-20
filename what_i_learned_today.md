What I learned today
=======================
# 15.07.2021
It's better to use [distroless](https://github.com/GoogleContainerTools/distroless) docker image instead of alpine because of security reasons (no shell as it is for alpine/ubuntu/general linux image)

# 20.07.2021
In bash you can create read only variables:
```
$ readonly MY_VARIABLE=123
$ MY_VARIABLE=1234
bash: MY_VARIABLE: readonly variable
$ echo $MY_VARIABLE
123
```
