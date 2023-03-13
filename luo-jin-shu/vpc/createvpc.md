---
description: CreateVpc
---

# CreateVpc

## 1. 接口描述

本接口用于创建一个私有网络VPC。

#### 准备工作

* 在创建VPC之前，你可以调用`DescribeVpcAvailableRegions`进行查看哪些节点支持VPC的创建。

{% hint style="info" %}
**注意事项**

* 同一个VPC节点能创建的VPC资源个数也是有限制的，详见VPC使用限制，如果需要申请更多资源，请提交Support申请。
* 本接口为异步接口，当创建VPC请求下发成功后会返回一个VPC`ID`列表，此时创建VPC操作并未立即完成。在此期间VPC的状态将会处于`CREATING`，VPC创建结果可以通过调用`DescribeVpcs`接口查询，如果VPC状态由`CREATING`(创建中)变为`AVAILABLE`，则代表VPC创建成功，`CREATE_FAILED`代表VPC创建失败。创建过程中不可对VPC进行任何操作。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称            | 必选 | 类型     | 描述                                                                 |
| --------------- | -- | ------ | ------------------------------------------------------------------ |
| vpcRegionId     | 是  | String | VPC的节点ID。                                                          |
| cidrBlock       | 是  | String | VPC的CIDR。                                                          |
| vpcName         | 是  | String | <p>VPC的名称。</p><p>范围1到64个字符。仅支持输入字母、数字、-和英文句点(.)。</p>               |
| resourceGroupId | 否  | String | <p>VPC所在的资源组ID。</p><p>如果不指定，则会放入默认资源组， 如果用户没有默认资源组权限， 则请求将会失败。</p> |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| vpcId     | String | VPC的ID。                                                  |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 创建CHI1节点的VPC。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: CreateVpc
<Common Request Params>

Request:
{
  "vpcRegionId": "CHI1",
  "cidrBlock": "10.0.0.0/8",
  "vpcName": "1122"
}

Response:
{
  "requestId": "T3811A0E7-C250-40A2-96AD-08AD759E1BC2",
  "response": {
    "requestId": "T3811A0E7-C250-40A2-96AD-08AD759E1BC2",
    "vpcId": "835957634816289496"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                           | 说明                 |
| ------- | --------------------------------------------- | ------------------ |
| 404     | INVALID\_VPC\_REGION\_NOT\_FOUND              | VPC RegionId 不存在。  |
| 403     | OPERATION\_DENIED\_VPC\_REGION\_EXCEED\_LIMIT | VPC RegionId下数量限制。 |
| 400     | INVALID\_PARAMETER\_VPC\_LAN\_IP\_NETMASK     | CidrBlock 掩码范围错误。  |
| 400     | INVALID\_PARAMETER\_VPC\_CIDR\_BLOCK          | CidrBlock 参数格式错误。  |
| 400     | INVALID\_PARAMETER\_VPC\_LAN\_IP              | CidrBlock 不是私网IP。  |
