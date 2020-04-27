# linux下常用指令


* strace: 跟踪系统调用 
* ltrace: 跟踪库函数调用
    * 详细: https://www.cnblogs.com/isohybrid/archive/2012/11/05/strace.html 
* 在服务端使用nc -l 端口号 来进行监听，在客户端使用nc IP地址 端口号来建立连接。建立连接后，nc会把从stdin读入的字节流发送给另一方，把接收到的字节流写入stdout中
    * nc localhost 2333
    * nc -l 2333

* ps lax | grep /bin/login |awk '{print $3}' |xargs sudo kill -9

* ps lax 带ppid

* ps aux 详细信息

* awk '{print $3}' 打印前面筛选的结果的第三行

* xargs 将前面的输出作为kill -9 的参数

* sudo netstat -anop 查看当前socket处于各状态的进程信息包括PID

* netstat -an | awk '/^tcp/ {++S[$NF]}  END {for (a in S) print a,S[a]} ' 统计机器中网络连接各个状态个数

* netstat -ant|awk '{print $6}'|sort|uniq –c 把状态全都取出来后使用uniq -c统计后再进行排序



* xxx > xxx  重定向 :左边为程序,右边为文件

* xxx | xxx  管道 :左边为程序,右边也为程序

* sh -i fork出一个进程,执行指定指令

* ltrace 显示程序库函数调用 ltrace -S 库函数包装的系统调用 strace 着眼于系统调用 

* nmap 网络嗅探工具

* traceroute icmp/tcp/udp 利用TTL探索路由路径

* 端口转发详见 https://www.cnblogs.com/fundebug/p/ssh-port-forwarding.html

* ssh -R localhost:2000:localhost:3000 root@103.59.22.17远端端口转发
    * 在远程云主机A1可以通过访问http://localhost:2000来访问本地主机的3000端口开启的服务(如web服务)
    * 在远程云主机B1(103.59.22.17)访问本地主机A1(内网机子)上的web服务 通过curl http://localhost:2000

* ssh -L localhost:2000:localhost:3000 root@103.59.22.17本地端口转发
    * 通过本地端口转发，可以将发送到本地主机A1端口2000的请求，转发到远程云主机B1的3000端口。
    * 这样，在本地主机A1上可以通过访问http://localhost:2000来访问远程云主机B1上的Node.js服务。在本地主机A1访问远程云主机B1上的Node.js服务  curl http://localhost:2000

* curl 是常用的命令行工具，用来请求 Web 服务器。它的名字就是客户端（client）的 URL 工具的意思 详见http://www.ruanyifeng.com/blog/2019/09/curl-reference.html
    * curl https://www.example.com/WebProject/index.html
    * curl -d'login=emma＆password=123'-X POST https://google.com/login
