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
### 3. 交互模式：进入容器内部进行操作
本例演示如何进入一个只读的 .sif 容器镜像并进行探查。此类操作不会改变容器本身，适用于运行稳定、可复现的任务。
    
    #进入容器内部
    singularity shell ubuntu.sif
    # 检查容器内的系统信息
    Singularity> cat /etc/os-release
    #查看磁盘空间
    Singularity> df -h
    #退出容器
    Singularity> exit
### 4. 绑定目录：在容器中访问主机上的文件
## 四、实战：封装并运行生物信息学工作流
### 1. Singularity基础知识
* build可以生产两种不同格式的容器
   *  SIF（Singularity Image File）：压缩后的只读的Singularity镜像文件，是生产使用的主要形式。确保了容器的可复现性和验证性。
   * Sandbox ：可写的容器存在形式，是文件系统中的一个目录，常用于开发或者创建自己的容器，是开发使用的主要形式。
* 两种容器格式之间的转换
   * sif 转 sandbox（只读 → 可写）

           #这会创建一个名为 my_sandbox 的目录，您可以在里面自由安装软件、修改配置。
           # 将只读的 .sif 文件转换为可写的沙盒目录
           singularity build --sandbox ./my_sandbox/ ubuntu.sif
   * sandbox 转 sif
 
           #将定制好的环境固化为一个便携的、不可变的镜像文件，便于分发和部署。
           # 将沙盒目录打包回只读的 .sif 文件
           singularity build final_container.sif ./my_sandbox/
### 2. 构建自定义容器
#### Docker vs Singularity 构建机制对比：
Singularity采用单次构建机制，相比Docker的分层缓存构建，在调试阶段效率较低。* 任何一步出错，都需要从头开始执行整个构建过程.
为此我们推荐三阶段工作流：
* 沙盒调试 - 在可写环境中交互式验证配置
* 配方固化 - 将成功配置写入Definition File
* 最终构建 - 一次性生成生产就绪的SIF镜像
这种流程既保证了开发调试的灵活性，又确保了最终镜像的稳定性和可复现性。
#### 构建定制化容器——OFF-PEAK
##### （1）Sandbox 实验阶段
* sif 转 sandbox
通过一下命令，# 在 Windows 上安装SingularityCE 的完整指南
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
### 3. 交互模式：进入容器内部进行操作
本例演示如何进入一个只读的 .sif 容器镜像并进行探查。此类操作不会改变容器本身，适用于运行稳定、可复现的任务。
    
    #进入容器内部
    singularity shell ubuntu.sif
    # 检查容器内的系统信息
    Singularity> cat /etc/os-release
    #查看磁盘空间
    Singularity> df -h
    #退出容器
    Singularity> exit
### 4. 绑定目录：在容器中访问主机上的文件
## 四、实战：封装并运行生物信息学工作流
### 1. Singularity基础知识
* build可以生产两种不同格式的容器
   *  SIF（Singularity Image File）：压缩后的只读的Singularity镜像文件，是生产使用的主要形式。确保了容器的可复现性和验证性。
   * Sandbox ：可写的容器存在形式，是文件系统中的一个目录，常用于开发或者创建自己的容器，是开发使用的主要形式。
* 两种容器格式之间的转换
   * sif 转 sandbox（只读 → 可写）

           #这会创建一个名为 my_sandbox 的目录，您可以在里面自由安装软件、修改配置。
           # 将只读的 .sif 文件转换为可写的沙盒目录
           singularity build --sandbox ./my_sandbox/ ubuntu.sif
   * sandbox 转 sif
 
           #将定制好的环境固化为一个便携的、不可变的镜像文件，便于分发和部署。
           # 将沙盒目录打包回只读的 .sif 文件
           singularity build final_container.sif ./my_sandbox/
### 2. 构建自定义容器
#### Docker vs Singularity 构建机制对比：
Singularity采用单次构建机制，相比Docker的分层缓存构建，在调试阶段效率较低。* 任何一步出错，都需要从头开始执行整个构建过程.
为此我们推荐三阶段工作流：
* 沙盒调试 - 在可写环境中交互式验证配置
* 配方固化 - 将成功配置写入Definition File
* 最终构建 - 一次性生成生产就绪的SIF镜像
这种流程既保证了开发调试的灵活性，又确保了最终镜像的稳定性和可复现性。
#### 构建定制化容器——OFF-PEAK
##### （1）Sandbox 实验阶段
* **sif 转 sandbox**  通过以下命令，将只读的 ubuntu.sif 镜像转换为一个名为 ubuntu_sandbox 的可写目录，以便在容器内自由安装软件或修改配置。

        singularity build --sandbox ./ubuntu_sandbox/ ubuntu.sif
* **进入可写的沙盒环境** 通过以下命令，以可写模式启动一个交互式 Shell，进入之前构建的 ubuntu_sandbox 沙盒容器，允许您直接在其中安装软件或修改文件。

        singularity shell --writable ./ubuntu_sandbox/
* **基础系统配置**
    * **设置环境变量** 告诉 apt 工具以非交互模式运行，安装过程中不会弹出任何需要用户输入的对话框（如时区选择、服务配置等），实现全自动安装
 
            Singularity> export DEBIAN_FRONTEND=noninteractive
    * **设置语言环境** 设置系统语言和字符编码为 C.UTF-8，避免因语言环境导致的警告信息，确保命令行输出稳定一致

            Singularity> export LANG=C.UTF-8 LC_ALL=C.UTF-8
 
    * **替换软件源** 将 Ubuntu 官方软件源替换为阿里云镜像源，在国内网络环境下获得更快的下载速度
 
            Singularity> sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list
            Singularity> sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list
    * **刷新软件包列表缓存**   获取当前所有可用软件包的最新版本信息和依赖关系，为后续的 apt-get install 命令提供准确的软件包数据库
 
            Singularity> apt-get update
* **安装系统工具**

       Singularity> apt-get install -y --no-install-recommends \
    ca-certificates wget curl gnupg2 software-properties-common \
    build-essential \
    zlib1g-dev libcurl4-openssl-dev libssl-dev libxml2-dev libpng-dev \
    python3 python3-pip bedtools

  
        
        
        
  


           



