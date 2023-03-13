---
description: DescribeVpcs
---

# DescribeVpcs

## 1. 接口描述

本接口用于查询一个或多个指定VPC的信息。用户可以根据VPC ID、Subnet ID、 VPC节点ID、VPC名称等信息来搜索VPC信息。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称            | 必选 | 类型              | 描述                                                   |
| --------------- | -- | --------------- | ---------------------------------------------------- |
| vpcIds          | 否  | Array of String | <p>VPC ID。</p><p>取值可以由多个VPC ID组成一个。最多支持100个ID查询。</p> |
| cidrBlock       | 否  | String          | VPC的CIDR。                                            |
| vpcStatus       | 否  | String          | [VPC的状态。](../datastructure.md#vpcstatus)             |
| vpcName         | 否  | String          | VPC的名称。                                              |
| vpcRegionId     | 否  | String          | VPC的节点ID。                                            |
| resourceGroupId | 否  | String          | <p>资源组的ID。</p><p>如果不传，则返回该用户可见的所有资源组内的Ddos IP。</p>   |
| pageSize        | 否  | Integer         | <p>返回的分页大小。</p><p>默认为20，最大为1000。</p>                 |
| pageNum         | 否  | Integer         | <p>返回的分页数。</p><p>默认为1。</p>                           |



## 3. 响应结果

| 参数名称       | 类型                                              | 描述                                                       |
| ---------- | ----------------------------------------------- | -------------------------------------------------------- |
| requestId  | String                                          | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| dataSet    | Array of [VpcInfo](../datastructure.md#vpcinfo) | VpcInfo结果集。                                              |
| totalCount | Integer                                         | 符合条件的数据总数。                                               |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 分页查询Vpc列表**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: DescribeVpcs
<Common Request Params>

Request:
{
  "pageSize": 10,
  "pageNum": 1
}

Response:
{
  "requestId": "T890357C5-9793-4668-BB32-217134475DAC",
  "response": {
    "requestId": "T890357C5-9793-4668-BB32-217134475DAC",
    "totalCount": 9,
    "dataSet": [
      {
        "vpcId": "675574041725115352",
        "vpcRegionId": "HKG5",
        "vpcRegionName": "HKG-A_C",
        "vpcName": "111",
        "cidrBlock": "10.0.0.0/8",
        "createTime": "2022-07-21T02:45:01Z",
        "vpcStatus": "AVAILABLE",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group"
      },
      {
        "vpcId": "677036631693206488",
        "vpcRegionId": "CHI1",
        "vpcRegionName": "CHI-A",
        "vpcName": "VPC-CHI-A-Default",
        "cidrBlock": "10.0.0.0/8",
        "createTime": "2022-07-23T03:10:55Z",
        "vpcStatus": "DELETING",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group"
      },
      {
        "vpcId": "695843306310998744",
        "vpcRegionId": "MAA2",
        "vpcRegionName": "MAA-A_C",
        "vpcName": "VPC-MAA-A_C-Default",
        "cidrBlock": "10.0.0.0/16",
        "createTime": "2022-08-18T01:56:26Z",
        "vpcStatus": "CREATING",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group"
      },
      {
        "vpcId": "705474328350696152",
        "vpcRegionId": "SIN3",
        "vpcRegionName": "SIN-A_B",
        "vpcName": "VPC-SIN-A_B-Default",
        "cidrBlock": "10.0.0.0/8",
        "createTime": "2022-08-31T08:51:35Z",
        "vpcStatus": "CREATING",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group"
      },
      {
        "vpcId": "706724644945666264",
        "vpcRegionId": "AMS2",
        "vpcRegionName": "AMS-C",
        "vpcName": "VPC-AMS-C-Default",
        "cidrBlock": "10.0.0.0/8",
        "createTime": "2022-09-02T02:15:42Z",
        "vpcStatus": "CREATING",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group"
      },
      {
        "vpcId": "706839622411361496",
        "vpcRegionId": "TYO2",
        "vpcRegionName": "TYO-A",
        "vpcName": "VPC-TYO-A-Default",
        "cidrBlock": "10.0.0.0/8",
        "createTime": "2022-09-02T06:04:09Z",
        "vpcStatus": "CREATING",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group"
      },
      {
        "vpcId": "736091361115114712",
        "vpcRegionId": "AMS2",
        "vpcRegionName": "AMS-C",
        "vpcName": "VPC-AMS-C-Default",
        "cidrBlock": "10.0.0.0/8",
        "createTime": "2022-10-12T14:42:08Z",
        "vpcStatus": "CREATING",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group"
      },
      {
        "vpcId": "750526251764025304",
        "vpcRegionId": "FRA5",
        "vpcRegionName": "FRA-B_D_E",
        "vpcName": "VPC-FRA-B_D_E-Default",
        "cidrBlock": "10.0.0.0/8",
        "createTime": "2022-11-01T12:41:41Z",
        "vpcStatus": "CREATING",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group"
      },
      {
        "vpcId": "786474054256176856",
        "vpcRegionId": "LAX5",
        "vpcRegionName": "LAX-C_D_E",
        "vpcName": "VPC-LAX-C-Default",
        "cidrBlock": "10.0.0.0/8",
        "createTime": "2022-12-21T03:03:33Z",
        "vpcStatus": "CREATING",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
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

| HTTP状态码 | 错误码 | 说明 |
| ------- | --- | -- |
|         |     |    |
