# RenewDdosIpAddress

## 1. 接口描述

调用本接口用于续费处在回收站的一个Ddos IP。

{% hint style="info" %}
#### 注意事项

* 只有在回收站且状态为 **RECYCLE** 的Ddos IP才能操作。
* 续费时请确保账户余额充足。可通过`DescribeAccountBalance`接口查询账户余额。
* Ddos IP的ddosIpChargeType为PREPAID时，接口调用成功后，需根据新订单号去支付费用。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称     | 必选 | 类型     | 描述                                                                                                 |
| -------- | -- | ------ | -------------------------------------------------------------------------------------------------- |
| ddosIpId | 是  | String | <p>一个Ddos IP ID。</p><p>可通过<code>DescribeDdosIpAddresses</code>接口返回值中的 <code>ddosIpId</code>获取。</p> |



## 3. 响应结果

| 参数名称        | 类型     | 描述                                                       |
| ----------- | ------ | -------------------------------------------------------- |
| requestId   | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| orderNumber | String | <p>订单编号。<br>当ddosIpChargeType为PREPAID时会返回。</p>           |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. 续费指定ID的Ddos IP

续费指定的Ddos IP。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: RenewDdosIpAddress
<Common Request Params>

Request：
{
    "ddosIpId": "ddosIpId1"
}

Response：
{
  "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
  "response": { 
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                        | 说明               |
| ------- | ------------------------------------------ | ---------------- |
| 403     | OPERATION\_DENIED\_DDOS\_IP\_NOT\_RECYCLED | 指定的Ddos IP不在回收站。 |
| 404     | INVALID\_DDOS\_IP\_NOT\_FOUND              | 指定的Ddos IP不存在。   |
