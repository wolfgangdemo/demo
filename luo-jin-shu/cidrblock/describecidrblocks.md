# DescribeCidrBlocks

## 1. 接口描述

调用本接口用于查询一个或多个Cidr Block的信息。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称            | 必选 | 类型              | 描述                                                        |
| --------------- | -- | --------------- | --------------------------------------------------------- |
| cidrBlockIds    | 否  | Array of String | <p>Cidr Block ID。</p><p>最多支持100个ID查询。</p>                 |
| cidrBlock       | 否  | String          | CIDR。                                                     |
| cidrBlockName   | 否  | String          | Cidr Block名称。                                             |
| zoneId          | 否  | String          | Cidr Block所属的可用区ID。                                       |
| cidrBlockType   | 否  | String          | <p>Cidr Block的类型。</p><p>取值范围：IPV4、IPV6。</p>               |
| gateway         | 否  | String          | 网关地址。                                                     |
| chargeType      | 否  | String          | <p>计费类型。</p><p>PREPAID：预付费，即包年包月。</p><p>POSTPAID：后付费。</p> |
| resourceGroupId | 否  | String          | <p>资源组的ID。</p><p>如果不传，则返回该用户可见的所有资源组内的实例。</p>             |
| pageSize        | 否  | Integer         | <p>返回的分页大小。</p><p>默认为20，最大为1000。</p>                      |
| pageNum         | 否  | Integer         | <p>返回的分页数。</p><p>默认为1。</p>                                |



## 3. 响应结果

| 参数名称       | 类型                                                          | 描述                                                       |
| ---------- | ----------------------------------------------------------- | -------------------------------------------------------- |
| requestId  | String                                                      | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| totalCount | Integer                                                     | 符合条件的数据总数。                                               |
| dataSet    | Array of [CidrBlockInfo](../datastructure.md#cidrblockinfo) | 结果集。                                                     |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 分页查询Cidr Block列表**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: DescribeCidrBlocks
<Common Request Params>

Request:
{
  "pageNum": 1,
  "pageSize": 1
}

Response:
{
  "requestId": "T9731D74B-4EA3-498E-AC75-4C036ABAF598",
  "response": {
    "requestId": "T9731D74B-4EA3-498E-AC75-4C036ABAF598",
    "totalCount": 14,
    "dataSet": [
      {
        "cidrBlockId": "767715590704998412",
        "cidrBlockType": "IPV4",
        "cidrBlockName": "mycidrblock",
        "zoneId": "CHI-A",
        "cidrBlock": "1.1.218.184/29",
        "gateway": "1.1.218.185",
        "availableIpStart": "1.1.218.186",
        "availableIpEnd": "1.1.218.190",
        "availableIpCount": 5,
        "instanceIds": [
          "780812773306141196"
        ],
        "status": "RECYCLE",
        "chargeType": "POSTPAID",
        "createTime": "2022-11-25T05:53:50Z",
        "expireTime": "2022-11-25T08:00:42Z",
        "resourceGroupId": "5eab5afc-88a2-46a9-bad3-278df7069f13",
        "resourceGroupName": "Default Resource Group"
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

| HTTP状态码 | 错误码                       | 说明        |
| ------- | ------------------------- | --------- |
| 404     | INVALID\_ZONE\_NOT\_FOUND | 指定的区域不存在。 |
