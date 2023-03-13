# AssociateEipAddress

## 1. 接口描述

调用本接口将EIP绑定到同区域的机器实例上。

{% hint style="info" %}
#### 注意事项

* 只有状态为 **AVAILABLE** 的EIP才能操作。
* Exsi操作系统的机器实例无法绑定EIP。
* EIP与机器实例的可用区需一致。
* 机器实例的状态需要是**RUNNING。**
* 一个机器实例绑定的EIP数量有限额，如需提高限额，请联系support。
* 本接口属于异步接口，即系统会先返回一个请求ID，但EIP与机器实例并未绑定完成，系统后台的绑定任务仍在进行。您可以调用`DescribeEipAddresses`查询EIP的状态：
  * 当EIP处于 **ASSOCIATING** 状态时，表示EIP正在绑定中，在该状态下，您只能执行查询操作，不能执行其他操作。
  * 当EIP处于 **INUSE** 状态时，表示EIP绑定完成。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称       | 必选 | 类型     | 描述                                                                                      |
| ---------- | -- | ------ | --------------------------------------------------------------------------------------- |
| eipId      | 是  | String | <p>一个EIP ID。</p><p>可通过<code>DescribeEipAddresses</code>接口返回值中的<code>eipId</code>获取。</p> |
| instanceId | 是  | String | <p>机器实例ID。</p><p>可通过<code>DescribeInstances</code>接口返回值中的<code>instanceId</code>获取。</p> |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. EIP绑定机器实例&#x20;

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: AssociateEipAddress
<Common Request Params>

Request：
{
    "eipId": "eipId1"，
    "instanceId": "instanceId1"
}

Response：
{
  "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
  "response": {  
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                             | 说明               |
| ------- | ----------------------------------------------- | ---------------- |
| 404     | INVALID\_EIP\_NOT\_FOUND                        | 指定的EIP不存在。       |
| 403     | INVALID\_INSTANCE\_NOT\_FOUND                   | 实例不存在。           |
| 403     | OPERATION\_DENIED\_INSTANCE\_RECYCLED           | 实例在回收站。          |
| 403     | OPERATION\_DENIED\_INSTANCE\_NOT\_RUNNING       | 实例状态不是Running。   |
| 403     | OPERATION\_DENIED\_EIP\_ZONE\_NOT\_SAME         | 指定的EIP与实例区域不一致。  |
| 403     | FAILED\_OPERATION\_FOR\_RECYCLE\_RESOURCE       | 指定的EIP在回收站。      |
| 400     | OPERATION\_DENIED\_EIP\_STATUS\_NOT\_AVAILABLE  | 指定的EIP状态不可用。     |
| 403     | OPERATION\_DENIED\_EIP\_ESXI\_INSTANCE\_ASSIGN  | 指定的EIP不支持ESXI实例。 |
| 403     | OPERATION\_DENIED\_EIP\_INSTANCE\_EXCEED\_LIMIT | 实例绑定EIP数量超过限制。   |
