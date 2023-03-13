---
description: AssociateSubnetInstances
---

# AssociateSubnetInstances

## 1. 接口描述

本接口用于将一台或多台实例加入同一个子网并分配内网IP。

{% hint style="info" %}
**注意事项**

* 本接口属于异步接口，即系统会先返回一个请求ID，并不表示实例绑定Subnet完成，系统后台的绑定任务仍在进行。您可以调用DescribeSubnets 查询Subnet 下实例绑定状态：
  * 当privateIpStatus 处于**BINDED**状态时，表示实例已成功绑定Subnet
  * 当privateIpStatus 处于**BINDING**状态时，表示实例正在绑定Subnet
  * 当privateIpStatus 处于**UNBINDING**状态时，表示实例正在解绑Subnet
* 实例状态需为`RUNNING`才能够绑定Subnet 。
* Subnet与实例的可用区需一致。
* Subnet状态需为`AVAILABLE`且Subnet还有剩余可用IP。
* 通常情况下，一台实例只允许加入一个子网如果实例已经加入其他子网，则操作将会失败。如果有特殊场景需要加入多个子网，请联系Support。
* 支持批量操作，每次请求批量实例上限为100。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称               | 必选 | 类型                                                                              | 描述            |
| ------------------ | -- | ------------------------------------------------------------------------------- | ------------- |
| subnetId           | 是  | String                                                                          | Subnet ID。    |
| subnetInstanceList | 是  | Array of [AssociateSubnetInstance](../datastructure.md#associatesubnetinstance) | Subnet绑定实例集合。 |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 实例绑定Subnet。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: AssociateSubnetInstances
<Common Request Params>

Request:
{
  "subnetId": "833049815985166808",
  "subnetInstanceList": [
    {
      "instanceId": "820653960707704280",
      "privateIpAddress": "10.0.0.2"
    }
  ]
}

Response:
{
  "requestId": "TD3AA7771-C9C1-4EC2-A743-FD934710CEB6",
  "response": {
    "requestId": "TD3AA7771-C9C1-4EC2-A743-FD934710CEB6"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                               | 说明                  |
| ------- | ------------------------------------------------- | ------------------- |
| 403     | OPERATION\_DENIED\_INSTANCE\_NOT\_SUPPORT\_SUBNET | 实例不支持绑定Subnet。      |
| 403     | OPERATION\_DENIED\_INSTANCE\_NOT\_RUNNING         | 实例状态不是Running。      |
| 404     | INVALID\_SUBNET\_NOT\_FOUND                       | Subnet不存在。          |
| 403     | OPERATION\_DENIED\_SUBNET\_STATUS\_NOT\_SUPPORT   | Subnet状态不支持。        |
| 403     | OPERATION\_DENIED\_DIFFERENT\_ZONE                | Subnet与实例有不一致的可用区。  |
| 403     | OPERATION\_DENIED\_SUBNET\_EXIST\_INSTANCE        | Subnet存在实例。         |
| 400     | INVALID\_PARAMETER\_DUPLICATE\_LAN\_IP            | Subnet分配重复的内网IP给实例。 |
| 400     | INVALID\_PARAMETER\_LAN\_IP\_NOT\_SUPPORT         | .1结尾的内网IP不支持。       |
| 403     | OPERATION\_DENIED\_IP\_ASSOCIATED\_INSTANCE       | 内网IP已经绑定实例。         |
| 403     | OPERATION\_DENIED\_SUBNET\_NOT\_REPEAT\_INSTANCE  | Subnet下实例不能重复。      |
