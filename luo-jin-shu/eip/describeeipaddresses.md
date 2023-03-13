# DescribeEipAddresses

## 1. 接口描述

调用本接口用于查询一台或多台指定EIP的信息。用户可以根据EIP ID、IP或者计费模式等信息来搜索EIP的信息。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称            | 必选 | 类型              | 描述                                                        |
| --------------- | -- | --------------- | --------------------------------------------------------- |
| eipChargeType   | 否  | String          | <p>付费类型。</p><p>PREPAID：预付费，即包年包月。</p><p>POSTPAID：后付费。</p> |
| eipIds          | 否  | Array of String | 取值可以由多个EIP ID共同组成。最多支持100个ID查询。                           |
| eipStatus       | 否  | String          | [EIP状态](../datastructure.md#eipstatus)。                   |
| instanceId      | 否  | String          | 机器实例ID。                                                   |
| instanceName    | 否  | String          | 机器实例名称。                                                   |
| ipAddress       | 否  | String          | IP地址。                                                     |
| zoneId          | 否  | String          | EIP所属的可用区ID。                                              |
| resourceGroupId | 否  | String          | <p>资源组的ID。</p><p>如果不传，则返回该用户可见的所有资源组内的EIP。</p>            |
| pageNum         | 否  | Integer         | <p>返回的分页数。</p><p>默认为1。</p>                                |
| pageSize        | 否  | Integer         | <p>返回的分页大小。</p><p>默认为20，最大为1000。</p>                      |



## 3. 响应结果

| 参数名称       | 类型                                                    | 描述                                                       |
| ---------- | ----------------------------------------------------- | -------------------------------------------------------- |
| requestId  | String                                                | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| dataSet    | Array of [EipAddress](../datastructure.md#eipaddress) | EIP列表。                                                   |
| totalCount | Integer                                               | 符合条件的EIP总数量。                                             |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. 列表根据eipChargeType搜索

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: DescribeEipAddresses
<Common Request Params>

Request：
{
    "eipChargeType": "PREPAID"
}

Response：
{   
  "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
  "response": {
     "requestId": "T98044459-95B2-477E-9A2F-00253A70CC6E"，
     "dataSet": [
         {
            "eipId": "eipId1",
            "zoneId": "SEL-A",
            "ipAddress": "x.x.x.x",
            "instanceId": "instanceId1",
            "instanceName": "instanceName",
            "eipChargeType": "PREPAID",
            "period": 1,
            "createTime": "2022-09-25T16:53:38Z",
            "expiredTime": "2022-10-25T16:53:38Z",
            "eipStatus": "AVAILABLE",
            "resourceGroupId": "xx",
            "resourceGroupName": "xx"
         }
     ],
     totalCount: 1
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
|         |     |    |
|         |     |    |
