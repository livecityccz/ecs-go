## **适配系统和架构**

### **编译支持的架构**

- amd64、arm、arm64、386、mips、mipsle、s390x、riscv64

### **测试支持的架构**

- amd64、arm64

> 更多架构请自行测试。

### **编译支持的系统**

- Linux、Windows、MacOS、FreeBSD、OpenBSD

### **测试支持的系统**

- Linux、Windows

> 更多系统请自行测试。

### **待支持的系统**

- MacOS、FreeBSD、OpenBSD（存在硬件测试 BUG 未修复）

---

## **功能**

- 系统基础信息查询，IP基础信息并发查询：  
  自研 [basics](https://github.com/oneclickvirt/basics)、[gostun](https://github.com/oneclickvirt/gostun)
- CPU 测试：  
  自研 [cputest](https://github.com/oneclickvirt/cputest)，支持 sysbench(lua/golang版本)、geekbench、winsat
- 内存测试：  
  自研 [memorytest](https://github.com/oneclickvirt/memorytest)，支持 sysbench、dd
- 硬盘测试：  
  自研 [disktest](https://github.com/oneclickvirt/disktest)，支持 dd、fio、winsat
- 流媒体解锁信息并发查询：  
  借鉴 [netflix-verify](https://github.com/sjlleo/netflix-verify) 等逻辑，开发至 [CommonMediaTests](https://github.com/oneclickvirt/CommonMediaTests)
- 常见流媒体测试并发查询：  
  自研至 [UnlockTests](https://github.com/oneclickvirt/UnlockTests)，逻辑借鉴 [RegionRestrictionCheck](https://github.com/lmc999/RegionRestrictionCheck) 等
- IP 质量/安全信息并发查询：  
  自研，二进制文件编译至 [securityCheck](https://github.com/oneclickvirt/securityCheck)
- 邮件端口测试：  
  自研 [portchecker](https://github.com/oneclickvirt/portchecker)
- 三网回程测试：  
  借鉴 [zhanghanyun/backtrace](https://github.com/zhanghanyun/backtrace)，二次开发至 [oneclickvirt/backtrace](https://github.com/oneclickvirt/backtrace)
- 三网路由测试：  
  基于 [NTrace-core](https://github.com/nxtrace/NTrace-core)，二次开发至 [nt3](https://github.com/oneclickvirt/nt3)
- 网速测试：  
  基于 [speedtest.net](https://github.com/spiritLHLS/speedtest.net-CN-ID) 和 [speedtest.cn](https://github.com/spiritLHLS/speedtest.cn-CN-ID) 数据，开发至 [oneclickvirt/speedtest](https://github.com/oneclickvirt/speedtest)
- 三网 Ping 值测试：  
  借鉴 [ecsspeed](https://github.com/spiritLHLS/ecsspeed)，二次开发至 [pingtest](https://github.com/oneclickvirt/pingtest)

---

## **使用说明**

### **Linux/FreeBSD/MacOS**

#### **一键命令**

将默认安装依赖，默认更新包管理器，默认非互动模式，下面的非一键命令版本可控制是否安装依赖/是否更新包管理器/默认互动模式

- **国际用户无加速：**

  ```bash
  export noninteractive=true && curl -L https://raw.githubusercontent.com/oneclickvirt/ecs/master/goecs.sh -o goecs.sh && chmod +x goecs.sh && bash goecs.sh env && bash goecs.sh install && goecs
  ```

- **国际/国内使用 CDN 加速：**

  ```bash
  export noninteractive=true && curl -L https://cdn.spiritlhl.net/https://raw.githubusercontent.com/oneclickvirt/ecs/master/goecs.sh -o goecs.sh && chmod +x goecs.sh && bash goecs.sh env && bash goecs.sh install && goecs
  ```

- **国内用户使用 CNB 加速：**

  ```bash
  export noninteractive=true && curl -L https://cnb.cool/oneclickvirt/ecs/-/git/raw/main/goecs.sh -o goecs.sh && chmod +x goecs.sh && bash goecs.sh env && bash goecs.sh install && goecs
  ```

#### **详细说明**

1. **下载脚本**

   **国际用户无加速：**

   ```bash
   curl -L https://raw.githubusercontent.com/oneclickvirt/ecs/master/goecs.sh -o goecs.sh && chmod +x goecs.sh
   ```

   **国际/国内使用 CDN 加速：**

   ```bash
   curl -L https://cdn.spiritlhl.net/https://raw.githubusercontent.com/oneclickvirt/ecs/master/goecs.sh -o goecs.sh && chmod +x goecs.sh
   ```

   **国内用户使用 CNB 加速：**

   ```bash
   curl -L https://cnb.cool/oneclickvirt/ecs/-/git/raw/main/goecs.sh -o goecs.sh && chmod +x goecs.sh
   ```

2. **更新包管理器（可选择）并安装环境**

   ```bash
   ./goecs.sh env
   ```

   **非互动模式：**

   ```bash
   export noninteractive=true && ./goecs.sh env
   ```

3. **安装 `goecs`**

   ```bash
   ./goecs.sh install
   ```

4. **升级 `goecs`**

   ```bash
   ./goecs.sh upgrade
   ```

5. **卸载 `goecs`**

   ```bash
   ./goecs.sh uninstall
   ```

6. **帮助命令**

   ```bash
   ./goecs.sh -h
   ```

7. **唤起菜单**

   ```bash
   goecs
   ```

#### **命令参数化**

<details>
<summary>展开查看各参数说明</summary>

```bash
Usage: goecs [options]
  -backtrace
        Enable/Disable backtrace test (in 'en' language or on windows it always false) (default true)
  -basic
        Enable/Disable basic test (default true)
  -comm
        Enable/Disable common media test (default true)
  -cpu
        Enable/Disable CPU test (default true)
  -cpum string
        Set CPU test method (supported: sysbench, geekbench, winsat) (default "sysbench")
  -cput string
        Set CPU test thread mode (supported: single, multi) (default "multi")
  -disk
        Enable/Disable disk test (default true)
  -diskm string
        Set disk test method (supported: fio, dd, winsat) (default "fio")
  -diskmc
        Enable/Disable multiple disk checks, e.g., -diskmc=false
  -diskp string
        Set disk test path, e.g., -diskp /root
  -email
        Enable/Disable email port test (default true)
  -h    Show help information
  -l string
        Set language (supported: en, zh) (default "zh")
  -log
        Enable/Disable logging in the current path
  -memory
        Enable/Disable memory test (default true)
  -memorym string
        Set memory test method (supported: sysbench, dd, winsat) (default "sysbench")
  -menu
        Enable/Disable menu mode, disable example: -menu=false (default true)
  -nt3
        Enable/Disable NT3 test (in 'en' language or on windows it always false) (default true)
  -nt3loc string
        Specify NT3 test location (supported: GZ, SH, BJ, CD for Guangzhou, Shanghai, Beijing, Chengdu) (default "GZ")
  -nt3t string
        Set NT3 test type (supported: both, ipv4, ipv6) (default "ipv4")
  -security
        Enable/Disable security test (default true)
  -speed
        Enable/Disable speed test (default true)
  -spnum int
        Set the number of servers per operator for speed test (default 2)
  -upload
        Enable/Disable upload the result (default true)
  -ut
        Enable/Disable unlock media test (default true)
  -v    Display version information
```
</details>

---

### **Windows**

1. 下载带 exe 文件的压缩包：[Releases](https://github.com/oneclickvirt/ecs/releases)
2. 解压后，右键以管理员模式运行。

---

### **Docker**

国际镜像地址：https://hub.docker.com/r/spiritlhl/goecs

请确保执行下述命令前本机已安装Docker

特权模式+host网络

```shell
docker run --rm --privileged --network host spiritlhl/goecs:latest -menu=false -l zh
```

非特权模式+非host网络

```shell
docker run --rm spiritlhl/goecs:latest -menu=false -l zh
```

使用Docker执行测试，硬件测试会有一些偏差和虚拟化架构判断失效，还是推荐直接测试而不使用Docker测试。

国内镜像地址：https://cnb.cool/oneclickvirt/ecs/-/packages/docker/ecs

请确保执行下述命令前本机已安装Docker

特权模式+host网络

```shell
docker run --rm --privileged --network host docker.cnb.cool/oneclickvirt/ecs:latest -menu=false -l zh
```

非特权模式+非host网络

```shell
docker run --rm docker.cnb.cool/oneclickvirt/ecs:latest -menu=false -l zh
```

我来帮你修复排版，以下是格式调整后的完整内容：

### 从源码中进行编译

<details>
<summary>展开查看编译说明</summary>

1. 克隆仓库的 public 分支（不含私有依赖）
```bash
git clone -b public https://github.com/oneclickvirt/ecs.git
cd ecs
```

2. 安装 Go 环境（如已安装可跳过）
```bash
# 下载并安装 Go
wget https://go.dev/dl/go1.23.4.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.23.4.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
```

3. 编译
```bash
go build -o goecs
```

4. 运行测试
```bash
./goecs -menu=false -l zh
```