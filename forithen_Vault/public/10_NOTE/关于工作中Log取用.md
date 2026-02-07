关于Linux详细学习笔记
[[Linux操作系统学习]]
相关阅读
[[关于Shell]]


# 关于Server这个概念
### 第 1 层：物理 / 虚拟服务器（Machine / Host）

- 一台物理机
    
- 或一台 VM / EC2
    
- 特点：
    
    - CPU
        
    - 内存
        
    - 磁盘
        
    - OS（Linux）
        

👉 更准确的英文是：

- **host**
    
- **machine**
    
- **node**
    

但日常口语里，大家也直接叫 **server**。

### 第 2 层：操作系统层（OS）

比如：

- Linux  
    -（极少数）Windows Server
    

这是：

- 你 ssh 登录的对象
    
- 你用 `ls / grep / tail` 的地方
    

### 第 3 层：应用服务器（Application Server）

比如：

- Tomcat
    
- JBoss
    
- WebLogic
    
- Nginx
    
- MySQL（数据库 server）
    

👉 这是：

- 跑在 OS 上的“服务进程”
    
- 负责提供某种功能

# 为什么服务器「大部分是 Linux」
服务器选 Linux，不是因为它“强”，  
而是因为它“可控、可自动化、可长期稳定运行”
## 几个现实原因（和你工作强相关）

### 🔹 1）稳定、能跑几年不重启

- Linux 可以：
    
    - 连续跑 **几百天**
        
    - 不重启、不更新
        
- 金融系统：
    
    - 批处理
        
    - 月末
        
    - 年末  
        👉 **最怕重启引发未知风险**
### 🔹 2）远程操作和自动化极强
Linux：

- 天然适合脚本
    
- cron / batch 非常成熟
    
- 和 CI/CD 完美适配

# linux取Log常用命令
## 1️⃣ 看 log 的“入口命令”

### `cd`：进 log 目录

`cd /opt/tomcat/logs cd /var/log`

---

### `ls -ltr`：看有哪些 log（必用）

`ls -ltr`

含义你可以这样记：

- `-l`：详细信息
    
- `-t`：按时间
    
- `-r`：反过来（旧 → 新）
    

👉 **最新的 log 通常在最下面**

---

## 2️⃣ 实时看 log（最常用）

### `tail -f`

`tail -f catalina.out`

- `tail`：看文件末尾
    
- `-f`：follow，持续追踪
    

📌 场景：

- 重现问题
    
- 看 batch / 请求实时输出
    

---

### `tail -n 100`

`tail -n 100 app.log`

👉 看最后 100 行（比全部 cat 安全）

---

## 3️⃣ 查关键字（定位问题核心）

### `grep`（核心中的核心）

`grep ERROR app.log grep -i error app.log`

- `-i`：忽略大小写
    

---

### 常见组合（非常实用）

`grep ERROR app.log | tail -n 50`

👉 **只看最近 50 条 ERROR**

---

### 查某个时间段（进阶）

`grep "2026-02-03 11:" app.log`

---

## 4️⃣ 不要轻易用 `cat`（血的教训）

`cat huge.log   # ❌ 很容易把终端卡死`

替代方案：

`less huge.log`

- 支持上下翻
    
- `/ERROR` 搜索
    
- `q` 退出
    

👉 **读大 log，默认用 `less`**

---

## 5️⃣ 多 log / 轮转

`app.log app.log.1 app.log.2.gz`

### 看压缩 log

`zcat app.log.2.gz | grep ERROR`

---

## 6️⃣ Tomcat 常见 log（你以后会反复见）

`catalina.out        # stdout / stderr（最常看） localhost.log manager.log access_log*.txt     # 访问日志`


## 基本移动 / 查看
```
pwd                       # 当前目录
cd /path/to/dir           # 切换目录
cd ..                     # 上一级
ls                        # 列文件
ls -l                     # 详细
ls -ltr                   # 按时间排序（旧→新）

```

### 文件查看（重点）
```
cat file.txt              # 输出全文（小文件）
less file.txt             # 安全查看大文件（/搜索，q退出）
head file.txt             # 前10行
head -n 50 file.txt       # 前50行
tail file.txt             # 后10行
tail -n 100 file.txt      # 后100行
tail -f file.txt          # 实时追踪

```

### 查找关键字（日志必用）
```
grep ERROR file.log
grep -i error file.log
grep -n ERROR file.log
grep -v DEBUG file.log

```
```
grep ERROR *.log
grep ERROR file.log | tail -n 50

```
### 管道（|）——核心思想
```
前一个命令的输出 → 后一个命令的输入

cat file.log | grep ERROR
grep ERROR file.log | tail -n 20
tail -f app.log | grep Exception


```

### 排序 / 统计（日志分析）
```
sort file.txt
sort | uniq
sort | uniq -c
sort | uniq -c | sort -nr

grep ERROR app.log | wc -l

```

### 查时间 / 范围
```
grep "2026-02-03" app.log
grep "11:2" app.log

```

### 压缩日志
```
zcat app.log.1.gz
zcat app.log.1.gz | grep ERROR

```

### 查进程（服务器必用）
```
ps -ef
ps -ef | grep java
ps -ef | grep tomcat

top

```

### 查端口
```
netstat -an | grep 8080
ss -lntp | grep 8080

```

### 磁盘 / 容量
```
df -h
du -sh *
du -sh logs/

```

### 权限 / 所属
```
ls -l
chmod 755 script.sh
chmod +x script.sh
chown user:group file

```

### 搜文件
```
find . -name "*.log"
find /opt -type f | grep catalina

```

### 环境变量
```
env
echo $PATH
export VAR=value

```

### 重定向（很重要）
```
command > out.txt
command >> out.txt
command 2> err.txt
command > all.txt 2>&1

```

### 一些“组合拳”（你工作里会常用）
tail -f catalina.out | grep ERROR

---

grep Exception app.log | wc -l 
`wc` = word count，用来“数数量”的命令

例如 wc file.txt
 输出 行数  单词数  字节数  文件名
wc -l 表示只计算行数
 grep ERROR app.log | wc -l 有多少行包含 ERROR

---

zcat app.log.2.gz | grep ERROR | tail -n 20
zcat app.log.2.gz | grep ERROR | tail -n 20


---

ps -ef | grep java | grep -v grep
`ps` = process status，用来“看当前在跑什么进程”

ps -ef 列出系统里“所有正在运行的进程”
输出的每列对应的是如下
UID   PID  PPID  C  STIME  TTY  TIME  CMD
需要关注
- **PID**：进程号（kill 用）
    
- **UID**：谁启动的
    
- **CMD**：跑的是什么程序