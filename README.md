# learned-today

## Configuring Rasperry Pi Time Sync

* Disable ntp service
* Remove ntp ntpdate sntp if present
* Config systemd-timesyncd.service on /etc/systemd/timesyncd.conf
* Set NTP pool below [Time]
* Enable and start systemd-timesyncd.service
* Set timedatectl set-ntp true
* timedatectl to check if the sync and service is on
* Done!

Notes:

I tried very hard to make ntp work, but id did not, sometime failing to boot, sometimes not syncing and it does not integrate well with the builtin Pi's timedatectl.
I also tried ansible-galaxy ntp role from (geerlingguy)[https://github.com/geerlingguy/ansible-role-ntp] NTP role, but it did not work on my setup and I wasn't able to assess why.