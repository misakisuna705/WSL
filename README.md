<!-- vim-markdown-toc GFM -->

+ [Chocolatey](#chocolatey)
    * [安裝](#安裝)
    * [命令](#命令)
    * [插件](#插件)
+ [WSL](#wsl)
    * [啟用](#啟用)
        - [虛擬化平台](#虛擬化平台)
        - [WSL 功能](#wsl-功能)
        - [WSL 2](#wsl-2)
    * [更新](#更新)
    * [部署](#部署)
        - [Ubuntu](#ubuntu)
        - [LxRunOffline](#lxrunoffline)

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

## 啟用

### 虛擬化平台

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

### WSL 功能

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

### WSL 2

```powershell
wsl --set-default-version 2
```

## 更新

-   [元件](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

## 部署

### Ubuntu

-   [載點](https://aka.ms/wsl-ubuntu-1804)

-   副檔名更改成 zip，並解壓縮

### LxRunOffline

```powershell
LxRunOffline i -n Ubuntu -d e:\WSL\Ubuntu -f  "C:\Users\[使用者名稱]\Downloads\Ubuntu_1804.2019.522.0_x64\install.tar.gz" -s
```
