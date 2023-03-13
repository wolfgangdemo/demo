# DescribeZones

## 1. 接口描述 <a href="#1.-jie-kou-miao-shu" id="1.-jie-kou-miao-shu"></a>

本接口(DescribeZones)用于查询可用区信息。



## 2. 输入参数 <a href="#2.-shu-ru-can-shu" id="2.-shu-ru-can-shu"></a>

以下请求参数列表仅列出了接口中需要请求参数

| 参数名称           | 是否必选 | 类型     | 描述                                                                                   |
| -------------- | ---- | ------ | ------------------------------------------------------------------------------------ |
| acceptLanguage | 否    | String | <p>接收的区域地域的语言。可选值如下：</p><ul><li>zh-CN：中文</li><li>en-US：英文</li></ul><p>默认值：en-US。</p> |

&#x20;

## 3. 响应Response <a href="#3.-xiang-ying-response" id="3.-xiang-ying-response"></a>

| 参数名称      | 类型            | 描述                                                       |
| --------- | ------------- | -------------------------------------------------------- |
| requestId | String        | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 requestId。</p> |
| zoneSet   | Array of Zone | 可用区列表信息。                                                 |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. 查询可用区

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: DescribeZones
<Common Request Params>

Request：
{}

Response：
{
  "requestId": "TBD9EB7E4-3982-43F4-8479-7E963997BC85",
  "response": {  
    "requestId": "TBD9EB7E4-3982-43F4-8479-7E963997BC85",
    "zoneSet": [
        {
            "zoneId":"HKG-B",
            "zoneName":"HKG Zone B",
            "cityName":"Hong Kong",
            "areaName":"Asia Pacific"
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
