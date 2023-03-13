# BindCidrBlockIps

## 1. 接口描述

调用本接口用于实例绑定一个或多个Cidr Block IP。

{% hint style="info" %}
**注意事项**

* 只有状态为 **AVAILABLE** 的Cidr Block才能操作。
* Cidr Block与实例的可用区需一致。
* 实例的状态需要是**RUNNING。**
* 本接口属于异步接口，即系统会先返回一个请求ID，但Cidr Block与实例并未绑定完成，系统后台的绑定任务仍在进行。您可以调用`DescribeCidrBlockIps`查询Cidr Block的绑定状态。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称        | 必选 | 类型                                                      | 描述                                                                                                   |
| ----------- | -- | ------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| cidrBlockId | 是  | String                                                  | <p>待操作的Cidr Block ID。</p><p>可通过<code>DescribeCidrBlocks</code>接口返回值中的<code>cidrBlockId</code>获取。</p> |
| ipBindList  | 是  | Array of [IpBindParam](../datastructure.md#ipbindparam) | 待绑定的IP参数列表。                                                                                          |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 批量绑定IP**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: BindCidrBlockIps
<Common Request Params>

Request:
{
  "cidrBlockId": "cidrBlockId",
  "ipBindList": [
    {
      "instanceId": "instanceId1",
      "ip": "1111:1111:2:25::2"
    },
    {
      "instanceId": "instanceId2",
      "ip": "1.1.1.1"
    }
  ]
}

Response:
{
  "requestId": "T2979BBDB-5B06-444F-857E-93FEFE665C0D",
  "response": {
    "requestId": "T2979BBDB-5B06-444F-857E-93FEFE665C0D"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                                   | 说明                       |
| ------- | ----------------------------------------------------- | ------------------------ |
| 404     | INVALID\_CIDRBLOCK\_NOT\_FOUND                        | 指定的Cidr Block不存在。        |
| 404     | INVALID\_INSTANCE\_NOT\_FOUND                         | 指定的实例不存在。                |
| 403     | OPERATION\_DENIED\_INSTANCE\_NOT\_RUNNING             | 指定的实例不是运行状态。             |
| 403     | OPERATION\_DENIED\_DIFFERENT\_ZONE                    | 指定的实例和Cidr Block不在同一个区域。 |
| 403     | OPERATION\_DENIED\_CIDRBLOCK\_RECYCLED                | 在回收站中的Cidr Block不支持该操作。  |
| 403     | OPERATION\_DENIED\_CIDRBLOCK\_IP\_COUNT\_REACH\_LIMIT | 已绑定的IP数量达到了上限。           |
