## struct ifreq结构体使用  
这个结构定义在/usr/include/net/if.h，用来配置和获取ip地址，掩码，MTU等接口信息的。

```c
/* Interface request structure used for socket ioctl's. All interface
   ioctl's must have parameter definitions which begin with ifr_name.
   The remainder may be interface specific. */
 
struct ifreq
  {
# define IFHWADDRLEN 6
# define IFNAMSIZ IF_NAMESIZE
    union
      {
        char ifrn_name[IFNAMSIZ]; /* Interface name, e.g. "en0". */
      } ifr_ifrn;
 
    union
      {
        struct sockaddr ifru_addr;
        struct sockaddr ifru_dstaddr;
        struct sockaddr ifru_broadaddr;
        struct sockaddr ifru_netmask;
        struct sockaddr ifru_hwaddr;
        short int ifru_flags;
        int ifru_ivalue;
        int ifru_mtu;
        struct ifmap ifru_map;
        char ifru_slave[IFNAMSIZ]; /* Just fits the size */
        char ifru_newname[IFNAMSIZ];
        __caddr_t ifru_data;
      } ifr_ifru;
  };
# define ifr_name ifr_ifrn.ifrn_name /* interface name */
# define ifr_hwaddr ifr_ifru.ifru_hwaddr /* MAC address */
# define ifr_addr ifr_ifru.ifru_addr /* address */
# define ifr_dstaddr ifr_ifru.ifru_dstaddr /* other end of p-p lnk */
# define ifr_broadaddr ifr_ifru.ifru_broadaddr /* broadcast address */
# define ifr_netmask ifr_ifru.ifru_netmask /* interface net mask */
# define ifr_flags ifr_ifru.ifru_flags /* flags */
# define ifr_metric ifr_ifru.ifru_ivalue /* metric */
# define ifr_mtu ifr_ifru.ifru_mtu /* mtu */
# define ifr_map ifr_ifru.ifru_map /* device map */
# define ifr_slave ifr_ifru.ifru_slave /* slave device */
# define ifr_data ifr_ifru.ifru_data /* for use by interface */
# define ifr_ifindex ifr_ifru.ifru_ivalue /* interface index */
# define ifr_bandwidth ifr_ifru.ifru_ivalue /* link bandwidth */
# define ifr_qlen ifr_ifru.ifru_ivalue /* queue length */
# define ifr_newname ifr_ifru.ifru_newname /* New name */
# define _IOT_ifreq _IOT(_IOTS(char),IFNAMSIZ,_IOTS(char),16,0,0)
# define _IOT_ifreq_short _IOT(_IOTS(char),IFNAMSIZ,_IOTS(short),1,0,0)
# define _IOT_ifreq_int _IOT(_IOTS(char),IFNAMSIZ,_IOTS(int),1,0,0)
```

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

### 实例1, 获取网卡的IP地址

```c
#include<sys/socket.h> // socket()
#include<netinet/in.h> // struct sockaddr_in、htons()
#include<arpa/inet.h> // htons()、inet_aton()、inet_ntoa()
#include<net/if.h>  //struct ifrq
#include<stdio.h>
int main()
{
    int getIpAddrSocket = socket(AF_INET, SOCK_DGRAM, 0);
    if (getIpAddrSocket < 0) {
        perror("socket()");
        return -1;
    }

    struct ifreq ipAddrIfreq;
    strcpy(ipAddrIfreq.ifr_name, "eth0");

    if (ioctl(getIpAddrSocket, SIOCGIFADDR, &ipAddrIfreq) < 0) {
        perror("ioctl()");
        close(getIpAddrSocket);
        return -1;
    }

    printf("ip: %s\n", inet_ntoa(((struct sockaddr_in *)&ipAddrIfreq.ifr_addr)->sin_addr));
}

```
