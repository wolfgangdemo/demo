---
description: Instance
---

# ChangeDisksAttach

## 1. 接口描述

本接口（ChangeDisksAttach）用于将一个或多个已经挂载到一台实例的云硬盘挂载到另外一台实例上。

{% hint style="info" %}
**注意事项**

* 此接口相当于先后进行DetachDisks与AttachDisks操作。
* 云硬盘当前的状态(diskStatus)必须处于**挂载中**。
* 云硬盘当前所挂载的实例可以不同。
* 更换挂载的云硬盘数量不能超过新的实例所挂载的最大数量。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称       | 必选 | 类型              | 描述         |
| ---------- | -- | --------------- | ---------- |
| diskIds    | 是  | Array of String | 云硬盘ID集合。   |
| instanceId | 是  | String          | 需要挂载的新实例D。 |

## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **换绑实例。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: ChangeDisksAttach
<Common Request Params>

Response:

```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                       | 说明                  |
| ------- | ------------------------- | ------------------- |
| **400** | INVALID\_DISK\_NOT\_FOUND | 无法找到指定的云硬盘。         |
| **400** | ILLEGAL\_DISK\_STATUS     | 所选云盘的状态无法操作。        |
| **400** | INSTANCE\_REINITING       | 需要挂载的新实例正在格式化。      |
| **400** | REGION\_MISMATCH          | 云硬盘与需要挂载的新实例不在同一区域。 |
| **400** | EXCEED\_LIMITATION        | 超出新实例可挂载云硬盘的最大数量    |

