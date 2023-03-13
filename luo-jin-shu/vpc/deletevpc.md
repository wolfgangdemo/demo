---
description: DeleteVpc
---

# DeleteVpc

## 1. 接口描述

本接口用于删除一个Vpc。

{% hint style="info" %}
**注意事项**

* 本接口为异步接口，当删除Vpc请求下发成功后会返回一个RequestId，此时删除Vpc操作并未立即完成。在此期间Vpc的状态将会处于`DELETING`，结果可以通过调用`DescribeVpcs`接口查询，如果Vpc列表不存在该Vpc，则代表Vpc删除成功。`DELETING`状态不能进行任何操作。
* 不能删除存在Subnet的Vpc，可通过`DescribeVpcs`接口查看。
* 该接口只能被处于 **AVAILABLE** 或 **CREATE\_FAILED**  状态的Vpc调用。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称  | 必选 | 类型     | 描述      |
| ----- | -- | ------ | ------- |
| vpcId | 是  | String | VPC的ID。 |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 删除VPC。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: DeleteVpc
<Common Request Params>

Request:
{
  "vpcId": "835957634816289496"
}

Response:
{
  "requestId": "TBDB421E3-47F4-46FD-AE4E-C912CB89744E",
  "response": {
    "requestId": "TBDB421E3-47F4-46FD-AE4E-C912CB89744E"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                           | 说明            |
| ------- | --------------------------------------------- | ------------- |
| 403     | OPERATION\_DENIED\_VPC\_STATUS\_NOT\_SUPPORT  | VPC状态不支持。     |
| 403     | OPERATION\_DENIED\_VPC\_EXIST\_SUBNET\_ASSIGN | VPC下存在Subent。 |
| 403     | OPERATION\_DENIED\_VPC\_EXIST\_INSTANCE       | VPC下存在实例。     |
|         |                                               |               |
