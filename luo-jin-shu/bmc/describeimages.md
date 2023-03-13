# DescribeImages

## 1. 接口描述

调用本接口用于查看镜像列表。

{% hint style="info" %}
**注意事项**

* 镜像列表中的镜像并不是适用于所有机型，具体机型适用的镜像可以根据`DescribeInstanceTypes`接口返回结构中的`imageIds`来查询。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称           | 必选 | 类型              | 描述                                                                                                           |
| -------------- | -- | --------------- | ------------------------------------------------------------------------------------------------------------ |
| imageIds       | 否  | Array of String | 镜像ID。                                                                                                        |
| imageName      | 否  | String          | 镜像名称。                                                                                                        |
| catalog        | 否  | String          | <p>镜像所属分类。</p><p>可能值：</p><ul><li>centos</li><li>windows</li><li>ubuntu</li><li>debian</li><li>esxi</li></ul> |
| imageType      | 否  | String          | <p>镜像类型。</p><p>PUBLIC_IMAGE: 公共镜像。</p><p>CUSTOM_IMAGE：自定义镜像。</p><p>目前不支持自主的创建自定义镜像，如有需求，请提交support。</p>      |
| osType         | 否  | String          | <p>操作系统类型。</p><p>可能值：</p><ul><li>windows</li><li>linux</li></ul>                                             |
| instanceTypeId | 否  | String          | 支持的机型ID。                                                                                                     |

## 3. 响应结果

| 参数名称      | 类型                                                  | 描述                                         |
| --------- | --------------------------------------------------- | ------------------------------------------ |
| requestId | String                                              | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |
| images    | Array of [ImageInfo](../datastructure.md#imageinfo) | 结果集。                                       |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **获取所有的镜像。**

不带任何参数查询所有的镜像。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: DescribeImages
<Common Request Params>

Response:
{
  "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9",
  "response": {
    "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9",
    "images": [
      {
        "imageId": "bd5faa16-39d2-4bbf-a5c8-b95a193b1626",
        "imageName": "CentOS7.4-x86_64",
        "catalog": "centos",
        "imageType": "PUBLIC_IMAGE",
        "osType": "linux"
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

| HTTP状态码 | 错误码                                 | 说明        |
| ------- | ----------------------------------- | --------- |
| **404** | INVALID\_INSTANCE\_TYPE\_NOT\_FOUND | 指定的机型不存在。 |
