# **Cài đặt trên Mac**

# **MỤC LỤC**
* [1. Install nvm](#1-Install-nvm)
* [2. Install NodeJS](#2-Install-NodeJS)
* [3. Install Docker](#3-Install-Docker)
* [4. Install VSCode](#4-Install-VSCode)

## **1. Install nvm**

```sh
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
```

## **2. Install NodeJS**

```sh
nvm install 8.9.4
```

Kiểm tra Node đã được cài đặt:

```
node --version
```

## **3. Install Docker**

Làm theo hướng dẫn ở đây để cài đặt Docker cho Mac (bản ổn định): https://docs.docker.com/docker-for-mac/install/

Sau khi chạy ứng dụng Docker đã cài đặt bạn sẽ có biểu tượng cá voi trong thanh menu của mình, với trạng thái “Docker is running” màu xanh.

## **4. Install VSCode**

Truy cập trang: https://code.visualstudio.com

Nhấn nút “Download for Mac” và copy ứng dụng đã tải vào thư mục Applications.

## **4.1. Cài Hyperledger Composer Extension cho VSCode**

Chạy VSCode và nhấn nút “Extensions” trên toolbar dọc bên trái.

Gõ composer trong search bar và sau đó nhấn nút Install chuyển đến Hyperleger Composer extension. Sau khi cài đặt hoàn tất bạn cần nhấn nút Reload để kích hoạt extension.


