# learned-today

## Configuring Ubuntu Timezone

* sudo dpkg-reconfigure tzdata

## Configuring Ubuntu firewall



## Configuring Rasperry Pi Time Sync

* Disable ntp service
  * sudo systemctl stop ntp
  * sudo systemctl disable ntp
* Remove ntp ntpdate sntp if present
  * ansible group -m ansible.builtin.apt -a "name=ntp state=absent" -b
  * ansible group -m ansible.builtin.apt -a "name=ntpdate state=absent" -b
  * ansible group -m ansible.builtin.apt -a "name=sntp state=absent" -b
* Config systemd-timesyncd.service on nano /etc/systemd/timesyncd.conf
* Set NTP pool below [Time]
  * NTP Server Pool config NTP=Pool1 Pool2 Pool3 Pool4
* Enable and start systemd-timesyncd.service
  * ansible group -m ansible.builtin.service -a "name=systemd-timesyncd.service state=started" -b
* Set timedatectl set-ntp true
  * ansible group -a "timedatectl set-ntp true" -b
* timedatectl to check if the sync and service is on
* Done!

Notes:

I tried to make ntp work, but it did not, sometime it failed to boot, sometimes it did not sync and it does not integrate well with the builtin's Pi timedatectl.
I also tried ansible-galaxy from [geerlingguy](https://github.com/geerlingguy/ansible-role-ntp) NTP role, but it did not work on my setup and I wasn't able to assess why.

## Kubernetes

### Configuring RPI cluster k3s agent
Installation followed in https://github.com/k3s-io/k3s-ansible.

[Source](https://blog.alexellis.io/test-drive-k3s-on-raspberry-pi/)

Add  `cgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memory` to `/boot/cmdline.txt`. 

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
