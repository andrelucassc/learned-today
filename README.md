# learned-today

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
  * ansible group -m ansible.builtin.service -a "name=ntp state=started" -b
* Set timedatectl set-ntp true
  * ansible group -a "timedatectl set-ntp true" -b
* timedatectl to check if the sync and service is on
* Done!

Notes:

I tried very hard to make ntp work, but id did not, sometime failing to boot, sometimes not syncing and it does not integrate well with the builtin Pi's timedatectl.
I also tried ansible-galaxy ntp role from [geerlingguy](https://github.com/geerlingguy/ansible-role-ntp) NTP role, but it did not work on my setup and I wasn't able to assess why.

## Getting Pods on specific node

* kubectl get pods --all-namespaces -o wide --field-selector spec.nodeName=<node>
