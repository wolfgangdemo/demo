# DeleteImages

## 1. 接口描述

本接口（DeleteImages）用于删除一个或多个镜像。

{% hint style="info" %}
**注意事项**

* 当[镜像状态](https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/xu-ni-ji/shu-ju-jie-gou#imageinfo)为**可用(Available)**时才允许删除。镜像状态(imageStatus)可从[DescribeImages](https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/\~/changes/117/xu-ni-ji/jing-xiang/describeimages)的imageId中获取。
* 每个地域最多只支持创建**5**个自定义镜像，删除自定义镜像可以释放账户的配额。
* 如果镜像已经用来创建了云硬盘或实例，则必须先将云硬盘或实例删除。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称     | 必选 | 类型              | 描述            |
| -------- | -- | --------------- | ------------- |
| imageIds | 是  | Array of String | 将要被删除的镜像ID集合。 |

## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **删除一个或多个镜像。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: DeleteImages
<Common Request Params>

Response:
{
  "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9",
  "response": {
    "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9"
  }
}
```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                        | 说明         |
| ------- | -------------------------- | ---------- |
| **404** | INVALID\_IMAGE\_NOT\_FOUND | 没有找到指定的镜像。 |
