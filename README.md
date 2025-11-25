# 在 Windows 上安装SingularityCE 的完整指南
## 一、安装 WSL2
首先需要在 Windows 系统上安装 WSL2（Windows Subsystem for Linux）：
[WSL2 官方安装指南](https://learn.microsoft.com/zh-cn/windows/wsl/install)
## 二、安装 SingularityCE
### 1. 启动 Windows Subsystem for Linux (WSL)
 [Windows 系统安装说明](https://docs.sylabs.io/guides/main/admin-guide/installation.html#windows)
* 以管理员身份运行PowerShell
* 执行命令启动 WSL：

        wsl
### 2. 安装 SingularityCE
在 WSL 环境中执行以下步骤：
* 进入家目录
  
        cd ~
* 检查当前路径（确认在正确位置）
  
        pwd  # 应该显示 /home/username
* 下载并安装 SingularityCE
    
        wget https://github.com/sylabs/singularity/releases/download/v4.0.0/singularity-ce_4.0.0-jammy_amd64.deb
          sudo apt install ./singularity-ce_4.0.0-jammy_amd64.deb
* 验证安装

        singularity --version
        singularity exec library://ubuntu echo "Hello World!"
## 三、 实战：核心操作入门
### 1. 拉取镜像：从云端库获取现成的容器
    singularity pull library://sylabsed/examples/lolcow
    singularity pull ubuntu.sif library://ubuntu
### 2. 运行容器：执行容器默认的程序
运行命令后，终端会显示一幅由字符组成的牛形图案，并附带一条随机的幽默名言或笑话。
        
    singularity run lolcow_latest.sif
### 3.交互模式：进入容器内部进行操作
本例演示如何进入一个只读的 .sif 容器镜像并进行探查。此类操作不会改变容器本身，适用于运行稳定、可复现的任务。
    
    #进入容器内部
    singularity shell ubuntu.sif
    # 检查容器内的系统信息
    Singularity> cat /etc/os-release
    #查看磁盘空间
    Singularity> df -h
    #退出容器
    Singularity> exit
### 4.绑定目录：在容器中访问主机上的文件
## 四、实战：封装并运行生物信息学工作流
### 1.Singularity基础知识
* build可以生产两种不同格式的容器
   *  SIF（Singularity Image File）：压缩后的只读的Singularity镜像文件，是生产使用的主要形式。确保了容器的可复现性和验证性。
   * Sandbox ：可写的容器存在形式，是文件系统中的一个目录，常用于开发或者创建自己的容器，是开发使用的主要形式。

