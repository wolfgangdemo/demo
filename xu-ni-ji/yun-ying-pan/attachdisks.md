# AttachDisks

## 1. 接口描述

本接口（AttachDisks）用于用于挂载云硬盘到云主机实例。

{% hint style="info" %}
**注意事项**

* 只有当云硬盘的状态为**Attaching(待挂载)**时才允许挂载云硬盘。
* 单次最多可挂载**10**块云硬盘。
* 挂载云硬盘的数量不能超过实例可用的最大数量。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称       | 必选 | 类型              | 描述         |
| ---------- | -- | --------------- | ---------- |
| diskIds    | 是  | Array of String | 云硬盘ID集合。   |
| instanceId | 是  | String          | 需要挂载的实例ID。 |

## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **挂载云硬盘到云主机实例。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: AttachDisks
<Common Request Params>

Response:

```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                              | 说明               |
| ------- | -------------------------------- | ---------------- |
| **400** | INVALID\_ILLEGAL\_DISK\_PORTABLE | 无法操作不可移动的云盘。     |
| **400** | INVALID\_ILLEGAL\_DISK\_STATUS   | 所选云盘的状态无法操作。     |
| **400** | INVALID\_INSTANCE\_REINITING     | 无法操作正在初始化的实例。    |
| **400** | INVALID\_REGION\_MISMATCH        | 云盘与需要绑定的实例区域不匹配。 |
| **400** | INVALID\_EXCEED\_LIMITATION      | 超出实例可挂载云盘的最大数量   |

