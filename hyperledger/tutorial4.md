
# **Một số vấn đề trong thực hành**

## **Chạy lại Business Network**

Sau khi đã cài đặt đầy đủ, nếu chúng ta đã dừng các container bằng lệnh `./stopFabric.sh` hoặc khởi động lại Docker thì có thể chạy lại Business Network như sau

```sh
# 1. Khởi động Fabric

# Chuyển đến thư mục lưu các script fabric

cd fabric-dev-servers

export FABRIC_VERSION=hlfv11
./startFabric.sh

# 2. Cài đặt Business Network

# Chyển đến thư mục dự án mynetwork

cd mynetwork

composer network install --card PeerAdmin@hlfv1 --archiveFile mynetwork@0.0.3.bna

# 3. Khởi động Business Network**

composer network start --networkName mynetwork --networkVersion 0.0.3 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file networkadmin.card

# 4. Chạy REST Server

composer-rest-server -c admin@mynetwork -n never -u true -w true
```

## **Xoá phiên bản cũ**

Các phiên bản khác nhau khi được triển khai sẽ tạo ra các images khác nhau và chiếm 1 lượng ổ cứng không nhỏ

```sh
docker images -a
REPOSITORY                                                                                                    TAG                 IMAGE ID            CREATED             SIZE
<none>                                                                                                        <none>              ca867ae615a5        4 days ago          1.44GB
dev-peer0.org1.example.com-mynetwork-0.0.3-24a51367fce019098f3fbe266185954da9fd792747f83aab9f97ff9a4b97b5c1   latest              f71be1d92a77        4 days ago          1.44GB
<none>                                                                                                        <none>              63788b597b51        4 days ago          1.44GB
<none>                                                                                                        <none>              f6ec4b6052b3        4 days ago          1.44GB
dev-peer0.org1.example.com-mynetwork-0.0.2-bec90581df0db7a8089269cf62204620431168911c146e2018d2186ca16ec0c6   latest              7fafed2e20de        6 days ago          1.44GB
<none>                                                                                                        <none>              a93fd387495c        6 days ago          1.44GB
<none>                                                                                                        <none>              7f63a786c2a1        6 days ago          1.44GB
dev-peer0.org1.example.com-mynetwork-0.0.1-5102b31c4c64a2c7168becb06b80aedd494906f6e3c64b6a47492c1257b55507   latest              278007ebb461        6 days ago          1.44GB
<none>                                                                                                        <none>              a2c2af52e580        6 days ago          1.44GB
<none>                                                                                                        <none>              edbdf113da73        6 days ago          1.44GB
hyperledger/fabric-ca                                                                                         x86_64-1.1.0        72617b4fa9b4        12 months ago       299MB
hyperledger/fabric-orderer                                                                                    x86_64-1.1.0        ce0c810df36a        12 months ago       180MB
hyperledger/fabric-peer                                                                                       x86_64-1.1.0        b023f9be0771        12 months ago       187MB
hyperledger/fabric-ccenv                                                                                      x86_64-1.1.0        c8b4909d8d46        12 months ago       1.39GB
hyperledger/fabric-baseimage                                                                                  x86_64-0.4.6        dbe6787b5747        13 months ago       1.37GB
hyperledger/fabric-couchdb                                                                                    x86_64-0.4.6        7e73c828fc5b        13 months ago       1.56GB
```

Do đó ta có thể xoá các phiên bản không sử dụng theo IMAGE ID để giải phóng dung lượng

```sh
# Xoá phiên bản 0.0.1
docker rmi -f 278007ebb461

# Xoá phiên bản 0.0.2
docker rmi -f 7fafed2e20de
```

