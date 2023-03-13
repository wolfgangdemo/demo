# ModifyInstancesResourceGroup

## 1. 接口描述

调用本接口用于修改实例所属的资源组。

{% hint style="info" %}
**注意事项**

* 支持批量操作。每次请求批量实例的上限为100。
* 该接口只有管理员角色的用户能够进行操作。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称            | 必选 | 类型              | 描述                                     |
| --------------- | -- | --------------- | -------------------------------------- |
| instanceIds     | 是  | Array of String | <p>实例ID列表。<br>每次请求允许操作的实例数量上限是100。</p> |
| resourceGroupId | 是  | String          | 资源组ID。                                 |

## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **将实例移动到指定资源组。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: ModifyInstancesResourceGroup
<Common Request Params>

Request:
{
  "instanceIds": ["instanceId1", "instanceId2"],
  "resourceGroupId": "resourceGroup1"
}

Response:
{
  "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9",
  "response": {
    "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9"
  }
}
```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                            | 说明     |
| ------- | ---------------------------------------------- | ------ |
| 404     | OPERATION\_FAILED\_RESOURCE\_GROUP\_NOT\_FOUND | 资源组不存在 |
| 404     | OPERATION\_FAILED\_RESOURCE\_NOT\_FOUND        | 资源不存在  |
