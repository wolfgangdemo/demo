# TerminateCidrBlock

## 1. 接口描述

本接口用于退还一个Cidr Block。

{% hint style="info" %}
**注意事项**

* 不再使用的Cidr Block，可通过本接口主动退还。如果是后付费，退还的Cidr Block将停止计费。
* 本接口无法主动退还预付费订阅模式的Cidr Block，**订阅模式**的Cidr Block将会在订阅到期后自动退还。
* 无法退还关联了实例的Cidr Block，如需退还请先解绑所有实例。
* 退还后的Ipv4 Cidr Block将进入回收站，进入回收站后如无其他操作将在24小时后自动释放，也可以调用`ReleaseCidrBlocks`接口主动进行释放。Ipv6 Cidr Block调用本接口会直接释放，不会进入回收站。
* 已经在回收站中或者正在创建中的Cidr Block调用该接口无效。
* 创建失败并且状态为`CREATE_FAILED`的Cidr Block调用本接口会直接删除Cidr Block，对于预付费的Cidr Block会退还所有的支付金额。
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
**1. 退还一个Cidr Block**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: TerminateCidrBlock
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

| HTTP状态码 | 错误码                                        | 说明                       |
| ------- | ------------------------------------------ | ------------------------ |
| 403     | OPERATION\_DENIED\_CIDRBLOCK\_SUBSCRIPTION | 预付费订阅模式的Cidr Block不允许退还。 |
| 403     | OPERATION\_DENIED\_INSTANCE\_EXIST         | 存在绑定实例的Cidr Block不允许退还。  |
