# XPS 7590-i9-linux
Optimize Linux things on the XPS 7590 with the i9 and the NVIDIA GTX 1650

### Pre-requirements

- Copy everything in this GIT to it’s place on root.

### Enable S3 (deep sleep)

1. add this to **GRUB_CMDLINE_LINUX_DEFAULT** in **/etc/default/grub**

```
mem_sleep_default=deep
```

2. Update GRUB

### NVIDIA On-Demand

1. Install the newest NVIDIA drivers (435.17+)
2. on Ubuntu based systems open NVIDIA settings and set the PRIME profile to **on-demand**
3. Install **mate-optimus** (https://github.com/ubuntu-mate/mate-optimus) **OR** use **GNOME Shell 3.36+** (right click application / use NVIDIA or something) to use the NVIDIA GPU.

With the modprobe parameter in nvidia.conf power-management is great and the NVIDIA GPU turns off when not in use.

### TLP

I cut the max CPU frequency when on battery with TLP to conserve power.
Have a look at the example config in this GIT.

### Fan control

```
apt install i8kutils
systemctl enable --now krstboot
systemctl enable krstresume
```

DELL BIOS based fan control will be disabled and custom fan control will take over. The configs in /etc/i8kmon.conf prevent the fans to start while doing basic tasks and watching videos (until 60°C).

### Undervolt (careful)

Personally I haven’t find the right settings for me right now. Adjust the undervolting values in /etc/systemd/system/undervolt.service.

```
pip3 install undervolt
systemctl enable --now undervolt.timer
```

### 