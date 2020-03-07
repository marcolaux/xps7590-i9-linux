# xps7590-i9-linux
optimize Linux things on the XPS 7950 with the i9

### enable S3 (deep sleep)

add this to **GRUB_CMDLINE_LINUX_DEFAULT** in **/etc/default/grub**
```
mem_sleep_default=deep
```

### undervolt

https://github.com/georgewhewell/undervolt

```
undervolt --core -125 --cache -125 --gpu -125
```

### NVIDIA On-Demand

Just install the newest NVIDIA drivers, set it to **on-demand** in the NVIDIA settings and create the following file to conserve power and get down up to ~6 W when idle:

/etc/modprobe.d/nvidia.conf

```
options nvidia NVreg_DynamicPowerManagement=0x02
```

Install mate-optimus (https://github.com/ubuntu-mate/mate-optimus) or use the newest GNOME Shell (right click application / use NVIDIA or something) to use the NVIDIA GPU.

### TLP

I cut the max CPU frequency when on battery with TLP to conserve power.
Have a look at the example config in this GIT.
