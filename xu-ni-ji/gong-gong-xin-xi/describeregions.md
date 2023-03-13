# DescribeRegions

## 1. 接口描述

本接口(DescribeRegions)用于查询可用地区。

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称      | 必选 | 类型              | 描述      |
| --------- | -- | --------------- | ------- |
| regionIds | 否  | Array of String | 区域ID集合。 |

## 3. 响应结果

| 参数名称      | 类型                                                                                                                              | 描述                                         |
| --------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| regions   | Array of [RegionInfo](https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/xu-ni-ji/shu-ju-jie-gou#regioninfo) | 区域信息集合。                                    |
| requestId | String                                                                                                                          | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **查询可用地区。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: DescribeRegions
<Common Request Params>

Response:

```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)
