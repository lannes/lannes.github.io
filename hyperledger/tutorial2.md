

# **Cài đặt môi trường và ứng dụng**

# **MỤC LỤC**
* [1. Install Hyperledger Fabric](#1-Install-Hyperledger-Fabric)
   * [1.1. Download scripts](#11-Download-scripts)
   * [1.2. Install Hyperledger Fabric](#12-Install-Hyperledger-Fabric)
* [2. Install support tools](#2-Install-support-tools)
* [3. Start Fabric](#3-Start-Fabric)
* [4. Deploy Business Network](#4-Deploy-Business-Network)
   * [4.1. Create a Business Network](#41-Create-a-Business-Network)
   * [4.2. Create a Business Network Definition Archive](#42-Create-a-Business-Network-Definition-Archive)
   * [4.3. Install a Business Network](#43-Install-a-Business-Network)
   * [4.4. Start a Business Network](#44-Start-a-Business-Network)
   * [4.5. Import a Business Network Card](#45-Import-a-Business-Network-Card)
* [5. Create REST server](#5-Create-REST-server)
* [6. Create a application](#6-Create-a-application)
* [7. Reference](#7-Reference)

## **1. Install Hyperledger Fabric**

### **1.1. Download scripts**

```sh
# Tạo và di chuyển đến thư mục fabric-dev-servers
mkdir ~/fabric-dev-servers && cd ~/fabric-dev-servers

# Tải script
curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.tar.gz

# Giải nén
tar -xvf fabric-dev-servers.tar.gz
```

### **1.2. Install Hyperledger Fabric**

Chọn phiên bản 1.1

```sh
# Chỉ định phiên bản FABRIC
export FABRIC_VERSION=hlfv11

# Chạy script download image
./downloadFabric.sh
```

Kiểm tra các images đã tải về

```sh
docker images

REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
hyperledger/fabric-ca        x86_64-1.1.0        72617b4fa9b4        12 months ago       299MB
hyperledger/fabric-orderer   x86_64-1.1.0        ce0c810df36a        12 months ago       180MB
hyperledger/fabric-peer      x86_64-1.1.0        b023f9be0771        12 months ago       187MB
hyperledger/fabric-ccenv     x86_64-1.1.0        c8b4909d8d46        12 months ago       1.39GB
hyperledger/fabric-couchdb   x86_64-0.4.6        7e73c828fc5b        12 months ago       1.56GB
```

## **2. Install support tools**

```sh
# 1. Công cụ sinh Business Network
npm install -g yo@2.0.5

npm install -g generator-hyperledger-composer@0.19

# 2. Công cụ triển khai Business Network
npm install -g composer-cli@0.19

# 3. Công cụ sinh server API
npm install -g composer-rest-server@0.19
```

## **3. Start Fabric**

Khi bắt đầu một bản thực thi, cần chạy script khởi động, tạo ra một thẻ PeerAdmin:

```sh
./startFabric.sh
./createPeerAdminCard.sh
```

Kết quả chạy

```sh
Development only script for Hyperledger Fabric control
Running 'startFabric.sh'
FABRIC_VERSION is set to 'hlfv11'
FABRIC_START_TIMEOUT is unset, assuming 15 (seconds)
Removing network composer_default
Creating network "composer_default" with the default driver
Creating orderer.example.com ... done
Creating ca.org1.example.com ... done
Creating couchdb             ... done
Creating peer0.org1.example.com ... done
sleeping for 15 seconds to wait for fabric to complete start up
```

## **4. Deploy Business Networks**

### **4.1. Create a Business Network**

```sh
yo hyperledger-composer
```

Chọn các thông số như sau

```sh
? Please select the type of project: Business Network
You can run this generator using: 'yo hyperledger-composer:businessnetwork'
Welcome to the business network generator
? Business network name: mynetwork
? Description: This is my test network
? Author name:  dongnh
? Author email: dongnh@vtc.vn
? License: Apache-2.0
? Namespace: org.example.mynetwork
? Do you want to generate an empty template network? No: generate a populated sample network
```

Thư mục mynetwork được tạo ra chứa các file của dự án

```sh
create package.json
create README.md
create models/org.example.mynetwork.cto
create permissions.acl
create .eslintrc.yml
create features/sample.feature
create features/support/index.js
create test/logic.js
create lib/logic.js
```

### **4.2. Create a Business Network Definition Archive** 

Chạy lệnh
```sh
# Chuyển đến thư mục mynetwork
cd mynetwork

# Tạo Business Network
composer archive create -t dir -n .
```

Kết quả chạy

```sh
Creating Business Network Archive


Looking for package.json of Business Network Definition
	Input directory: /Users/huydong/fabric-dev-servers/mynetwork

Found:
	Description: This is my test network
	Name: mynetwork
	Identifier: mynetwork@0.0.1

Written Business Network Definition Archive file to 
	Output file: mynetwork@0.0.1.bna

Command succeeded
```

### **4.3. Install a Business Network**

```sh
composer network install --card PeerAdmin@hlfv1 --archiveFile mynetwork@0.0.1.bna
```

Kết quả chạy

```sh
✔ Installing business network. This may take a minute...
Successfully installed business network mynetwork, version 0.0.1

Command succeeded
```

* Nếu chạy bị lỗi `Error trying install business network. Error: No valid responses from any peers.` hoặc lỗi `Error: Error trying install business network. Error: The business network is already installed on all the peers` thì chạy lại lệnh `./startFabric.sh`

### **4.4. Start a Business Network**

Chạy Business Network với thông số ặc định của tài khoản admin

networkAdmin: **admin**

networkAdminEnrollSecret: **adminpw**

```sh
composer network start --networkName mynetwork --networkVersion 0.0.1 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file networkadmin.card
```

Kết quả chạy

```sh
Starting business network mynetwork at version 0.0.1

Processing these Network Admins: 
	userName: admin

✔ Starting business network definition. This may take a minute...
Successfully created business network card:
	Filename: networkadmin.card

Command succeeded
```

Kiểm tra bằng lệnh `docker ps` để thấy các container đang chạy trên docker.

Lệnh trên đồng thời tạo ra file **networkadmin.card**  là 1 file business network card chứa tất cả các thông tin cần thiết để kết nối  đến blockchain business network. Thẻ này chứa các định danh cho mỗi đối tượng tham gia. Có thể có nhiều thẻ cho một Business Network, trong đó các thẻ thuộc về nhiều đối tượng tham gia.

```js
{
   "name": "hlfv1",
   "x-type": "hlfv1",
   "x-commitTimeout": 300,
   "version": "1.0.0",
   "client": {
      "organization": "Org1",
      "connection": {
         "timeout": {
            "peer": {
               "endorser": "300",
               "eventHub": "300",
               "eventReg": "300"
            },
            "orderer":"300"
         }
      }
   },
   "channels": {
      "composerchannel": {
         "orderers": [
            "orderer.example.com"
         ],
         "peers": {
            "peer0.org1.example.com": {
            }
         }
      }
   },
   "organizations": {
      "Org1": {
         "mspid": "Org1MSP",
         "peers": [
            "peer0.org1.example.com"
         ],
         "certificateAuthorities": [
            "ca.org1.example.com"
         ]
      }
   },
   "orderers": {
      "orderer.example.com": {
         "url": "grpc://localhost:7050"
      }
   },
   "peers": {
      "peer0.org1.example.com": {
         "url": "grpc://localhost:7051"
      }
   },
   "certificateAuthorities": {
      "ca.org1.example.com": {
         "url": "http://localhost:7054",
         "caName": "ca.org1.example.com"
      }
   }
}
```

### **4.5. Import a Business Network Card**

```sh
composer card import --file networkadmin.card
```

Kết quả chạy

```sh
Successfully imported business network card
	Card file: networkadmin.card
	Card name: admin@mynetwork

Command succeeded
```

Kiểm tra kết nối đến network

```
composer network ping --card admin@mynetwork
```

Kết quả chạy

```sh
The connection to the network was successfully tested: mynetwork
	Business network version: 0.0.1
	Composer runtime version: 0.19.20
	participant: org.hyperledger.composer.system.NetworkAdmin#admin
	identity: org.hyperledger.composer.system.Identity#150bca7ca1262d827f9aff264be1b95af46c8439a7d8be6a5d5fa0bc37832aef

Command succeeded
```

## **5. Create REST server**

```sh
composer-rest-server
```

Kết quả chạy

```sh
? Enter the name of the business network card to use: admin@mynetwork
? Specify if you want namespaces in the generated REST API: never use namespaces
? Specify if you want to use an API key to secure the REST API: No
? Specify if you want to enable authentication for the REST API using Passport: No
? Specify if you want to enable the explorer test interface: Yes
? Specify a key if you want to enable dynamic logging: 
? Specify if you want to enable event publication over WebSockets: Yes
? Specify if you want to enable TLS security for the REST API: No

To restart the REST server using the same options, issue the following command:
   composer-rest-server -c admin@mynetwork -n never -u true -w true

Discovering types from business network definition ...
Discovering the Returning Transactions..
Discovered types from business network definition
Generating schemas for all types in business network definition ...
Generated schemas for all types in business network definition
Adding schemas for all types to Loopback ...
Added schemas for all types to Loopback
Web server listening at: http://localhost:3000
Browse your REST API at http://localhost:3000/explorer
```

Kiểm tra API tại địa chỉ http://localhost:3000/explorer

## **6. Create a application**

```sh
yo hyperledger-composer:angular
```

```sh
Welcome to the Hyperledger Composer Angular project generator
? Do you want to connect to a running Business Network? Yes
? Project name: mynetwork-app
? Description: Mynetwork Angular Project
? Author name: dongnh
? Author email: dongnh@vtc.vn
? License: Apache-2.0
? Name of the Business Network card: admin@mynetwork
? Do you want to generate a new REST API or connect to an existing REST API?  Connect to an existing REST API
? REST server address: http://localhost
? REST server port: 3000
? Should namespaces be used in the generated REST API? Namespaces are not used
Created application!
Completed generation process
...
```

Chạy ứng dụng

```sh
npm start
```

Ứng dụng sau khi biên dịch thành công chạy tại http://localhost:4200/

## **7. Reference**

[Hyperledger Composer v0.19](https://hyperledger.github.io/composer/v0.19/index.html)