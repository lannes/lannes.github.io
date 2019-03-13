# **Lịch sử giao dịch**

## **1.1. Cập nhật Query**

Tại thư mục ứng dụng **mynetwork** mở file **queries.qry** bổ sung nội dung sau

```sql
query showCommodityAllHistoricans {
  description: "Select commodity all historican"
  statement:
      SELECT org.hyperledger.composer.system.HistorianRecord FROM HistorianRegistry
          WHERE (transactionType == 'AddAsset' OR transactionType == 'UpdateAsset' OR transactionType == 'RemoveAsset')
}

query findCommmodityHistoriansWithTime {
  description: "Find commodity historians after a specified time"
  statement:
    SELECT org.hyperledger.composer.system.HistorianRecord FROM
        HistorianRegistry WHERE (transactionTimestamp > _$justnow)
}
```

## **1.2. Cập nhật Permission** 

Tại thư mục ứng dụng **mynetwork** mở file **permissions.acl** bổ sung nội dung sau

```
rule historianAccess {
  description: "Only allow members to read historian records referencing transactions they submitted."
  participant(p): "org.example.mynetwork.*"
  operation: READ
  resource(r): "org.hyperledger.composer.system.HistorianRecord"
  condition: (r.participantInvoking.getIdentifier() == p.getIdentifier())
  action: ALLOW
}
```

## **1.3. Nâng phiên bản**

Tại thư mục ứng dụng **mynetwork** mở file **package.json** nâng phiên bản *0.0.2* thành *0.0.3*

```sh
# 1. Tạo lại file BNA
composer archive create -t dir -n .

# 2. Cài đặt file BNA
composer network install --card PeerAdmin@hlfv1 --archiveFile mynetwork@0.0.3.bna

# 3. Chạy Business Network

# Nếu Business Network 0.0.2 đang chạy
composer network upgrade -c PeerAdmin@hlfv1 -n mynetwork -V 0.0.3

# Nếu Business Network 0.0.2 không chạy
composer network start --networkName mynetwork --networkVersion 0.0.3 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file networkadmin.card

# 4. Sinh REST Server
composer-rest-server
```

*Nhập các thông số cho REST Server như sau*

* Enter the name of the business network card to use: **admin@mynetwork**

* Specify if you want namespaces in the generated REST API: **never use namespaces**

* Specify if you want to use an API key to secure the REST API: **No**

* Specify if you want to enable authentication for the REST API using Passport: **No**

* Specify if you want to enable the explorer test interface: **Yes**
  
* Specify a key if you want to enable dynamic logging: 
  
* Specify if you want to enable event publication over WebSockets: **Yes**
  
* Specify if you want to enable TLS security for the REST API: **No**


