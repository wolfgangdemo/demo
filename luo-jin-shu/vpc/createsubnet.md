---
description: CreateVpc
---

# CreateSubnet

## 1. 接口描述

本接口用于创建一个私有网络Subnet。

#### 准备工作

* 查询可用区是否可创建Subnet：调用`DescribeSubnetAvailableResources`查看。
* 你可以创建一个单独的子网，也可以在VPC下创建子网，作为实现节点内不同可用区内网互联，推荐使用VPC下创建子网。当然你也可以选择在单独创建子网后再升级到VPC下。

{% hint style="info" %}
**注意事项**

* 同一个可用区能创建的Subnet资源个数也是有限制的，详见 Subnet使用限制，如果需要申请更多资源，请提交Support申请。
* 本接口为异步接口，当创建Subnet请求下发成功后会返回一个Subnet`ID`列表，此时创建Subnet操作并未立即完成。在此期间Subnet的状态将会处于`CREATING`，Subnet创建结果可以通过调用`DescribeSubnets`接口查询，如果Subnet状态由`CREATING`(创建中)变为`AVAILABLE`，则代表Subnet创建成功，`CREATE_FAILED`代表Subnet创建失败。创建过程中不可对Subnet进行任何操作。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称            | 必选 | 类型     | 描述                                                                                                                                                                               |
| --------------- | -- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| zoneId          | 是  | String | 可用区的节点ID。                                                                                                                                                                        |
| cidrBlock       | 是  | String | <p>Subnet的CIDR。</p><p>可选值<code>10.0.0.0/16</code>、<code>172.16.0.0/16</code>和<code>192.168.0.0/16</code>及它们包含的子网。</p><p>如果指定了VPC ID，那么子网网段必须在VPC的CIDR范围之内，且不能和VPC下其他子网网段有重叠。</p> |
| subnetName      | 是  | String | <p>Subnet的名称。</p><p>范围1到64个字符。仅支持输入字母、数字、-和英文句点(.)。</p>                                                                                                                          |
| resourceGroupId | 否  | String | <p>Subnet所在的资源组ID。</p><p>如果不指定，则会放入默认资源组， 如果用户没有默认资源组权限， 则请求将会失败。</p><p>如果指定VPC，则会忽略该参数自动使用与VPC相同的资源组。</p>                                                                       |
| vpcId           | 否  | String | VPC的ID。                                                                                                                                                                          |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| subnetId  | String | Subnet的ID。                                               |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 在SIN-B可用区创建Subnet。**

<pre class="language-json"><code class="lang-json"><strong>POST / HTTP/1.1
</strong>Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: CreateSubnet
&#x3C;Common Request Params>

Request:
{
  "zoneId": "SIN-B",
  "cidrBlock": "10.0.0.0/16",
  "subnetName": "Subnet-Test-alict"
}

Response:
{
  "requestId": "T39EC84B4-63B4-409E-A09D-F052434DF276",
  "response": {
    "requestId": "T39EC84B4-63B4-409E-A09D-F052434DF276",
    "subnetId": "832999436413042904"
  }
}
</code></pre>
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                                 | 说明                   |
| ------- | --------------------------------------------------- | -------------------- |
| 403     | OPERATION\_DENIED\_ZONE\_NOT\_SUPPORT\_SUBNET       | 可用区不支持创建Subnet。      |
| 404     | INVALID\_VPC\_NOT\_FOUND                            | VPC不存在。              |
| 403     | OPERATION\_DENIED\_VPC\_STATUS\_NOT\_SUPPORT        | VPC状态不支持。            |
| 403     | OPERATION\_DENIED\_NO\_AVAILABLE\_VPC\_REGION       | VPC RegionId 不可用。    |
| 403     | OPERATION\_DENIED\_ZONE\_NOT\_BELONG\_VPC           | 可用区不属于VPC RegionId。  |
| 400     | INVALID\_PARAMETER\_SUBNET\_CIDR\_BLOCK             | CidrBlock 参数格式错误。    |
| 400     | INVALID\_PARAMETER\_SUBNET\_LAN\_IP\_NETMASK        | CidrBlock 掩码范围错误。    |
| 400     | INVALID\_PARAMETER\_SUBNET\_LAN\_IP                 | CidrBlock 不是私网IP。    |
| 403     | OPERATION\_DENIED\_SUBNET\_EXCEED\_LIMIT            | Subnet在可用区数量限制。      |
| 403     | OPERATION\_DENIED\_VPC\_ZONE\_SUBNET\_EXCEED\_LIMIT | VPC 可用区下Subnet数量限制。  |
| 400     | INVALID\_PARAMETER\_VPC\_SUBNET\_OVER\_LAP          | Subnet网段与VPC下的网段有重叠。 |
| 404     | INVALID\_ZONE\_NOT\_FOUND                           | 指定的区域不存在。            |
| 400     | INVALID\_PARAMETER\_SUBNET\_CIDR\_NOT\_BELONG\_VPC  | Subnet网段不属于VPC网段下。   |
