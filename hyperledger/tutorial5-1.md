


## **1. Xác thực cho server REST**

Server REST có thể được cấu hình để xác thực ứng dụng client. Khi bật tuỳ chọn này client phải xác thực với server trước khi được phép gọi API REST.

### **1.1. Chọn kiểu xác thực**

Thư viện Passport cung cấp nhiều giải pháp xác thực, giả sử ta lựa chọn xác thực qua GitHub.

```sh
npm install -g passport-github
```

### **1.2. Cấu hình**

Để xác thực qua GitHub cần tạo ứng dụng OAuth trên GitHub.

1. Đăng nhập [GitHub](https://github.com/) với tài khoản
2. Click vào ảnh profile ở trên cùng bên phải, chọn **Settings** từ menu 
3. Click vào **OAuth applications** dưới **Developer settings** bên trái.
4. Click vào **Register a new application**
5. Thiết lập các thông số:
    * Application name: Composer
    * Homepage: http://localhost:3000/
    * Application description: OAuth application for Composer
    * Authorization callback URL: http://localhost:3000/auth/github/callback
6. Click vào **Register application**
7. Lưu ý các giá trị **Client ID** và **Client Secret**.

```sh
export COMPOSER_PROVIDERS='{
  "github": {
    "provider": "github",
    "module": "passport-github",
    "clientID": "REPLACE_WITH_CLIENT_ID",
    "clientSecret": "REPLACE_WITH_CLIENT_SECRET",
    "authPath": "/auth/github",
    "callbackURL": "/auth/github/callback",
    "successRedirect": "/",
    "failureRedirect": "/"
  }
}'
```

### **1.3. Bật chế độ xác thực**

```sh
composer-rest-server -c admin@mynetwork -a true
```

### **1.4. Xác thực qua web browser**

Truy cập link để xác thực qua [GitHub](http://localhost:3000/auth/github)

Sau khi xác thực thành công, sẽ chuyển về link callback [http://localhost:3000/explorer/](http://localhost:3000/explorer/)

### **1.5. Xác thực qua HTTP hoặc REST client**

Show access token từ link callback [http://localhost:3000/explorer/](http://localhost:3000/explorer/)

Chỉ định access token trong chuỗi truy vấn (?access_token=xxxxx) hoặc thêm vào header (X-Access-Token: xxxxx)

```sh
curl -v http://localhost:3000/api/system/ping?access_token=xxxxx
```

```sh
curl -v -H 'X-Access-Token: xxxxx' http://localhost:3000/api/system/ping
```
