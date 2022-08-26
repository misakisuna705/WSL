# Windows Subsystem for Linux

<!-- vim-markdown-toc GFM -->

* [Chocolatey](#chocolatey)
    - [安裝](#安裝)
    - [命令](#命令)
    - [插件](#插件)
* [WSL](#wsl)
    - [功能啟用](#功能啟用)
        + [虛擬化平台](#虛擬化平台)
        + [WSL](#wsl-1)
        + [WSL2](#wsl2)
    - [元件更新](#元件更新)
    - [系統部署](#系統部署)
        + [下載](#下載)
        + [安裝](#安裝-1)
    - [登入設定](#登入設定)
        + [Ubuntu 環境](#ubuntu-環境)
        + [Windows 環境](#windows-環境)
    - [環境更新](#環境更新)
* [Remote](#remote)
    - [Windows](#windows)
        + [ssh](#ssh)
            * [OpenSSH 版本檢視](#openssh-版本檢視)
            * [ssh server 安裝](#ssh-server-安裝)
            * [開機自動啓動](#開機自動啓動)
        + [vpn](#vpn)
    - [WSL](#wsl-2)
        + [ssh](#ssh-1)
            * [安裝 ssh server](#安裝-ssh-server)
            * [/etc/ssh/sshd_config](#etcsshsshd_config)
            * [開機自動啓動](#開機自動啓動-1)
                - [Linux 環境](#linux-環境)
                - [Windows 環境](#windows-環境-1)
        + [vpn](#vpn-1)

<!-- vim-markdown-toc -->

---

## Chocolatey

### 安裝

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

### 命令

```powershell
choco search 插件 # 搜尋某插件與其相關插件
choco info 插件 # 查詢該插件詳細資料
choco install 插件 # 安裝該插件
choco uninstall 插件 # 解除安裝該插件
choco upgrade 插件 # 升級該插件
choco upgrade all # 升級所有插件
```

### 插件

```powershell
choco install lxrunoffline
```

## WSL

### 功能啟用

#### 虛擬化平台

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

#### WSL

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

#### WSL2

```powershell
wsl --set-default-version 2
```

### 元件更新

-   [元件載點](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

### 系統部署

#### 下載

-   [Ubuntu 載點](https://aka.ms/wsl-ubuntu-1804)後
-   副檔名更改成 zip，並解壓縮

#### 安裝

```powershell
LxRunOffline i -n Ubuntu -d e:\WSL\Ubuntu -f  "C:\Users\[使用者名稱]\Downloads\Ubuntu_1804.2019.522.0_x64\install.tar.gz" -s
```

### 登入設定

#### Ubuntu 環境

```zsh
useradd -m -s /bin/bash [使用者名稱]
passwd [使用者名稱]
usermod -aG sudo [使用者名稱]
```

#### Windows 環境

```powershell
lxrunoffline su -n Ubuntu -v 1000
```

### 環境更新

```zsh
sudo apt update
sudo apt upgrade -y
sudo apt dist-upgrade
sudo apt autoclean
sudo apt autoremove -y
```

## Remote

### Windows

#### ssh

##### OpenSSH 版本檢視

```powershell
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
```

##### ssh server 安裝

```powershell
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

##### 開機自動啓動

```powershell
Get-Service -Name sshd | Set-Service -StartupType Auto
```

#### vpn

-   Zerotier 安裝

```powershell
choco install zerotier-one
```

### WSL

#### ssh

##### 安裝 ssh server

```zsh
sudo apt install -y openssh-server
```

##### /etc/ssh/sshd_config

```apacheconf
PasswordAuthentication yes
```

##### 開機自動啓動

###### Linux 環境

-   /etc/init.wsl

```zsh
#! /bin/sh
/etc/init.d/ssh $1
/etc/init.d/zerotier-one
```

-   可執行設定

```zsh
sudo chmod u+x /etc/init.wsl
```

###### Windows 環境

-   C:\Users\[使用者名稱]\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\Ubuntu.vbs

```vbnet
Set ws = CreateObject("Wscript.Shell")
ws.run "wsl -d Ubuntu -u root /etc/init.wsl start", vbhide
```

#### vpn

-   Zerotier 安裝

```zsh
curl -s https://install.zerotier.com | sudo bash
```

-   VLAN 加入

```zsh
sudo zerotier-cli join [號碼]
```
