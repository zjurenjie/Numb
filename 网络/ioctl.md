## ioctl网络相关接口
|类别|Request|说明|数据类型|
|--|--|--|--|
|套接字|SIOCATMARK|是否位于带外标记|int|
||SIOCSPGRP|设置套接字的进程ID或进程组ID|int|
||SIOCGPGRP|获取套接字的进程ID或进程组ID|int|
|文件|FIONBIN|设置/清楚非阻塞I/O标志|int|
||FIOASYNC|设置/清除信号驱动异步I/O标志|int|
||FIONREAD|获取接收缓存区中的字节数|int|
||FIOSETOWN|设置文件的进程ID或进程组ID|int|
||FIOGETOWN|获取文件的进程ID或进程组ID|int|
|接口|SIOCGIFCONF|获取所有接口的清单|struct ifconf|
||SIOCSIFADDR|设置接口地址|struct ifreq|
||SIOCGIFADDR|获取接口地址|struct ifreq|
||SIOCSIFFLAGS|设置接口标志|struct ifreq|
||SIOCGIFFLAGS|获取接口标志|struct ifreq|
||SIOCSIFDSTADDR|设置点到点地址|struct ifreq|
||SIOCGIFDSTADDR|获取点到点地址|struct ifreq|
||SIOCGIFBRDADDR|获取广播地址|struct ifreq|
||SIOCSIFBRDADDR|设置广播地址|struct ifreq|
||SIOCSIFNETMASK|设置子网掩码|struct ifreq|
||SIOCGIFNETMASK|获取子网掩码|struct ifreq|
||SIOCSIFMETRIC|获取接口的测度|struct ifreq|
||SIOCGIFMETRIC|设置接口的测度|struct ifreq|
||SIOCGIFMTU|获取接口MTU|struct ifreq|
||SIOCxxx|取决于系统的实现|
|ARP|SIOCSARP|创建/修改ARP表项|struct arpreq|
||SIOCGARP|获取ARP表项|struct arpreq|
||SIOCDARP|删除ARP表项|struct arpreq|
|路由|SIOCADDRT|增加路由|struct rtentry|
||SIOCDELRT|删除路由|struct rtentry|
|流|I_xxx|
