# DescribeImages

## 1. 接口描述

本接口（DescribeImages）用于查看镜像列表。

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称        | 必选 | 类型              | 描述                                                                                                                                                                                         |
| ----------- | -- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| imageIds    | 否  | Array of String | <p>镜像ID。<br>可从<a href="https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/~/changes/117/xu-ni-ji/jing-xiang/describeimages">DescribeImages</a> 返回的imageId获取。</p>        |
| imageName   | 否  | String          | 镜像名称。                                                                                                                                                                                      |
| regionId    | 否  | String          | <p>区域ID。<br>可从<a href="https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/~/changes/271/xu-ni-ji/gong-gong-xin-xi/describeregions">DescribeRegions</a>的regionId中获取。</p> |
| category    | 否  | String          | <p>镜像所属分类。</p><p>可能值：</p><ul><li>CentOS</li><li>Windows</li><li>Ubuntu</li><li>Debian</li></ul>                                                                                            |
| imageType   | 否  | String          | <p>镜像类型。</p><ul><li>PUBLIC_IMAGE-公共镜像。</li><li>CUSTOM_IMAGE-自定义镜像。</li></ul>                                                                                                               |
| osType      | 否  | String          | <p>操作系统类型。</p><p>可能值：</p><ul><li>windows</li><li>linux</li></ul>                                                                                                                           |
| imageStatus | 否  | String          | <p>镜像状态。</p><ul><li>CREATING-创建中</li><li>AVAILABLE-可用</li><li>UNAVAILABLE-不可用</li></ul>                                                                                                    |
| pageNum     | 否  | Integer         | <p>返回的分页数。</p><p>默认为1。</p>                                                                                                                                                                 |
| pageSize    | 否  | Integer         | <p>返回的分页大小。</p><p>默认为20，最大为1000。</p>                                                                                                                                                       |

## 3. 响应结果

| 参数名称      | 类型                                         | 描述                                         |
| --------- | ------------------------------------------ | ------------------------------------------ |
| requestId | String                                     | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |
| images    | Array of [ImageInfo](../shu-ju-jie-gou.md) | 结果集。                                       |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **获取所有可用镜像。**

不带任何参数查询所有可用镜像。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: DescribeImages
<Common Request Params>

Response:
{
    "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9",
    "response": {
        "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9",
        "totalCount": 1,
        "images": [
            {
                "imageId": "img-R7sPhNGg",
                "imageName": "img-R7sPhNGg",
                "imageStatus": "AVAILABLE",
                "imageSize": 30,
                "imageDescription": "这是一个自定义镜像",
                "regionId": "de-frankfurt-9a",
                "createTime": "2023-03-02T01:42:01Z",
                "category": "Debian",
                "type": "linux",
                "version": "11.5"
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
