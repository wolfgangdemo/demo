---
description: ModifySecurityGroupsAttribute
---

# ModifySecurityGroupsAttribute

## 1. 接口描述

本接口用于修改SecurityGroup的属性（目前只支持修改SecurityGroup的名称）。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称              | 必选 | 类型              | 描述                                                                                                                                        |
| ----------------- | -- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| securityGroupIds  | 是  | Array of String | <p>一个或多个待操作的SecurityGroup ID。</p><p>可通过<code>DescribeSecurityGroups</code>接口返回值中的securityGroupId获取。</p><p>每次请求批量SecurityGroup的上限为100。</p> |
| securityGroupName | 是  | String          | <p>SecurityGroup名称。</p><p>范围1到64个字符。仅支持输入字母、数字、-和英文句点(.)。</p>                                                                             |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **批量修改SecurityGroup的名称。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: ModifySecurityGroupsAttribute
<Common Request Params>

Request:
{
  "securityGroupIds": [
    "675574041725115352"
  ],
  "securityGroupName": "111"
}

Response:
{
  "requestId": "T261F6869-69AE-4F8B-9C23-9A774C83C62D",
  "response": {
    "requestId": "T261F6869-69AE-4F8B-9C23-9A774C83C62D"
  }
}
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

