1. [安装 Cockpit 管理 KVM 虚拟机](https://bynss.com/linux/594875.html)
2. [ubuntu 使用 kvm 搭建虚拟机 + bridge](https://blog.csdn.net/qq_38916811/article/details/120792767)
3. [ubuntu 18.04 server 扩容(LVM)磁盘 解决磁盘不足的情况](https://zhuanlan.zhihu.com/p/113368408)

虚拟机上网络配置
```
network:
  ethernets:
    enp1s0:
      addresses: [192.168.3.51/24]
      nameservers:
        addresses: [223.5.5.5, 8.8.8.8]
      routes:
      - to: default
        via: 192.168.3.1
  version: 2
```
[解决因docker bridge网桥引起的虚拟机网络故障_docker_ls_elect-DevPress官方社区 (csdn.net)](https://huaweicloud.csdn.net/6331155ed3efff3090b51baa.html?spm=1001.2101.3001.6650.11&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Eactivity-11-122811167-blog-90946701.pc_relevant_multi_platform_whitelistv3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Eactivity-11-122811167-blog-90946701.pc_relevant_multi_platform_whitelistv3&utm_relevant_index=12)

[(120条消息) 解决 因为docker启动容器 导致的虚拟机无法远程连接问题_yssa1125001的博客-CSDN博客](https://blog.csdn.net/yssa1125001/article/details/109694774)