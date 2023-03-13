# CreateImage

## 1. 接口描述

本接口（CreateImage）用于创建自定义镜像。

{% hint style="info" %}
**注意事项**

* 每个区域最多只支持创建**5**个自定义镜像，当该地区达到最大限额时，将无法继续创建自定义镜像，如有特殊需求可联系**Support**增加上限。
* 制作镜像会拷贝实例的系统盘，创建时请确保实例处于**关机**状态，不要对实例进行任何操作。
* 创建出的镜像大小与实例的系统盘大小相同。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称             | 必选 | 类型     | 描述                                                                 |
| ---------------- | -- | ------ | ------------------------------------------------------------------ |
| instanceId       | 是  | String | 需要制作镜像的实例ID。                                                       |
| imageName        | 是  | String | <p>镜像名称。</p><ul><li>长度不超过24位</li><li>支持中文、字母、数字或连接符号 -_.</li></ul> |
| imageDescription | 否  | String | <p>镜像描述。<br>不超过255个字符。</p>                                         |

## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |
| imageId   | String | 镜像ID。                                      |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **创建一个镜像。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: CreateImage
<Common Request Params>

Response:
{
  "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9",
  "response": {
    "requestId": "T4C35327C-7B13-47B8-A815-5E5213D4A9F9",
    "imageId": "img-tqcr7c2e"
  }
}
```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                               | 说明            |
| ------- | ------------------------------------------------- | ------------- |
| **404** | INVALID\_INSTANCE\_NOT\_FOUND                     | 没有找到实例。       |
| **400** | UNSUPPORTED\_OPERATION\_INSTANCE\_STATE\_STARTING | 实例开机中，不允许该操作。 |
| **400** | LIMIT\_EXCEEDED\_IMAGE\_QUOTA                     | 镜像配额超出限制。     |
