# RenewCidrBlock

## 1. 接口描述

本接口用于续费一个Cidr Block。

{% hint style="info" %}
**注意事项**

* 续费时请确保账户余额充足。可通过`DescribeAccountBalance`接口查询账户余额。
* Ipv6的Cidr Block不可使用该接口。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称        | 必选 | 类型     | 描述                                                                                                   |
| ----------- | -- | ------ | ---------------------------------------------------------------------------------------------------- |
| cidrBlockId | 是  | String | <p>待操作的Cidr Block ID。</p><p>可通过<code>DescribeCidrBlocks</code>接口返回值中的<code>cidrBlockId</code>获取。</p> |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 续费一个Ipv4的Cidr Block**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: RenewCidrBlock
<Common Request Params>

Request:
{
  "cidrBlockId": "cidrBlockId"
}

Response:
{
  "requestId": "TC9E90021-5016-455C-B2F4-9D640EF63176",
  "response": {
    "requestId": "TC9E90021-5016-455C-B2F4-9D640EF63176"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                                | 说明                  |
| ------- | -------------------------------------------------- | ------------------- |
| 403     | OPERATION\_DENIED\_CIDRBLOCK\_TYPE\_NOT\_SUPPORTED | 该Cidr Block类型不支持续费。 |
