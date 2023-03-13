---
description: DescribeSubnetAvailableResources
---

# DescribeSubnetAvailableResources

## 1. 接口描述

本接口用于查询可创建Subnet资源的可用区。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称   | 必选 | 类型     | 描述                                        |
| ------ | -- | ------ | ----------------------------------------- |
| zoneId | 否  | String | <p>可用区ID。</p><p>不传则查询所有可创建Subnet的可用区。</p> |



## 3. 响应结果

| 参数名称      | 类型              | 描述                                                       |
| --------- | --------------- | -------------------------------------------------------- |
| requestId | String          | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |
| zoneIdSet | Array of zoneId | zone结果集。                                                 |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 查询SEL-A可用区能否创建Subnet。**

<pre class="language-json"><code class="lang-json">POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: DescribeSubnetAvailableResources
&#x3C;Common Request Params>
<strong>
</strong><strong>Request:
</strong>{
  "zoneId": "SEL-A"
}

Response:
{
  "requestId": "T0C815970-AE04-470B-B22A-67C42DDFA679",
  "response": {
    "requestId": "T0C815970-AE04-470B-B22A-67C42DDFA679",
    "zoneIdSet": [
      "SEL-A"
    ]
  }
}
</code></pre>
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                       | 说明        |
| ------- | ------------------------- | --------- |
| 404     | INVALID\_ZONE\_NOT\_FOUND | 指定的区域不存在。 |
