# 请求结构

### 1. 服务地址 <a href="#1.-.e6.9c.8d.e5.8a.a1.e5.9c.b0.e5.9d.80" id="1.-.e6.9c.8d.e5.8a.a1.e5.9c.b0.e5.9d.80"></a>

目前Zenlayer Cloud API 请求的服务域名为 **console.zenlayer.com。**

### 2. 通信协议 <a href="#2.-.e9.80.9a.e4.bf.a1.e5.8d.8f.e8.ae.ae" id="2.-.e9.80.9a.e4.bf.a1.e5.8d.8f.e8.ae.ae"></a>

Zenlayer Cloud API 的所有接口均通过 HTTPS 进行通信，提供高安全性的通信通道。

### 3. 请求方法 <a href="#3.-.e8.af.b7.e6.b1.82.e6.96.b9.e6.b3.95" id="3.-.e8.af.b7.e6.b1.82.e6.96.b9.e6.b3.95"></a>

支持的 HTTP 请求方法：**POST。**

POST 请求支持的 Content-Type 类型：**application/json**。 必须使用签名方法v2（ZC2-HMAC-SHA256）。

### 4. 字符编码 <a href="#4.-.e5.ad.97.e7.ac.a6.e7.bc.96.e7.a0.81" id="4.-.e5.ad.97.e7.ac.a6.e7.bc.96.e7.a0.81"></a>

均使用**`UTF-8`**编码。
