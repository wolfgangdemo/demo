# AllocateEipAddresses

## 1. 接口描述

调用本接口用于创建一个或多个EIP。

#### 准备工作

* 查询区域可购买的EIP：调用`DescribeEipAvailableResources`查看指定地区的资源供给情况。
* 成本估算：了解EIP的的计费方式。更多详情，请参见计费概述。

{% hint style="info" %}
**注意事项**

* 预付费EIP的购买会预先扣除本次EIP购买所需金额，后付费EIP购买时需要确保账户账号状态正常。
* 调用本接口创建EIP，支持代金券自动抵扣，详情请参考代金券选用规则。
* 本接口为异步接口，当创建EIP请求下发成功后会返回一个`ID`列表，此时创建EIP操作并未立即完成。在此期间EIP的状态将会处于`CREATING`，EIP创建结果可以通过调用`DescribeEipAddresses` 接口查询，如果EIP状态由`CREATING`(创建中)变为`AVAILABLE`，则代表EIP创建成功，`CREATE_FAILED`代表EIP创建失败。创建过程中不可对EIP进行任何操作。
* 单次最多能创建100个EIP。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称             | 必选 | 类型                                                 | 描述                                                                                       |
| ---------------- | -- | -------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| zoneId           | 是  | String                                             | EIP所属的可用区ID。                                                                             |
| eipChargeType    | 是  | String                                             | <p>付费类型。</p><p>PREPAID：预付费，即包年包月。</p><p>POSTPAID：后付费。</p>                                |
| eipChargePrepaid | 否  | [ChargePrepaid](../datastructure.md#chargeprepaid) | <p>预付费模式。<br>即包年包月相关参数设置。</p><p>通过该参数可以指定包年包月实例的购买时长等属性。</p><p>若指定实例的付费模式为预付费则该参数必传。</p> |
| amount           | 否  | Integer                                            | <p>指定创建EIP的数量。</p><p>范围为 1-100。</p><p>默认值：1。</p>                                         |
| resourceGroupId  | 否  | String                                             | <p>资源组ID。</p><p>如果不指定，则会放入默认资源组。如果用户没有默认资源组权限， 则请求将会失败。</p>                              |

## 3. 响应结果

| 参数名称        | 类型              | 描述                                                                                                                                                                                                             |
| ----------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| eipIdSet    | Array of String | <p>EIP 的ID列表。<br>当通过本接口来创建EIP时会返回该参数，表示一个或多个EIP ID。返回EIP ID列表并不代表EIP创建成功，可根据 <code>DescribeEipAddresses</code> 接口查询对应EIP ID的状态来判断创建是否完成；如果EIP状态由<code>CREATING</code>(创建中)变为<code>AVAILABLE</code>，则为创建成功。</p> |
| orderNumber | String          | <p>订单编号。</p><p>当eipChargeType为PREPAID时会返回。</p>                                                                                                                                                                 |
| requestId   | String          | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p>                                                                                                                                                       |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 用最简单的参数创建一个后付费的EIP**

创建一个SEL-A区域后付费的EIP。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: AllocateEipAddresses
<Common Request Params>

Request：
{
    "eipChargeType": "POSTPAID",
    "zoneId": "SEL-A"
}

Response：
{
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
    "response": {
        "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
        "eipIdSet": ["eipId1"],
        "orderNumber" : ""
    }
}
```

**2. 创建2个预付费的EIP**

创建2个SEL-A区域1个月预付费EIP。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: AllocateEipAddresses
<Common Request Params>

Request：
{
    "eipChargeType": "PREPAID",
    "zoneId": "SEL-A",
    "amount": 2,
    "eipChargePrepaid": {
        "period": 1
    }
}

Response：
{
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
    "response": {
        "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
        "eipIdSet": ["eipId1","eipId2"],
        "orderNumber" : "orderNumber1"
    }    
}
```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。

## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                | 说明               |
| ------- | ---------------------------------- | ---------------- |
| 404     | INVALID\_ZONE\_NOT\_FOUND          | 指定的可用区不存在。       |
| 400     | INVALID\_EIP\_TYPE\_ZONE\_NO\_SELL | 指定EIP在指定的可用区未售卖。 |
| 400     | MISSING\_PARAMETER                 | 指的参数为空。          |
