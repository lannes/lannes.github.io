
## **1. Cập nhật ứng dụng**

### **1.1. Cập nhật Model** 

Mở file **org.example.mynetwork.cto** thay bằng nội dung sau

```js
/**
 * My commodity trading network
 */
namespace org.example.mynetwork

asset Commodity identified by tradingSymbol {
    o String tradingSymbol
    o String description
    o String mainExchange
    o Double quantity
    --> Trader owner
}

participant Trader identified by tradeId {
    o String tradeId
    o String firstName
    o String lastName
}

transaction Trade {
    --> Commodity commodity
    --> Trader newOwner
}

event TradeNotification {
    --> Commodity commodity
}

transaction RemoveHighQuantityCommodities {
}

event RemoveNotification {
    --> Commodity commodity
}
```

### **1.2. Cập nhật Logic**

Mở file **logic.js** thay bằng nội dung sau

```js
/**
 * Track the trade of a commodity from one trader to another
 * @param {org.example.mynetwork.Trade} trade - the trade to be processed
 * @transaction
 */
async function tradeCommodity(trade) {

    // set the new owner of the commodity
    trade.commodity.owner = trade.newOwner;
    let assetRegistry = await getAssetRegistry('org.example.mynetwork.Commodity');

    // emit a notification that a trade has occurred
    let tradeNotification = getFactory().newEvent('org.example.mynetwork', 'TradeNotification');
    tradeNotification.commodity = trade.commodity;
    emit(tradeNotification);

    // persist the state of the commodity
    await assetRegistry.update(trade.commodity);
}

/**
 * Remove all high volume commodities
 * @param {org.example.mynetwork.RemoveHighQuantityCommodities} remove - the remove to be processed
 * @transaction
 */
async function removeHighQuantityCommodities(remove) {

    let assetRegistry = await getAssetRegistry('org.example.mynetwork.Commodity');
    let results = await query('selectCommoditiesWithHighQuantity');

    for (let n = 0; n < results.length; n++) {
        let trade = results[n];

        // emit a notification that a trade was removed
        let removeNotification = getFactory().newEvent('org.example.mynetwork','RemoveNotification');
        removeNotification.commodity = trade;
        emit(removeNotification);
        await assetRegistry.remove(trade);
    }
}
```

### **1.3. Cập nhật permission**

Mở file **permissions.acl** thay bằng nội dung sau

```
/**
 * Access control rules for tutorial-network
 */
rule Default {
    description: "Allow all participants access to all resources"
    participant: "ANY"
    operation: ALL
    resource: "org.example.mynetwork.*"
    action: ALLOW
}

rule SystemACL {
  description:  "System ACL to permit all access"
  participant: "ANY"
  operation: ALL
  resource: "org.hyperledger.composer.system.**"
  action: ALLOW
}
```

### **1.4. Tạo file query**

Trong thư mục mynetwork tạo file **queries.qry** với nội dung

```
/** Sample queries for Commodity Trading business network
*/

query selectCommodities {
  description: "Select all commodities"
  statement:
      SELECT org.example.mynetwork.Commodity
}

query selectCommoditiesByExchange {
  description: "Select all commodities based on their main exchange"
  statement:
      SELECT org.example.mynetwork.Commodity
          WHERE (mainExchange == _$exchange)
}

query selectCommoditiesByOwner {
  description: "Select all commodities based on their owner"
  statement:
      SELECT org.example.mynetwork.Commodity
          WHERE (owner == _$owner)
}

query selectCommoditiesWithHighQuantity {
  description: "Select commodities based on quantity"
  statement:
      SELECT org.example.mynetwork.Commodity
          WHERE (quantity > 60)
}
```

## **2. Tạo lại file business network archive**

### **2.1. Nâng phiên bản**

Mở file **package.json** nâng phiên bản 0.0.1 thành 0.0.2

### **2.2. Tạo lại file BNA**

```sh
composer archive create -t dir -n .
```

## **3. Deploy Business Network**

### **3.1. Cập nhật business network**

```sh
composer network install --card PeerAdmin@hlfv1 --archiveFile mynetwork@0.0.2.bna
```

### **3.2. Nâng cấp phiên bản**

```sh
composer network upgrade -c PeerAdmin@hlfv1 -n mynetwork -V 0.0.2
```

Sau bước này kiểm tra bằng `docker ps` ta thấy có thêm container 0.0.2

### **3.3. Kiểm tra phiên bản đang hoạt động**

```sh
composer network ping -c admin@mynetwork | grep Business
```

Kết quả chạy

```
	Business network version: 0.0.2
```

## **4. Sinh lại REST API**

Tại thư mục **mynetwork** chạy lệnh

```sh
composer-rest-server
```

```
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
Registering named query: selectCommodities
Registering named query: selectCommoditiesByExchange
Registering named query: selectCommoditiesByOwner
Registering named query: selectCommoditiesWithHighQuantity
Generated schemas for all types in business network definition
Adding schemas for all types to Loopback ...
Added schemas for all types to Loopback
Web server listening at: http://localhost:3000
Browse your REST API at http://localhost:3000/explorer
```

## **5. Test API**

Mở trình duyệt và nhập link: http://localhost:3000/explorer 

### **5.1. Tạo 3 Trader**

Vào mục **Trader** chọn phương thức **POST** của Trader

```
{
  "$class": "org.example.mynetwork.Trader",
  "tradeId": "TRADER1",
  "firstName": "Jenny",
  "lastName": "Jones"
}

{
  "$class": "org.example.mynetwork.Trader",
  "tradeId": "TRADER2",
  "firstName": "Jack",
  "lastName": "Sock"
}

{
  "$class": "org.example.mynetwork.Trader",
  "tradeId": "TRADER3",
  "firstName": "Rainer",
  "lastName": "Valens"
}
```

### **5.2. Tạo 2 tài sản cho TRADER1 và TRADER2**

Vào mục **Commodity** chọn phương thức **POST** của Commodity

```
{
  "$class": "org.example.mynetwork.Commodity",
  "tradingSymbol": "EMA",
  "description": "Corn",
  "mainExchange": "EURONEXT",
  "quantity": 10,
  "owner": "resource:org.example.mynetwork.Trader#TRADER1"
}

{
  "$class": "org.example.mynetwork.Commodity",
  "tradingSymbol": "CC",
  "description": "Cocoa",
  "mainExchange": "ICE",
  "quantity": 80,
  "owner": "resource:org.example.mynetwork.Trader#TRADER2"
}
```

### **5.3. Truy vấn dữ liệu**

#### **5.3.1. Truy vấn không tham số**

Tại mục _Query_ chọn phương thức _GET_ của _selectCommodities_

`Try it out` cho kết quả

```
[
  {
    "$class": "org.example.mynetwork.Commodity",
    "tradingSymbol": "CC",
    "description": "Cocoa",
    "mainExchange": "ICE",
    "quantity": 80,
    "owner": "resource:org.example.mynetwork.Trader#TRADER2"
  },
  {
    "$class": "org.example.mynetwork.Commodity",
    "tradingSymbol": "EMA",
    "description": "Corn",
    "mainExchange": "EURONEXT",
    "quantity": 10,
    "owner": "resource:org.example.mynetwork.Trader#TRADER1"
  }
]
```

#### **5.3.2. Truy vấn có tham số** 

Tại mục _Query_ chọn _GET_ của _selectCommoditiesByExchange_, nhập _Exchange_ là _EURONEXT_

`Try it out` cho kết quả

```
[
  {
    "$class": "org.example.mynetwork.Commodity",
    "tradingSymbol": "EMA",
    "description": "Corn",
    "mainExchange": "EURONEXT",
    "quantity": 10,
    "owner": "resource:org.example.mynetwork.Trader#TRADER1"
  }
]
```

#### **5.3.3. Cập nhật dữ liệu**

Kiểm tra trước khi cập nhật: Tại mục _Query_ chọn _GET_ của _selectCommoditiesWithHighQuantity_

Kết quả

```
[
  {
    "$class": "org.example.mynetwork.Commodity",
    "tradingSymbol": "CC",
    "description": "Cocoa",
    "mainExchange": "ICE",
    "quantity": 80,
    "owner": "resource:org.example.mynetwork.Trader#TRADER2"
  }
]
```

Tại mục _RemoveHighQuantityCommodities_, chọn _POST_ của _RemoveHighQuantityCommodities_

Kết quả

```
{
  "$class": "org.example.mynetwork.RemoveHighQuantityCommodities",
  "transactionId": "04f48473f1f86e293da59c2c9c259dfc5b5fefb028b68c2a8fcdeb4b9bbfbc81"
}
```

Kiểm tra lại

Kết quả

```
[]
```

























