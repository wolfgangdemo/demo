# ModifyImagesAttributes

## 1. 接口描述

本接口（ModifyImageAttribute）用于修改镜像属性。

{% hint style="info" %}
**注意事项**

* 目前支持修改自定义镜像的属性有：
  * 镜像描述。
* 如果传入多个镜像ID，仅支持所有镜像修改为同一属性。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称             | 必选 | 类型              | 描述                                                                                                                                                                                 |
| ---------------- | -- | --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| imageIds         | 是  | Array of String | <p>镜像ID。<br>可从<a href="https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/~/changes/117/xu-ni-ji/jing-xiang/describeimages">DescribeImages</a>返回的imageId获取。</p> |
| imageDescription | 否  | String          | <p>新的镜像描述。<br>不超过255个字符。</p>                                                                                                                                                       |

## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **修改镜像属性。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: ModifyImagesAttributes
<Common Request Params>

Response:

```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)
