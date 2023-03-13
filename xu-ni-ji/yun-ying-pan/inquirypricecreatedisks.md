# InquiryPriceCreateDisks

## 1. 接口描述

本接口（InquiryPriceCreateDisks）用于创建云硬盘询价。

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称          | 必选 | 类型                                                                | 描述                                                                                                                                                                                         |
| ------------- | -- | ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| regionId      | 是  | String                                                            | <p>区域ID。<br>可从<a href="https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/~/changes/271/xu-ni-ji/gong-gong-xin-xi/describeregions">DescribeRegions</a>的regionId中获取。</p> |
| diskSize      | 是  | Integer                                                           | 云盘大小，单位GB。                                                                                                                                                                                 |
| diskAmount    | 否  | Integer                                                           | <p>创建云硬盘数量。</p><p>最小值与默认值均为1。</p>                                                                                                                                                          |
| chargeType    | 是  | String                                                            | <p>付费类型。</p><p>PREPAID：预付费，即包年包月。</p><p>POSTPAID：后付费。</p>                                                                                                                                  |
| chargePrepaid | 否  | [ChargePrepaid](../../luo-jin-shu/datastructure.md#chargeprepaid) | <p>预付费模式，即包年包月相关参数设置。</p><p>通过该参数可以指定包年包月实例的购买时长等属性。</p><p>若指定实例的付费模式为预付费则该参数必传。</p>                                                                                                       |

## 3. 响应结果

| 参数名称          | 类型                                                | 描述                                         |
| ------------- | ------------------------------------------------- | ------------------------------------------ |
| requestId     | String                                            | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |
| dataDiskPrice | [Price](../../luo-jin-shu/datastructure.md#price) | 云盘价格。                                      |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **创建云硬盘询价。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: InquiryPriceCreateDisks
<Common Request Params>

Response:

```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                          | 说明        |
| ------- | ---------------------------- | --------- |
| **404** | INVALID\_PRODUCT\_NOT\_FOUND | 云硬盘产品未找到。 |
