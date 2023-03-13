---
description: DeleteSubnet
---

# DeleteSubnet

## 1. 接口描述

本接口用于删除一个Subnet。

{% hint style="info" %}
**注意事项**

* 本接口为异步接口，当删除Subnet请求下发成功后会返回一个RequestId，此时删除Subnet操作并未立即完成。在此期间Subnet的状态将会处于`DELETING`，结果可以通过调用`DescribeSubnets`接口查询，如果Subnet列表不存在该Subnet，则代表Subnet删除成功。`DELETING`状态不能进行任何操作。
* 不能删除存在实例的Subnet，可通过`DescribeSubnets`接口查看。
* 该接口只能处于 **AVAILABLE** 或 **CREATE\_FAILED** 状态的Subnet调用。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称     | 必选 | 类型     | 描述         |
| -------- | -- | ------ | ---------- |
| subnetId | 是  | String | Subnet的ID。 |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 删除Subnet。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: DeleteSubnet
<Common Request Params>

Request:
{
  "subnetId": "833032938374308056"
}

Response:
{
  "requestId": "TA8D35A96-1BCC-4D10-96CB-CCB7600C1428",
  "response": {
    "requestId": "TA8D35A96-1BCC-4D10-96CB-CCB7600C1428"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                             | 说明            |
| ------- | ----------------------------------------------- | ------------- |
| 400     | OPERATION\_FAILED\_RESOURCE\_NOT\_FOUND         | 指定的Subnet不存在。 |
| 403     | OPERATION\_DENIED\_SUBNET\_EXIST\_INSTANCE      | Subnet下存在实例。  |
| 403     | OPERATION\_DENIED\_SUBNET\_STATUS\_NOT\_SUPPORT | Subnet的状态不支持。 |
|         |                                                 |               |
