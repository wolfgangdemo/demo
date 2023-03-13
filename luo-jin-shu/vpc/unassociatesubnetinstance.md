---
description: UnAssociateSubnetInstance
---

# UnAssociateSubnetInstance

## 1. 接口描述

本接口用于将某子网下一台实例从Subnet中解绑。

{% hint style="info" %}
**注意事项**

* 本接口属于异步接口，即系统会先返回一个请求ID，并不表示实例解绑Subnet完成，系统后台的解绑任务仍在进行。您可以调用`DescribeSubnets`查询Subnet下实例绑定状态：
  * 当privateIpStatus 处于**UNBINDING**状态时，表示实例正在解绑Subnet
  * 当Subnet不存在实例，表示实例解绑Subnet成功
* Subnet与实例的绑定状态privateIpStatus为**BINDED**才能操作，如果实例不在子网下，将不会进行任何操作。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称       | 必选 | 类型     | 描述         |
| ---------- | -- | ------ | ---------- |
| subnetId   | 是  | String | Subnet的ID。 |
| instanceId | 是  | String | 实例的ID。     |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 实例解绑Subnet。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: UnAssociateSubnetInstance
<Common Request Params>

Request:
{
  "subnetId": "833049815985166808",
  "instanceId": "820653960707704280"
}

Response:
{
  "requestId": "T5B77142F-C218-4AD1-89A4-70082816CA6B",
  "response": {
    "requestId": "T5B77142F-C218-4AD1-89A4-70082816CA6B"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                              | 说明            |
| ------- | ------------------------------------------------ | ------------- |
| 404     | INVALID\_SUBNET\_NOT\_FOUND                      | Subnet不存在。    |
| 403     | OPERATION\_DENIED\_SUBNET\_ASSOCIATING\_INSTANCE | Subnet正在绑定实例。 |
|         |                                                  |               |
