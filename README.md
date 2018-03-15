# IRTS_SDK

全球电离层实时云服务(Ionosphere Real Time Service, IRTS)可服务于全球导航卫星定位，提供全球范围的实时电离层总电子含量进而实现导航定位中的电离层延迟修正。

IRTS采用云计算模式的电离层总电子含量播发方式。用户端将GNSS信号电离层穿刺点的位置信息发送给IRTS即可获取实时的电离层TEC并将其转换为电离层斜路径延迟量进而服务于导航定位。这种播发方式能够将电离层建模的数学方法与用户分离，用户只需要接收平台播发的总电子含量而无需电离层模型系数，有效降低了接收机端数据处理的复杂度，促进了接收机端数据处理模块的统一性。


IRTS采用了“虚实”组合服务器，将科学计算部分与用户交互分离，充分发挥各类服务器的计算效能，大大提升了平台服务的性能，可根据用户数量进行弹性的服务器配置从而节省平台运行的成本，同时具备多个虚拟服务器备份从而实现平台持续安全运行，并能够有效控制针对特定时空下电离层总电子含量的精度，而且可根据需求进行相应的部署即可服务于区域、全球用户。

### IRTS软件开发工具包

IRTS SDK封装了用户端与服务端的通信，通过几个函数即可便捷地实现服务端的连接、电离层TEC的获取等。工具包中包含三个文件：1）客户端头文件client.h; 2) 功能实现例子main.cpp; 3) IRTS链接库libirts。用户可根据实际的开发平台下载相应的动态链接库libirts（支持Windows，Linux，Mac OS，ARM架构的硬件[手机，树莓派等]）

下载IRTS SDK: [ftp://ftp.ionosphere.cn/software/IRTS_SDK/](ftp://ftp.ionosphere.cn/software/IRTS_SDK/)

**请务必下载IRTS_SDK压缩包以及相应的动态链接库libirts，并将链接库文件重命名为libirts.so或libirts.dll后再编译使用。**

编译指令：
```bash
g++ -O2 -o test main.cpp -L. -lirts
```

部分代码说明：
```C++
char host[20]="irts.iono.cn"; //服务端地址

int port=10086;	//服务端口

char username[10]="test";	//用户名

char password[10]="irts2017"; //密码

MyClient client = MyClient(host,port,username,password); //初始化

client.connect();	//连接服务端，若失败返回false

client.get_utc();	//获取UTC时间，单位为小时

client.get_vtec(lat,lon,obs_hour1);	//获取对应时间、经纬度的VTEC

client.disconnect();	//中断与服务端的连接
```



