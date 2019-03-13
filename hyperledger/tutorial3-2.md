# **Lịch sử giao dịch**

## **1.1. Cập nhật Query**

Mở file queries.qry bổ sung nội dung sau

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

Mở file **permissions.acl** bổ sung nội dung sau

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

Mở file **package.json** nâng phiên bản 0.0.2 thành 0.0.3

```sh
composer archive create -t dir -n .

composer network install --card PeerAdmin@hlfv1 --archiveFile mynetwork@0.0.3.bna

Nếu Business Network 0.0.2 đang chạy

composer network upgrade -c PeerAdmin@hlfv1 -n mynetwork -V 0.0.3

Nếu Business Network 0.0.2 không chạy

composer network start --networkName mynetwork --networkVersion 0.0.3 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file networkadmin.card

composer-rest-server
```

