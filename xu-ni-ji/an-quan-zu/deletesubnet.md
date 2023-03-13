---
description: DeleteSecurityGroup
---

# DeleteSecurityGroup

## 1. 接口描述

本接口用于删除一个SecurityGroup。

{% hint style="info" %}
**注意事项**

* 不能删除存在实例的SecurityGroup，可通过`DescribeSecurityGroups`接口查看。
* SecurityGroup状态需是 **AVAILABLE 或** **CREATE\_FAILED** 才可调用。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称            | 必选 | 类型     | 描述                |
| --------------- | -- | ------ | ----------------- |
| securityGroupId | 是  | String | SecurityGroup的ID。 |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 删除SecurityGroup。**

```json
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                     | 说明                   |
| ------- | --------------------------------------- | -------------------- |
| 400     | OPERATION\_FAILED\_RESOURCE\_NOT\_FOUND | 指定的SecurityGroup不存在。 |
|         |                                         |                      |
