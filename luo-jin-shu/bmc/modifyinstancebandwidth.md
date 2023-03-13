# ModifyInstanceBandwidth

## 1. 接口描述

调用本接口用于修改实例带宽。

{% hint style="info" %}
**注意事项**

* 不同机型带宽上限范围不一致（可通过`DescribeInstanceTypes`接口获取）。
* 仅实例状态处于`RUNNING`状态，接口才能调用。
* 若当前实例的带宽在赠送带宽内，要修改的带宽在赠送带宽内，不涉及价格，立即生效。
* 若机器的[internetChargeType](../datastructure.md#internetchargetype)为ByBandwidth：
  * 实例的`instanceChargeType`为PREPAID：
    * 升配（target > cur）会生成待支付的订单，需要扣除本次升配的费用，立即生效。
    * 降配（target < cur）会生成下个周期的降配订单，下周期生效。
  * 实例的`instanceChargeType`为POSTPAID：
    * 立即生效。
  * 询带宽变更价格接口`DescribeInstanceBandwidth`。
* 本接口调用是异步操作，若该变更需要支付则会返回订单号。若订单号为空，则当前实例带宽变更状态为`CHANGING`，系统后台的变更带宽任务正在处理。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称             | 必选 | 类型      | 描述                                                                                        |
| ---------------- | -- | ------- | ----------------------------------------------------------------------------------------- |
| instanceId       | 是  | String  | <p>待操作的实例ID。</p><p>可通过<code>DescribeInstances</code>接口返回值中的<code>instanceId</code>获取。</p> |
| bandwidthOutMbps | 是  | Integer | <p>带宽。</p><p>范围：1~机型最大。</p>                                                               |



## 3. 响应结果

| 参数名称        | 类型     | 描述                                                       |
| ----------- | ------ | -------------------------------------------------------- |
| requestId   | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 requestId。</p> |
| orderNumber | String | 订单编号。                                                    |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. 升配实例的带宽

```javascript
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: ModifyInstanceBandwidth
<Common Request Params>

Request：
{
  "instanceId": "instanceId",
  "bandwidthOutMbps": 100
}

Response：
{
  "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
  "response": {  
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
    "orderNumber": "xxxx"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                       | 说明            |
| ------- | ----------------------------------------- | ------------- |
| 404     | INVALID\_INSTANCE\_NOT\_FOUND             | 指定的实例不存在。     |
| 403     | OPERATION\_DENIED\_INSTANCE\_NOT\_RUNNING | 指定的实例状态不是运行中。 |
| 400     | INVALID\_PARAMETER\_BANDWIDTH\_EXCEED     | 带宽参数超出最大值。    |
