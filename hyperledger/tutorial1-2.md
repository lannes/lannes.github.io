# **Cài đặt trên Windows 10**

# **MỤC LỤC**
* [1. Install Ubuntu](#1-Install-Ubuntu)
* [2. Install Docker](#2-Install-Docker)
    * [2.1. Setting Docker](#21-Setting-Docker)
    * [2.1. Install Docker Compose](#21-Install-Docker-Compose)
* [3. Install support tools](#3-Install-support-tools)
    * [3.1. Install Go](#31-Install-Go)
    * [3.2. Install NodeJs](#32-Install-NodeJs)
* [4. Mount drive](#4-Mount-drive)
    * [4.1. Share drive](#41-Share-drive)
    * [4.2. Mount drive](#42-Mount-drive)

## **1. Install Ubuntu**

1. Enable Hyper-V

![](./images/setup1.png)

2. Enable Windows Subsystem for Linux

![](./images/setup2.png)

3. Install Ubuntu

    Vào Windows Store tìm Ubuntu và cài đặt

## **2. Install Docker**

Làm theo hướng dẫn ở đây để cài đặt Docker cho Windows: [https://docs.docker.com/docker-for-windows/install](https://docs.docker.com/docker-for-windows/install)

Sau khi chạy ứng dụng Docker đã cài đặt bạn sẽ có biểu tượng cá voi trong thanh menu của mình, với trạng thái “Docker is running” màu xanh.

### **2.1. Setting Docker**

Kết nối Docker CE trên Windows 10 với Ubuntu

* Mở cổng 2375 cho daemon

![](./images/setup3.png)

* Thiết lập biến môi trường trên Ubuntu: thêm biến DOCKER_HOST mọi lần chạy Bash.

```sh
echo "export DOCKER_HOST='tcp://0.0.0.0:2375'" >> ~/.bashrc
source ~/.bashrc
```

### **2.3. Install docker compose**

Cài đặt docker compose trên Ubuntu bằng lệnh

```sh
sudo apt install docker-compose
``` 

## **3. Install support tools**

### **3.1. Install Go**

```sh
wget https://dl.google.com/go/go1.10.3.linux-amd64.tar.gz
sudo tar -xvf go1.10.3.linux-amd64.tar.gz
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```

### **3.2. Install NodeJs**

Phiên bản Node.js 9.x chưa được hỗ trợ.

```sh
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
nvm install 8.9.4
```

```sh
sudo apt-get install build-essential
```

Kiểm tra phiên bản npm 5.6.0

```sh
npm --version 
```

## **4. Mount drive**

Ví dụ ổ sử dụng chung giữa Windows và Ubuntu là ổ E

### **4.1. Share drive**

Share ổ giữa Windows và Ubuntu, cho phép Ubuntu dùng ổ e của Windows

### **4.2. Mount drive**

```sh
sudo mkdir /e
sudo mount --bind /mnt/e /e
mkdir /e/blockchain && cd /e/blockchain
```

#

*Cách khác để bật tắt Hyper-V*

* Enable Hyper-V

```cmd
dism.exe /Online /Enable-Feature:Microsoft-Hyper-V /All
```

* Disable Hyper-V

```cmd
dism.exe /Online /Disable-Feature:Microsoft-Hyper-V-All
```