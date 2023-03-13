# ModifyInstanceTrafficPackage

## 1. 接口描述

调用本接口用于修改实例流量包。

{% hint style="info" %}
**注意事项**

* 仅机器状态处于`RUNNING`状态，接口才能调用。
* 若机器的[`internetChargeType`](../datastructure.md#internetchargetype)为`ByTrafficPackage`：
  * 机器的`instanceChargeType`为`PREPAID`：
    * 升配（target > cur）会生成待支付的订单，需要扣除本次升配的费用，立即生效。
    * 降配（target < cur）会生成下个周期的降配订单，下周期生效。
  * 询带宽变更价格接口`DescribeInstanceTrafficPackage`。
* 本接口调用是异步操作，若该变更需要支付则会返回订单号。若订单号为空，当前实例流量包变更状态为`CHANGING`，系统后台的变更流量包任务正在处理。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称               | 必选 | 类型         | 描述                                                                                        |
| ------------------ | -- | ---------- | ----------------------------------------------------------------------------------------- |
| instanceId         | 是  | String     | <p>待操作的实例ID。</p><p>可通过<code>DescribeInstances</code>接口返回值中的<code>instanceId</code>获取。</p> |
| trafficPackageSize | 是  | BigDecimal | 流量包大小。                                                                                    |



## 3. 响应结果

| 参数名称        | 类型     | 描述                                                       |
| ----------- | ------ | -------------------------------------------------------- |
| requestId   | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 requestId。</p> |
| orderNumber | String | 订单编号。                                                    |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. 升配实例流量包

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: ModifyInstanceTrafficPackage
<Common Request Params>

Request：
{
  "instanceId": "instanceId",
  "trafficPackageSize: 100
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

| HTTP状态码 | 错误码                                                         | 说明                                                                 |
| ------- | ----------------------------------------------------------- | ------------------------------------------------------------------ |
| 403     | OPERATION\_DENIED\_INSTANCE\_EXIST\_PAY\_ORDER              | 指定的实例存在待支付的流量包订单。                                                  |
| 403     | OPERATION\_DENIED\_INTERNET\_CHARGE\_TYPE\_NOT\_BY\_TRAFFIC | 指定的[实例网络模型](../datastructure.md#internetchargetype)不是ByTrafficPac。 |
| 400     | INVALID\_PARAMETER\_TRAFFIC\_PACKAGE\_ERROR                 | 实例流量包参数校验错误。                                                       |
| 403     | OPERATION\_FILED\_INSTANCE\_NOT\_EXIST\_TRAFFIC\_PACKAGE    | 指定的实例不存在流量包。                                                       |
| 403     | OPERATION\_FILED\_INSTANCE\_EXIST\_PLAN\_TRAFFIC\_PACKAGE   | 指定的实例存在降配计划订单。                                                     |
| 400     | INVALID\_PARAMETER\_TRAFFIC\_PACKAGE\_LESS                  | 实例流量包参数需要大于等于默认值。                                                  |
