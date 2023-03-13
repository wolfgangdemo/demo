---
description: DescribeVpcAvailableRegions
---

# DescribeVpcAvailableRegions

## 1. 接口描述

本接口用于查询支持VPC组网的节点区域信息。

{% hint style="info" %}
**注意事项**

* 可能会注意到VPC节点ID有诸如`LAX2` 和 `LAX2_2.0,`这个原因是当前节点内的可用区属于不同的网络架构，目前无法做到内网子网间互通，故分拆成了不同的VPC节点。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称        | 必选 | 类型     | 描述        |
| ----------- | -- | ------ | --------- |
| zoneId      | 否  | String | 所属的可用区ID。 |
| vpcRegionId | 否  | String | VPC的节点ID。 |



## 3. 响应结果

| 参数名称         | 类型                                                          | 描述                                                       |
| ------------ | ----------------------------------------------------------- | -------------------------------------------------------- |
| requestId    | String                                                      | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| vpcRegionSet | Array of [VpcRegionInfo](../datastructure.md#vpcregioninfo) | VpcRegionInfo结果集。                                        |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 查询vpcRegionId为SIN3下的可用区ID**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: DescribeVpcAvailableRegions
<Common Request Params>

Request:
{
  "vpcRegionId": "SIN3"
}

Response:
{
  "requestId": "TAB1B2BEB-9FC9-4D19-82E5-175ECA8CE8A7",
  "response": {
    "requestId": "TAB1B2BEB-9FC9-4D19-82E5-175ECA8CE8A7",
    "vpcRegionSet": [
      {
        "vpcRegionName": "SIN-A_B",
        "zoneIds": [
          "SIN-A",
          "SIN-B"
        ],
        "vpcRegionId": "SIN3"
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
