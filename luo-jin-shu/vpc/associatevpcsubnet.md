---
description: AssociateVpcSubnet
---

# AssociateVpcSubnet

## 1. 接口描述

本接口用于为VPC添加Subnet。

{% hint style="info" %}
**注意事项**

* 本接口属于异步接口，即系统会先返回一个请求ID，并不表示Subnet绑定VPC完成，系统后台的绑定任务仍在进行。您可以调用`DescribeSubnets`查询Subnet绑定VPC状态。
* 指定Subnet的CIDR必须在VPC的CIDR范围内，且不能和VPC下其他子网的CIDR有重叠。
* 指定的Subnet的可用区必须包含在指定VPC节点内，可以通过`DescribeVpcAvailableRegions`来查看VPC节点下的可用区。
* 如果Subnet已经在VPC下，将不会进行任何操作。
* VPC状态需是`AVAILABLE`且Subnet状态需是`AVAILABLE`才能进行操作。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称     | 必选 | 类型     | 描述         |
| -------- | -- | ------ | ---------- |
| subnetId | 是  | String | Subnet的ID。 |
| vpcId    | 是  | String | VPC的ID。    |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. VPC添加Subnet。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: AssociateVpcSubnet
<Common Request Params>

Request:
{
  "subnetId": "426257512392561112",
  "vpcId": "835957634816289496"
}

Response:
{
  "requestId": "T7D2DD189-870C-4B13-B812-0A3C7B8D83F1",
  "response": {
    "requestId": "T7D2DD189-870C-4B13-B812-0A3C7B8D83F1"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                                 | 说明                        |
| ------- | --------------------------------------------------- | ------------------------- |
| 404     | INVALID\_VPC\_NOT\_FOUND                            | VPC不存在。                   |
| 404     | INVALID\_SUBNET\_NOT\_FOUND                         | Subnet不存在。                |
| 403     | OPERATION\_DENIED\_SUBNET\_STATUS\_NOT\_SUPPORT     | Subnet状态不支持。              |
| 403     | OPERATION\_DENIED\_SUBNET\_ASSOCIATED\_OTHER\_VPC   | Subnet已绑定其他VPC。           |
| 403     | OPERATION\_DENIED\_VPC\_STATUS\_NOT\_SUPPORT        | VPC状态不支持。                 |
| 403     | OPERATION\_DENIED\_NO\_AVAILABLE\_VPC\_REGION       | VPC RegionId 不可用。         |
| 403     | OPERATION\_DENIED\_ZONE\_NOT\_BELONG\_VPC           | Subnet可用区不属于VPC RegionId。 |
| 403     | OPERATION\_DENIED\_VPC\_ZONE\_SUBNET\_EXCEED\_LIMIT | VPC 可用区下Subnet数量限制。       |
| 400     | INVALID\_PARAMETER\_VPC\_SUBNET\_OVER\_LAP          | Subnet网段与VPC下的网段有重叠。      |
