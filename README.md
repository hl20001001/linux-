# Nmap

Nmap是一个网络扫描和主机发现工具。它被广泛用于安全评估和网络管理。

## 导航

- [主机选择](#主机选择)
- [主机发现](#主机发现)
- [扫描技术](#扫描技术)
- [端口指定和扫描顺序](#端口指定和扫描顺序)
- [服务/版本检测](#服务版本检测)
- [脚本扫描](#脚本扫描)
- [OS检测](#os检测)
- [时序和性能](#时序和性能)
- [防火墙/IDS规避和欺骗](#防火墙ids规避和欺骗)
- [输出](#输出)
- [其他选项](#其他选项)

## 主机选择
- `-iL <inputfilename>`：从列表中选择主机/网络进行输入
- `-iR <num hosts>`：随机选择目标
- `--exclude <host1[,host2][,host3],...>`：排除主机/网络
- `--excludefile <exclude_file>`：从文件中排除列表

## 主机发现
- `-sL`：列表扫描 - 只列出要扫描的目标
- `-sn`：Ping扫描 - 禁用端口扫描
- `-Pn`：将所有主机视为在线 -- 跳过主机发现
- `-PE/PP/PM`：ICMP回声，时间戳和网络掩码请求发现探测
- `-PO[protocol list]`：IP协议Ping
- `-n/-R`：从不进行DNS解析/始终解析
- `--dns-servers <serv1[,serv2],...>`：指定自定义DNS服务器
- `--system-dns`：使用操作系统的DNS解析器
- `--traceroute`：跟踪每个主机的跃点路径

## 扫描技术
- `-sS/sT/sA/sW/sM`：TCP SYN/Connect()/ACK/Window/Maimon扫描
- `-sU`：UDP扫描
- `-sN/sF/sX`：TCP Null，FIN和Xmas扫描
- `--scanflags <flags>`：自定义TCP扫描标志
- `-sI <zombie host[:probeport]>`：空闲扫描
- `-sY/sZ`：SCTP INIT/COOKIE-ECHO扫描
- `-sO`：IP协议扫描
- `-b <FTP relay host>`：FTP弹跳扫描

## 端口指定和扫描顺序
- `-p <port ranges>`：只扫描指定的端口
- `--exclude-ports <port ranges>`：从扫描中排除指定的端口
- `-F`：快速模式 - 扫描的端口少于默认扫描
- `-r`：顺序扫描端口 - 不随机化
- `--top-ports <number>`：扫描最常见的<number>个端口
- `--port-ratio <ratio>`：扫描比<ratio>更常见的端口

## 服务/版本检测
- `-sV`：探测开放端口以确定服务/版本信息
- `--version-intensity <level>`：设置从0（轻）到9（尝试所有探测）
- `--version-light`：限制为最可能的探测（强度2）
- `--version-all`：尝试每一个单独的探测（强度9）
- `--version-trace`：显示详细的版本扫描活动（用于调试）

## 脚本扫描
- `-sC`：等同于--script=default
- `--script=<Lua scripts>`：逗号分隔的目录，脚本文件或脚本类别列表
- `--script-args=<n1=v1,[n2=v2,...]>`：为脚本提供参数
- `--script-args-file=filename`：在文件中提供NSE脚本参数
- `--script-trace`：显示所有发送和接收的数据
- `--script-updatedb`：更新脚本数据库
- `--script-help=<Lua scripts>`：显示关于脚本的帮助

## OS检测
- `-O`：启用OS检测
- `--osscan-limit`：将OS检测限制为有前途的目标
- `--osscan-guess`：更积极地猜测OS

## 时序和性能
- `-T<0-5>`：设置时序模板（越高越快）
- `--min-hostgroup/max-hostgroup <size>`：并行主机扫描组大小
- `--min-parallelism/max-parallelism <numprobes>`：探测并行化
- `--min-rtt-timeout/max-rtt-timeout/initial-rtt-timeout <time>`：指定探测往返时间
- `--max-retries <tries>`：限制端口扫描探测重传次数
- `--host-timeout <time>`：在此时间后放弃目标
- `--scan-delay/--max-scan-delay <time>`：调整探测之间的延迟
- `--min-rate <number>`：发送数据包的速度不低于<number>每秒
- `--max-rate <number>`：发送数据包的速度不超过<number>每秒

## 防火墙/IDS规避和欺骗
- `-f; --mtu <val>`：分片数据包（可选带给定的MTU）
- `-D <decoy1,decoy2[,ME],...>`：用诱饵掩盖扫描
- `-S <IP_Address>`：欺骗源地址
- `-e <iface>`：使用指定的接口
- `-g/--source-port <portnum>`：使用给定的端口号
- `--proxies <url1,[url2],...>`：通过HTTP/SOCKS4代理中继连接
- `--data <hex string>`：将自定义有效载荷附加到发送的数据包中
- `--data-string <string>`：将自定义ASCII字符串附加到发送的数据包中
- `--data-length <num>`：将随机数据附加到发送的数据包中
- `--ip-options <options>`：发送带有指定IP选项的数据包
- `--ttl <val>`：设置IP生存时间字段
- `--spoof-mac <mac address/prefix/vendor name>`：欺骗你的MAC地址
- `--badsum`：发送带有错误的TCP/UDP/SCTP校验和的数据包

## 输出
- `-oN/-oX/-oS/-oG <file>`：将扫描结果以正常，XML，s|<rIpt kIddi3，和可grep的格式输出到给定的文件名
- `-oA <basename>`：一次性以三种主要格式输出
- `-v`：增加详细程度级别（使用-vv或更多以获得更大的效果）
- `-d`：增加调试级别（使用-dd或更多以获得更大的效果）
- `--reason`：显示端口处于特定状态的原因
- `--open`：只显示开放的（或可能开放的）端口
- `--packet-trace`：显示所有发送和接收的数据包
- `--iflist`：打印主机接口和路由（用于调试）
- `--append-output`：追加而不是覆盖指定的输出文件
- `--resume <filename>`：恢复中断的扫描
- `--noninteractive`：禁用键盘的运行时交互
- `--stylesheet <path/URL>`：XSL样式表将XML输出转换为HTML
- `--webxml`：从Nmap.Org引用样式表以获得更便携的XML
- `--no-stylesheet`：阻止将XSL样式表与XML输出关联

## 杂项
- `-6`：启用IPv6扫描
- `-A`：启用OS检测，版本检测，脚本扫描和路由跟踪
- `--datadir <dirname>`：指定自定义Nmap数据文件位置
- `--send-eth/--send-ip`：发送使用原始以太网帧或IP数据包
- `--privileged`：假设用户具有完全的权限
- `--unprivileged`：假设用户没有原始套接字权限
- `-V`：打印版本号

请注意，此处列出的选项只是Nmap的一小部分。要获取完整的选项列表和更详细的文档，请查看[Nmap官方文档](https://nmap.org/book/man.html)。

