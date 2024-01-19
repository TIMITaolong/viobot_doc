# dhcp

UI按打开，找到install/share/viobot/config/viobot.yaml文件打开，把net\_config\_set改成false，保存，重启设备。

![](image/1684140016902_FfcrIbfqcF.jpg)



电脑ip加一个段：10.21.0.100  &#x20;

再远程进去ssh [root@10.21.0.223](mailto:root@10.21.0.223 "root@10.21.0.223")&#x20;

```bash
vim /etc/netplan/01-netcfg.yaml
```

把dhcp4改成yes，下面几行全部注释掉

![](image/image_f-ZSti1D88.png)
