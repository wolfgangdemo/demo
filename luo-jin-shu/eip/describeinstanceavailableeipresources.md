# DescribeInstanceAvailableEipResources

## 1. 接口描述

调用本接口用于查询实例可绑定的EIP列表。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称       | 必选 | 类型     | 描述                                                                                     |
| ---------- | -- | ------ | -------------------------------------------------------------------------------------- |
| instanceId | 是  | String | <p>机器实例ID 。</p><p>可通过<code>DescribeInstances</code>接口返回的<code>instanceId</code>获取。</p> |



## 3. 响应结果

| 参数名称                 | 类型                                                                        | 描述                                                       |
| -------------------- | ------------------------------------------------------------------------- | -------------------------------------------------------- |
| requestId            | String                                                                    | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| instanceEipResources | Array of [InstanceAvailableEip](../datastructure.md#instanceavailableeip) | 实例可用EIP列表。                                               |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. 获取机器实例可用的EIP列表

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: DescribeInstanceAvailableEipResources
<Common Request Params>

Request：
{
    "instanceId": "instanceId1"
}

Response：
{
  "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
  "response": { 
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3"，
    "instanceEipResources": [
        {
             "eipId": "eipId1",
             "ipAddress: "xx.x.x.x"
        }
    ]
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码 | 说明 |
| ------- | --- | -- |
|         |     |    |
