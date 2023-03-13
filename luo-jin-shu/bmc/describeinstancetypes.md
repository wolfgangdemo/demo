# DescribeInstanceTypes

## 1. 接口描述

调用本接口用于查询实例机型配置。

{% hint style="info" %}
**注意事项**

`DescribeInstanceTypes`仅查询实例机型的配置和性能信息，如果您需要查询具体地域下可购买的实例机型，请查询 `DescribeAvailableResources。`
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称                | 必选 | 类型               | 描述                                                                 |
| ------------------- | -- | ---------------- | ------------------------------------------------------------------ |
| instanceTypeIds     | 否  | Array of String  | <p>实例机型ID。<br>数量不超过100个。</p>                                       |
| minimumCpuCoreCount | 否  | Integer          | <p>查询实例机型时，期望最小CPU内核的数目。</p><p>取值范围：正整数。</p>                       |
| maximumCpuCoreCount | 否  | Integer          | <p>查询实例机型时，期望最大CPU内核的数目。</p><p>取值范围：正整数。</p>                       |
| minimumMemorySize   | 否  | Integer          | <p>查询实例机型时，期望最小内存大小。</p><p>取值范围：正整数。</p><p>单位：GB。</p>              |
| maximumMemorySize   | 否  | Integer          | <p>查询实例机型时，期望最大内存大小。</p><p>取值范围：正整数。</p><p>单位：GB。</p>              |
| minimumBandwidth    | 否  | Integer          | <p>查询实例机型时，期望最小公网入方向带宽限制。</p><p>单位：Mbps。</p>                       |
| supportRaids        | 否  | Array of Integer | <p>查询实例机型时，对实例机型做raid时所支持的raid类型。</p><p>Raid可选值包括：0, 1, 5, 10。</p> |
| supportSubnet       | 否  | Boolean          | 查询实例机型时，机型是否支持内网组网。                                                |
| minimumDiskSize     | 否  | Integer          | <p>查询实例机型时，期望最小磁盘大小。</p><p>取值范围：正整数。</p><p>单位：GB。</p>              |
| maximumDiskSize     | 否  | Integer          | <p>查询实例机型时，期望最大磁盘大小。</p><p>取值范围：正整数。</p><p>单位：GB。</p>              |
| isHA                | 否  | Boolean          | 查询实例机型时，是否是高可用机型。                                                  |
| imageId             | 否  | String           | 查询实例机型时，支持某镜像的机型。                                                  |

&#x20;

## 3. 响应结果

| 参数名称          | 类型                                                        | 描述                                                       |
| ------------- | --------------------------------------------------------- | -------------------------------------------------------- |
| instanceTypes | Array of [InstanceType](../datastructure.md#instancetype) | 查询的机型信息。                                                 |
| requestId     | String                                                    | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 requestId。</p> |

&#x20;

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **获取所有的机型。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: DescribeInstanceTypes
<Common Request Params>

Response:
{
  "requestId": "TE056C563-E5B1-46B5-9C5A-514B7501F420",
  "response": {
    "requestId": "TE056C563-E5B1-46B5-9C5A-514B7501F420",
    "instanceTypes": [
      {
        "imageIds": [
          "e3f1cf2e-8929-4b8a-8747-d0b779b770f7",
          "6059cf45-daf7-4954-80a2-346e8c3c5fd7"
        ],
        "instanceTypeId": "M9O",
        "description": "2x6248",
        "cpuCoreCount": 80,
        "memorySize": 256,
        "maximumBandwidth": 10000,
        "supportRaids": [0,1,5,10],
        "supportSubnet": true,
        "isHA": true,
        "diskInfo": {
          "totalDiskSize": 4000,
          "diskDescription": "4x1.2TB SAS",
          "disks": [
            {
              "diskSize": 1000,
              "diskCount": 4
            }
          ]
        }
      },
      {
        "imageIds": [
          "f9f9f8a2-24a1-44dd-9f60-36c3bc5c0dae"
        ],
        "instanceTypeId": "MGI",
        "description": "2x6248",
        "cpuCoreCount": 80,
        "memorySize": 256,
        "maximumBandwidth": 10000,
        "supportRaids": [0,1],
        "supportSubnet": true,
        "isHA": true,
        "diskInfo": {
          "totalDiskSize": 2000,
          "diskDescription": "2x1.2TB SAS",
          "disks": [
            {
              "diskSize": 1000,
              "diskCount": 2
            }
          ]
        }
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

| HTTP状态码 | 错误码  | 说明   |
| ------- | ---- | ---- |
| ****    | **** | **** |

