# XPS 7590-i9-linux
Optimize Linux things on the XPS 7590 with the i9 and the NVIDIA GTX 1650

### Pre-requirements

- Copy everything in this GIT to it’s place on root.

- make the dell-bios-fan-control command executable

    ```
    sudo chmod +x /usr/sbin/dell-bios-fan-control
    ```

### Enable S3 (deep sleep)

1. add this to **GRUB_CMDLINE_LINUX_DEFAULT** in **/etc/default/grub**

```
mem_sleep_default=deep
```

2. Update GRUB
3. reboot

### NVIDIA On-Demand

1. Install the newest NVIDIA drivers (435.17+)
2. on Ubuntu based systems open NVIDIA settings and set the PRIME profile to **on-demand**
3. Install **mate-optimus** (https://github.com/ubuntu-mate/mate-optimus) **OR** use **GNOME Shell 3.36+** to use the NVIDIA GPU.
    - with mate-optimus use the commands **offload-glx** or **offload-vulkan** to run an application with the NVIDIA GPU enabled
    - with GNOME Shell right click an application icon in the shell and click something like **run with NVIDIA** - this should be in GNOME Shell 3.36+ and should work with the propriatary drivers

With the modprobe parameter in nvidia.conf power-management is great and the NVIDIA GPU turns off when not in use.

### TLP

I cut the max CPU frequency and disabled turbo boost when on battery with TLP to conserve power.
Have a look at the example config in this GIT.

### Fan control (to be tuned in the future)

```
apt install i8kutils
systemctl enable --now dell-bios-fan-control
systemctl enable --now i8kmon
```

DELL BIOS based fan control (thanks to @TomFreudenberg: https://github.com/TomFreudenberg/dell-bios-fan-control) will be disabled and custom fan control will take over. The configs in /etc/i8kmon.conf prevent the fans to start while doing basic tasks and watching videos (until 60°C).

EDIT: It’s not fine grained, yet as I only get no fans and pretty much maxed fans. I’ll update the fan configs when I find more usable values. Until now I would not mind this fan control step.
BIOS fan control is pretty much alright but they kick in a little too early for my taste.

### Undervolt (careful, to be tuned in the future)

Personally I haven’t find the right settings for me right now. Adjust the undervolting values in /etc/systemd/system/undervolt.service.

```
pip3 install undervolt
systemctl enable --now undervolt.timer
```

### 