# learned-today

## Configuring Ubuntu Timezone

* sudo dpkg-reconfigure tzdata

## Kubernetes
### Setting current context permanently

* kubectl config set-context --current --namespace=

### Getting Pods on specific node

* kubectl get pods --all-namespaces -o wide --field-selector spec.nodeName=<node>
 
### Setting node password
 
Copy new node password from `/etc/rancher/node/password` to `/var/lib/rancher/k3s/server/cred/node-passwd`.

## Configuring PostgreSQL Database Config File

[config](https://www.prisma.io/dataguide/postgresql/authentication-and-authorization/configuring-user-authentication)
 
##  Setting pipe with xargs
 
 Using xargs to to populate shell command:
 
 `cat .variables | grep -Po '\/[\w\/-]+' | xargs -I{} sh -c 'mkdir $HOME"$1"' -- {}`
 
 ## Poetry
 
 To configure poetry to use current active python version from pyenv:
[Link]( https://github.com/python-poetry/poetry/issues/5947)
 
 `poetry config virtualenvs.prefer-active-python true`
