# TerminateDdosIpAddress

## 1. 接口描述

本接口用于退还一个Ddos IP。

{% hint style="info" %}
#### 注意事项

* 不再使用的Ddos IP，可通过本接口主动退还。如果是后付费，退还的Ddos IP将停止计费。
* 本接口无法主动退还预付费订阅模式的Ddos IP，**订阅模式**的 Ddos IP将会在订阅到期后自动退还。
* 退还后的 Ddos IP将进入回收站，进入回收站后如无其他操作 Ddos IP将在24小时后自动释放，也可以调用`ReleaseDdosIpAddresses`接口主动进行释放。
* 该接口只能被状态处于 **AVAILABLE** 或 **INUSE** 或 **CREATE\_FAILED 或 RECYCLE** 的Ddos IP调用。
* 对于创建失败状态为 **CREATE\_FAILED**的Ddos IP，会自动退还所有的已支付金额。
* 处于 **INUSE** 状态的Ddos IP，系统会将Ddos IP与机器解绑。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称     | 必选 | 类型     | 描述                                                                                    |
| -------- | -- | ------ | ------------------------------------------------------------------------------------- |
| ddosIpId | 是  | String | <p>一个Ddos IP ID。</p><p>可通过<code>DescribeDdosIpAddresses</code>接口返回值中的ddosIpId 获取。</p> |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. 退还指定ID的Ddos IP

退还指定的Ddos IP。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: TerminateDdosIpAddress
<Common Request Params>

Request：
{
    "ddosIpId": "ddosIpId"
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

| HTTP状态码 | 错误码                                       | 说明                     |
| ------- | ----------------------------------------- | ---------------------- |
| 404     | INVALID\_DDOS\_IP\_NOT\_FOUND             | 指定的Ddos IP不存在。         |
| 404     | INVALID\_DDOS\_IP\_ORDER\_NOT\_FOUND      | 指定的Ddos IP订单不存在。       |
| 403     | OPERATION\_DENIED\_DDOS\_IP\_SUBSCRIPTION | 订阅模式的Ddos IP不支持该操作。    |
| 403     | OPERATION\_DENIED\_DDOS\_IP\_RECYCLED     | 已经在回收站中的Ddos IP不支持该操作。 |
