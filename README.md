<!-- vim-markdown-toc GFM -->

+ [Chocolatey](#chocolatey)
    * [安裝](#安裝)
    * [命令](#命令)
    * [插件](#插件)
+ [WSL](#wsl)
    * [功能啟用](#功能啟用)
        - [虛擬化平台](#虛擬化平台)
        - [WSL](#wsl-1)
        - [WSL 2](#wsl-2)
    * [元件更新](#元件更新)
    * [Linux 部署](#linux-部署)
        - [Ubuntu](#ubuntu)
        - [LxRunOffline](#lxrunoffline)
    * [登入設定](#登入設定)
        - [Linux 環境](#linux-環境)
        - [Windows 環境](#windows-環境)

<!-- vim-markdown-toc -->

---

# Chocolatey

## 安裝

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

## 命令

```powershell
choco search 插件 # 搜尋某插件與其相關插件
choco info 插件 # 查詢該插件詳細資料
choco install 插件 # 安裝該插件
choco uninstall 插件 # 解除安裝該插件
choco upgrade 插件 # 升級該插件
choco upgrade all # 升級所有插件
```

## 插件

```powershell
choco install lxrunoffline
```

# WSL

## 功能啟用

### 虛擬化平台

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

### WSL

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

### WSL 2

```powershell
wsl --set-default-version 2
```

## 元件更新

-   [載點](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

## Linux 部署

### Ubuntu

-   [載點](https://aka.ms/wsl-ubuntu-1804)

-   副檔名更改成 zip，並解壓縮

### LxRunOffline

```powershell
LxRunOffline i -n Ubuntu -d e:\WSL\Ubuntu -f  "C:\Users\[使用者名稱]\Downloads\Ubuntu_1804.2019.522.0_x64\install.tar.gz" -s
```

## 登入設定

### Linux 環境

```zsh
useradd -m -s /bin/bash [使用者名稱]
passwd [使用者名稱]
usermod -aG sudo [使用者名稱]
```

### Windows 環境

```powershell
lxrunoffline su -n Ubuntu -v 1000
```
