---
description: DescribeSubnets
---

# DescribeSubnets

## 1. 接口描述

本接口用于查询一台或多台指定Subnet的信息。用户可以根据Subnet ID、VPC ID、 区域、Subnet 名称等信息来搜索Subnet信息。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称            | 必选 | 类型              | 描述                                                         |
| --------------- | -- | --------------- | ---------------------------------------------------------- |
| subnetIds       | 否  | Array of String | <p>Subnet ID。</p><p>取值可以由多个Subnet ID组成一个。最多支持100个ID查询。</p> |
| cidrBlock       | 否  | String          | Subnet的CIDR。                                               |
| zoneId          | 否  | String          | Subnet所属的可用区ID。                                            |
| subnetStatus    | 否  | String          | [Subnet的状态。](../datastructure.md#subnetstatus)             |
| subnetName      | 否  | String          | Subnet的名称。                                                 |
| resourceGroupId | 否  | String          | <p>资源组的ID。</p><p>如果不传，则返回该用户可见的所有资源组内的Ddos IP。</p>         |
| vpcId           | 否  | String          | VPC ID。                                                    |
| pageSize        | 否  | Integer         | <p>返回的分页大小。</p><p>默认为20，最大为1000。</p>                       |
| pageNum         | 否  | Integer         | <p>返回的分页数。</p><p>默认为1。</p>                                 |



## 3. 响应结果

| 参数名称       | 类型                                                    | 描述                                                       |
| ---------- | ----------------------------------------------------- | -------------------------------------------------------- |
| requestId  | String                                                | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| dataSet    | Array of [SubnetInfo](../datastructure.md#subnetinfo) | SubnetInfo结果集。                                           |
| totalCount | Integer                                               | 符合条件的数据总数。                                               |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 分页查询CidrBlock为“10.0.0.0/8”的Subnet列表**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: DescribeSubnets
<Common Request Params>

Request:
{
  "cidrBlock": "10.0.0.0/8",
  "pageSize": 10,
  "pageNum": 1
}

Response:
{
  "requestId": "T2CF86177-29D1-41C0-91E7-542C38C194D7",
  "response": {
    "requestId": "T2CF86177-29D1-41C0-91E7-542C38C194D7",
    "totalCount": 8,
    "dataSet": [
      {
        "subnetId": "669986345980014296",
        "subnetName": "Subnet-LAX3B-Default",
        "zoneId": "LAX-B",
        "availableIpCount": "16777213",
        "cidrBlock": "10.0.0.0/8",
        "subnetStatus": "AVAILABLE",
        "createTime": "2022-07-13T09:43:16Z",
        "vpcSubnetStatus": "BINDED",
        "vpcId": null,
        "vpcName": null,
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group",
        "subnetInstanceSet": null
      },
      {
        "subnetId": "669998042870457304",
        "subnetName": "Subnet-LAX3B-Default",
        "zoneId": "LAX-B",
        "availableIpCount": "16777213",
        "cidrBlock": "10.0.0.0/8",
        "subnetStatus": "AVAILABLE",
        "createTime": "2022-07-13T10:06:31Z",
        "vpcSubnetStatus": "BINDED",
        "vpcId": null,
        "vpcName": null,
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group",
        "subnetInstanceSet": null
      },
      {
        "subnetId": "670074179940261592",
        "subnetName": "Subnet-SIN4E-Default",
        "zoneId": "SIN-E",
        "availableIpCount": "16777213",
        "cidrBlock": "10.0.0.0/8",
        "subnetStatus": "AVAILABLE",
        "createTime": "2022-07-13T12:37:47Z",
        "vpcSubnetStatus": "BINDED",
        "vpcId": null,
        "vpcName": null,
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group",
        "subnetInstanceSet": null
      },
      {
        "subnetId": "675574042144543192",
        "subnetName": "Subnet-HKG5A-Deafault",
        "zoneId": "HKG-A",
        "availableIpCount": "16777213",
        "cidrBlock": "10.0.0.0/8",
        "subnetStatus": "AVAILABLE",
        "createTime": "2022-07-21T02:45:02Z",
        "vpcSubnetStatus": "BINDED",
        "vpcId": "675574041725115352",
        "vpcName": "VPC-HKG-A-Default",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group",
        "subnetInstanceSet": null
      },
      {
        "subnetId": "706839622444915160",
        "subnetName": "Subnet-TYO2A-Default",
        "zoneId": "TYO-A",
        "availableIpCount": "16777213",
        "cidrBlock": "10.0.0.0/8",
        "subnetStatus": "CREATING",
        "createTime": "2022-09-02T06:04:09Z",
        "vpcSubnetStatus": "BINDING",
        "vpcId": "706839622411361496",
        "vpcName": "VPC-TYO-A-Default",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group",
        "subnetInstanceSet": null
      },
      {
        "subnetId": "736091361970760152",
        "subnetName": "Subnet-AMS-C-Default",
        "zoneId": "AMS-C",
        "availableIpCount": "16777213",
        "cidrBlock": "10.0.0.0/8",
        "subnetStatus": "CREATING",
        "createTime": "2022-10-12T14:42:08Z",
        "vpcSubnetStatus": "BINDING",
        "vpcId": "736091361115114712",
Disconnected from the target VM, address: '127.0.0.1:56971', transport: 'socket'
        "vpcName": "VPC-AMS-C-Default",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group",
        "subnetInstanceSet": null
      },
      {
        "subnetId": "750526252527395288",
        "subnetName": "Subnet-FRA-B-Default",
        "zoneId": "FRA-B",
        "availableIpCount": "16777213",
        "cidrBlock": "10.0.0.0/8",
        "subnetStatus": "CREATING",
        "createTime": "2022-11-01T12:41:41Z",
        "vpcSubnetStatus": "BINDING",
        "vpcId": "750526251764025304",
        "vpcName": "VPC-FRA-B_D_E-Default",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group",
        "subnetInstanceSet": null
      },
      {
        "subnetId": "786474054390385368",
        "subnetName": "Subnet-LAX-C-Default",
        "zoneId": "LAX-C",
        "availableIpCount": "16777213",
        "cidrBlock": "10.0.0.0/8",
        "subnetStatus": "CREATING",
        "createTime": "2022-12-21T03:03:33Z",
        "vpcSubnetStatus": "BINDING",
        "vpcId": "786474054256176856",
        "vpcName": "VPC-LAX-C-Default",
        "resourceGroupId": "5a4f6519-2977-47cb-b3fc-150fd2b4de71",
        "resourceGroupName": "Default Resource Group",
        "subnetInstanceSet": null
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
