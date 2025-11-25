# 在 Windows 上安装 Singularity 的完整指南
## 一、安装 WSL2
首先需要在 Windows 系统上安装 WSL2（Windows Subsystem for Linux）：
[WSL2 官方安装指南](https://learn.microsoft.com/zh-cn/windows/wsl/install)
## 二、安装Singularity
官方文档[Singularity 快速入门指南](https://docs.sylabs.io/guides/main/user-guide/quick_start.html)
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
