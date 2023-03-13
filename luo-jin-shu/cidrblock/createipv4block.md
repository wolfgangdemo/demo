# CreateIpv4Block

## 1. 接口描述

调用本接口创建一个或多个Ipv4 Cidr Block。

#### 准备工作

* 查询可用资源：调用[`DescribeAvailableIpv4Resources`](describeavailableipv4resources.md)查看指定地区的资源供给情况。
* 成本估算：了解Cidr Block的的计费方式。更多详情，请参见计费概述。

{% hint style="info" %}
**注意事项**

* 预付费Cidr Block的购买会预先扣除本次购买所需金额，后付费Cidr Block购买时需要确保账户账号状态正常。
* 调用本接口创建Cidr Block，支持代金券自动抵扣，详情请参考代金券选用规则。
* 本接口为异步接口，当创建Cidr Block请求下发成功后会返回一个`ID`列表，此时创建Cidr Block操作并未立即完成。在此期间Cidr Block的状态将会处于`CREATING`，Cidr Block创建结果可以通过调用`DescribeCidrBlocks` 接口查询，如果Cidr Block状态由`CREATING`(创建中)变为`AVAILABLE`，则代表Cidr Block创建成功，`CREATE_FAILED`代表Cidr Block创建失败。创建过程中不可对Cidr Block进行任何操作。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称            | 必选 | 类型                                                 | 描述                                                                                             |
| --------------- | -- | -------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| zoneId          | 是  | String                                             | Cidr Block所属的可用区ID。                                                                            |
| name            | 否  | String                                             | <p>Cidr Block的名称。</p><p>不得超过64个字符。</p>                                                         |
| chargeType      | 是  | String                                             | <p>付费类型。</p><p>PREPAID：预付费，即包年包月</p><p>POSTPAID：后付费。</p>                                       |
| chargePrepaid   | 否  | [ChargePrepaid](../datastructure.md#chargeprepaid) | <p>预付费模式。</p><p>即包年包月相关参数设置。通过该参数可以指定包年包月实例的购买时长等属性。若指定实例的付费模式为预付费则该参数必传。</p>                  |
| netmask         | 是  | Integer                                            | <p>购买的掩码。</p><p>取值范围1~32。</p><p>可以从<code>DescribeAvailableIpv4Resource</code>接口中获取可用的掩码列表。</p> |
| amount          | 否  | Integer                                            | <p>购买的数量。</p><p>默认为1。</p>                                                                      |
| resourceGroupId | 否  | String                                             | <p>Cidr Block所属的资源组ID。</p><p>如果指定的区域内存在可用的VLAN，则会忽略该参数自动使用与VLAN相同的资源组。</p>                     |



## 3. 响应结果

| 参数名称         | 类型     | 描述                                                       |
| ------------ | ------ | -------------------------------------------------------- |
| requestId    | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| orderNumber  | String | 订单编号。                                                    |
| cidrBlockIds | String | Cidr Block ID列表。                                         |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 创建一个后付费的Ipv4 Cidr Block**

在区域**`IST-B`**创建一个掩码为**`29`**，名称为**`example1`**的Ipv4 Cidr Block，并且加入默认资源组。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: CreateIpv4Block
<Common Request Params>

Request:
{
  "zoneId": "IST-B",
  "name": "example1",
  "chargeType": "POSTPAID",
  "netmask": 29
}

Response:
{
  "requestId": "T135376EE-7090-4773-B81E-7FB38358B656",
  "response": {
    "requestId": "T135376EE-7090-4773-B81E-7FB38358B656",
    "orderNumber": "orderNum",
    "cidrBlockIds": [
      "cidrBlockId"
    ]
  }
}
```

****

**2. 创建一个预付费的Ipv4 Cidr Block**

在区域**`AMS-D`**创建一个掩码为**`29`**，名称为**`example2`**的Ipv4 Cidr Block，并且加入默认资源组。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: CreateIpv4Block
<Common Request Params>

Request:
{
  "zoneId": "AMS-D",
  "name": "example2",
  "chargeType": "PREPAID",
  "chargePrepaid": {
    "period": 1
  },
  "netmask": 29,
  "amount": 1
}

Response:
{
  "requestId": "T3B843750-5B98-421B-9D74-D3234C664760",
  "response": {
    "requestId": "T3B843750-5B98-421B-9D74-D3234C664760",
    "orderNumber": "orderNum",
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

| HTTP状态码 | 错误码                                        | 说明         |
| ------- | ------------------------------------------ | ---------- |
| 404     | INVALID\_ZONE\_NOT\_FOUND                  | 指定的区域不存在。  |
| 403     | OPERATION\_DENIED\_NETMASK\_OUT\_OF\_STOCK | 指定的掩码库存不足。 |
| 403     | RESOURCE\_INSUFFICIENT\_PRODUCT\_SOLD\_OUT | 指定的产品已售罄。  |
