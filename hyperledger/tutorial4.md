
# **Chạy lại Business Network**

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
