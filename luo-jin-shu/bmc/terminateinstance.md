# TerminateInstance

## 1. 接口描述

本接口用于退还一个实例。

{% hint style="info" %}
**注意事项**

* 不再使用的实例，可通过本接口主动退还。如果是后付费，退还的实例将停止计费。
* 本接口无法主动退还预付费订阅模式的实例，**订阅模式**的实例将会在订阅到期后自动退还。
* 退还后的实例将进入回收站，进入回收站后如无其他操作实例将在24小时后自动释放，也可以调用`ReleaseInstances`接口主动进行释放。
* 已经在回收站中或者正在创建中的实例调用该接口无效。
* 创建失败并且状态为`CREATE_FAILED`的实例调用本接口会直接删除实例，对于预付费的实例会退还所有的支付金额。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称       | 必选 | 类型     | 描述                                                                                        |
| ---------- | -- | ------ | ----------------------------------------------------------------------------------------- |
| instanceId | 是  | String | <p>待操作的实例ID。</p><p>可通过<code>DescribeInstances</code>接口返回值中的<code>instanceId</code>获取。</p> |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **退还指定ID的实例**

退还实例ID为`instanceId`的实例。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: TerminateInstance
<Common Request Params>

Request:
{
  "instanceId": "instanceId"
}

Response:
{
  "requestId": "TC1748D3E-452D-4F74-8485-7AA73718E453",
  "response": {
    "requestId": "TC1748D3E-452D-4F74-8485-7AA73718E453"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                             | 说明                |
| ------- | ----------------------------------------------- | ----------------- |
| 404     | INVALID\_INSTANCE\_NOT\_FOUND                   | 指定的实例不存在。         |
| 403     | OPERATION\_DENIED\_INSTANCE\_RECYCLED           | 已经在回收站中的实例不支持该操作。 |
| 403     | OPERATION\_DENIED\_INSTANCE\_CREATING           | 创建中的实例不支持该操作。     |
| 403     | OPERATION\_DENIED\_INSTANCE\_STATUS\_INSTALLING | 安装中的实例不支持该操作。     |
| 403     | OPERATION\_DENIED\_INSTANCE\_SUBSCRIPTION       | 订阅模式的实例不支持该操作。    |
| 403     | OPERATION\_DENIED\_POSTPAID\_PROMISE            | 资源处于后付费承诺期，无法手动终止 |
|         |                                                 |                   |

