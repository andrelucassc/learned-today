### Configuring RPI cluster k3s agent
Installation followed in https://github.com/k3s-io/k3s-ansible.

[Source](https://blog.alexellis.io/test-drive-k3s-on-raspberry-pi/)

Add  `cgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memory` to `/boot/cmdline.txt`. 
