# DescribeImageQuota

## 1. 接口描述

本接口（DescribeImageQuota）用于查询可创建镜像的配额。

{% hint style="info" %}
**注意事项**

* 每个区域最多只支持创建**5**个自定义镜像，如有特殊需求可联系Support增加上限。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称      | 必选 | 类型              | 描述                                                                                                                                                                                         |
| --------- | -- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| regionIds | 否  | Array of String | <p>区域ID。<br>可从<a href="https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/~/changes/271/xu-ni-ji/gong-gong-xin-xi/describeregions">DescribeRegions</a>的regionId中获取。</p> |

## 3. 响应结果

| 参数名称      | 类型                                                                                                                                      | 描述                                         |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| requestId | String                                                                                                                                  | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |
| images    | Array of [ImageQuotaInfo](https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/xu-ni-ji/shu-ju-jie-gou#imagequotainfo) | 结果集。                                       |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **查询用户帐号各区域的镜像配额**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: DescribeImageQuota
<Common Request Params>

Response:
{
  "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9",
  "response": {
    "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9",
    "imageRegionQuota": [
      {
        "regionId": "sa-jeddah-1a",
        "count": "0",
        "maxCount": "5"
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

| HTTP状态码 | 错误码                         | 说明         |
| ------- | --------------------------- | ---------- |
| **404** | INVALID\_REGION\_NOT\_FOUND | 没有找到指定的区域。 |
