# ModifyCidrBlocksAttribute

## 1. 接口描述

本接口用于修改一个或多个Cidr Block的属性（目前只支持修改名称）。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称         | 必选 | 类型              | 描述                                                                                                                      |
| ------------ | -- | --------------- | ----------------------------------------------------------------------------------------------------------------------- |
| cidrBlockIds | 是  | Array of String | <p>一个或多个待操作的实例ID。</p><p>可通过<code>DescribeCidrBlocks</code>接口返回值中的<code>cidrBlockId</code>获取。</p><p>每次请求批量实例的上限为100。</p> |
| name         | 是  | String          | <p>Cidr Block的名称。</p><p>不得超过64个字符。</p>                                                                                  |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 批量修改Cidr Block的名称**

修改**`cidrBlockId1`**和**`cidrBlockId2`**的名称为**`myCidrBlockName`。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: ModifyCidrBlocksAttribute
<Common Request Params>

Request:
{
  "cidrBlockIds": [
    "cidrBlockId1",
    "cidrBlockId2"
  ],
  "name": "myCidrBlockName"
}

Response:
{
  "requestId": "TF7DE750F-B3AA-4A65-BB46-1EE89072FC04",
  "response": {
    "requestId": "TF7DE750F-B3AA-4A65-BB46-1EE89072FC04"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码 | 说明 |
| ------- | --- | -- |
|         |     |    |
