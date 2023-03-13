# UnAssociateDdosIpAddress

## 1. 接口描述

调用本接口将Ddos IP上已绑定的机器解绑。

{% hint style="info" %}
#### 注意事项

* 对于状态为 **`INUSE`**和 **`AVAILABLE` ** 的Ddos IP **** 可以进行该操作，如果状态为**`AVAILABLE`**，将不会有任何变更。
* 对 **INUSE** 的Ddos IP进行操作成功后，Ddos IP的状态将变为**UNACCOSCIATING。**
* 本接口属于异步接口，即系统会先返回一个请求ID，但Ddos IP并未完成解绑，系统后台的解绑任务仍在进行。您可以调用`DescribeDdosIpAddresses`查询Ddos IP的状态：
  * 当Ddos IP处于**UNACCOSCIATING**状态时，表示Ddos IP正在解绑中，在该状态下，您只能执行查询操作，不能执行其他操作。
  * 当Ddos IP处于**AVAILABLE** 时，表示Ddos IP完成解绑。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称     | 必选 | 类型     | 描述                                                                                                 |
| -------- | -- | ------ | -------------------------------------------------------------------------------------------------- |
| ddosIpId | 是  | String | <p>一个Ddos IP ID。</p><p>可通过<code>DescribeDdosIpAddresses</code>接口返回值中的 <code>ddosIpId</code>获取。</p> |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. Ddos IP解绑实例

指定Ddos IP解绑实例。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: UnAssociateDdosIpAddress
<Common Request Params>

Request：
{
    "ddosIpId": "ddosIpId1"
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

| HTTP状态码 | 错误码                                               | 说明               |
| ------- | ------------------------------------------------- | ---------------- |
| 404     | INVALID\_DDOS\_IP\_NOT\_FOUND                     | 指定的Ddos IP不存在。   |
| 403     | FAILED\_OPERATION\_FOR\_RECYCLE\_RESOURCE         | 指定的Ddos IP在回收站。  |
| 403     | OPERATION\_DENIED\_DDOS\_IP\_STATUS\_NOT\_SUPPORT | 指定的Ddos IP状态不支持。 |
