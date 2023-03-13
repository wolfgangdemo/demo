# CreateIpv6Block

## 1. 接口描述

调用本接口创建一个或多个Ipv6 Cidr Block。

#### 准备工作

* 查询库存：调用[`DescribeAvailableIpv6Resources`](describeavailableipv6resources.md)查看指定地区的资源供给情况。

{% hint style="info" %}
**注意事项**

* 每个Ipv6 Cidr Block包含500个可用的IP。
* 本接口为异步接口，当创建Cidr Block请求下发成功后会返回一个`ID`列表，此时创建Cidr Block操作并未立即完成。在此期间Cidr Block的状态将会处于`CREATING`，Cidr Block创建结果可以通过调用`DescribeCidrBlocks` 接口查询，如果Cidr Block状态由`CREATING`(创建中)变为`AVAILABLE`，则代表Cidr Block创建成功，`CREATE_FAILED`代表Cidr Block创建失败。创建过程中不可对Cidr Block进行任何操作。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称            | 必选 | 类型      | 描述                                                                         |
| --------------- | -- | ------- | -------------------------------------------------------------------------- |
| zoneId          | 是  | String  | Cidr Block所属的可用区 ID。                                                       |
| name            | 否  | String  | <p>Cidr Block的名称。</p><p>不得超过64个字符。</p>                                     |
| amount          | 否  | Integer | <p>购买的数量。</p><p>默认为1。</p>                                                  |
| resourceGroupId | 否  | String  | <p>Cidr Block所属的资源组ID。</p><p>如果指定的区域内存在可用的VLAN，则会忽略该参数自动使用与VLAN相同的资源组。</p> |



## 3. 响应结果

| 参数名称         | 类型              | 描述                                                       |
| ------------ | --------------- | -------------------------------------------------------- |
| requestId    | String          | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| cidrBlockIds | Array of String | Cidr Block ID列表。                                         |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 创建一个Ipv6 Cidr Block**

在区域**`ISB-B`**创建一个名称为**`example`**的Cidr Block，并且加入默认资源组。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: CreateIpv6Block
<Common Request Params>

Request:
{
  "zoneId": "ISB-B",
  "name": "example",
  "amount": 1
}

Response:
{
  "requestId": "T17BD4918-239C-4633-9F3A-9D2D5E0BA4E2",
  "response": {
    "requestId": "T17BD4918-239C-4633-9F3A-9D2D5E0BA4E2",
    "cidrBlockIds": [
      "cidrBlockId"
    ]
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                        | 说明        |
| ------- | ------------------------------------------ | --------- |
| 404     | INVALID\_ZONE\_NOT\_FOUND                  | 指定的区域不存在。 |
| 403     | RESOURCE\_INSUFFICIENT\_PRODUCT\_SOLD\_OUT | 指定的产品已售罄。 |
