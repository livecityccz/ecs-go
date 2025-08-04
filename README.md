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

## **使用说明**

### **Linux/FreeBSD/MacOS**

#### **一键命令**

将默认安装依赖，默认更新包管理器，默认非互动模式，下面的非一键命令版本可控制是否安装依赖/是否更新包管理器/默认互动模式

- **国际用户无加速：**

  ```bash
  export noninteractive=true && curl -L https://raw.githubusercontent.com/livecityccz/ecs-go/master/goecs.sh -o goecs.sh && chmod +x goecs.sh && bash goecs.sh env && bash goecs.sh install && goecs
  ```

- **国际/国内使用 CDN 加速：**

  ```bash
  export noninteractive=true && curl -L https://cdn.spiritlhl.net/https://raw.githubusercontent.com/livecityccz/ecs-go/master/goecs.sh -o goecs.sh && chmod +x goecs.sh && bash goecs.sh env && bash goecs.sh install && goecs
  ```

- **国内用户使用 CNB 加速：**

  ```bash
  export noninteractive=true && curl -L https://cnb.cool/livecityccz/ecs-go/-/git/raw/main/goecs.sh -o goecs.sh && chmod +x goecs.sh && bash goecs.sh env && bash goecs.sh install && goecs
  ```

#### **详细说明**

1. **下载脚本**

   **国际用户无加速：**

   ```bash
   curl -L https://raw.githubusercontent.com/livecityccz/ecs-go/master/goecs.sh -o goecs.sh && chmod +x goecs.sh
   ```

   **国际/国内使用 CDN 加速：**

   ```bash
   curl -L https://cdn.spiritlhl.net/https://raw.githubusercontent.com/livecityccz/ecs-go/master/goecs.sh -o goecs.sh && chmod +x goecs.sh
   ```

   **国内用户使用 CNB 加速：**

   ```bash
   curl -L https://cnb.cool/livecityccz/ecs-go/-/git/raw/main/goecs.sh -o goecs.sh && chmod +x goecs.sh
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

1. 下载带 exe 文件的压缩包：[Releases](https://github.com/livecityccz/ecs-go/releases)
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

国内镜像地址：https://cnb.cool/livecityccz/ecs-go/-/packages/docker/ecs

请确保执行下述命令前本机已安装Docker

特权模式+host网络

```shell
docker run --rm --privileged --network host docker.cnb.cool/livecityccz/ecs-go:latest -menu=false -l zh
```

非特权模式+非host网络

```shell
docker run --rm docker.cnb.cool/livecityccz/ecs-go:latest -menu=false -l zh
```
