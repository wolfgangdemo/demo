# CreateDisks

## 1. 接口描述

本接口（CreateDisks）用于创建一个或多个云硬盘。

{% hint style="info" %}
**注意事项**

* 云硬盘大小不得小于**20**，如有特殊需求可联系Support降低下限。
* 云硬盘大小不得大于**2000**，如有特殊需求可联系Support增加上限。
* 预付费云硬盘的购买会预先扣除本次实例购买所需金额，如果余额不足，请求将会失败。后付费实例购买时需要确保账户账号状态正常。
* 调用本接口创建云硬盘，支持代金券自动抵扣，详情请参考代金券选用规则。
* 本接口为异步接口，当创建云盘请求下发成功后会返回一个云盘`ID`列表，此时创建云盘操作并未立即完成。在此期间云盘的状态将会处于**AVAILABLE（待挂载）**或**ATTACHING（挂载中）**，云盘创建结果可以通过[DescribeDisks](https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/xu-ni-ji/yun-ying-pan/describeimages-1)查询，如果云盘状态(diskStatus)由**AVAILABLE(待挂载)**或**ATTACHING（挂载中）**变为**IN\_USE（使用中）**，则代表云硬盘创建成功，查询不到则代表云硬盘创建失败，创建过程中不可对云硬盘进行任何操作。
* 如果选择创建后挂载到实例，则diskAmount不能超过实例可挂载云硬盘的最大数量。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称            | 必选 | 类型                                                                | 描述                                                                                                                                                                                                                        |
| --------------- | -- | ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| chargeType      | 是  | String                                                            | <p>付费类型。</p><p>PREPAID：预付费，即包年包月。</p><p>POSTPAID：后付费。</p>                                                                                                                                                                 |
| chargePrepaid   | 否  | [ChargePrepaid](../../luo-jin-shu/datastructure.md#chargeprepaid) | <p>预付费模式。<br>即包年包月相关参数设置。通过该参数可以指定包年包月实例的购买时长等属性。若指定实例的付费模式为预付费则该参数必传。</p>                                                                                                                                                |
| diskName        | 否  | String                                                            | <p>云盘名称。</p><ul><li>必须以数字或字母开头或结尾。</li><li>长度在1和64个字符之间。</li><li>仅支持输入字母、数字、空格、-和英文句点(.)。</li></ul>                                                                                                                       |
| diskSize        | 否  | Integer                                                           | 云盘大小，单位GB，最小值20。                                                                                                                                                                                                          |
| diskAmount      | 否  | Integer                                                           | <p>云盘创建数量。</p><p>最小值与默认值均为1。</p>                                                                                                                                                                                          |
| instanceId      | 否  | String                                                            | 创建后需要挂载的实例ID。                                                                                                                                                                                                             |
| regionId        | 否  | String                                                            | <p>云盘所属的区域ID。<br>如果传了instanceId，则该字段无效。<br>可从<a href="https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/~/changes/271/xu-ni-ji/gong-gong-xin-xi/describeregions">DescribeRegions</a>的regionId中获取。</p> |
| resourceGroupId | 否  | String                                                            | 实例所在的资源组ID，如不指定则放入默认资源组。                                                                                                                                                                                                  |

## 3. 响应结果

| 参数名称        | 类型              | 描述                                         |
| ----------- | --------------- | ------------------------------------------ |
| requestId   | String          | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |
| diskIds     | Array of String | 云硬盘ID集合。                                   |
| orderNumber | String          | 订单编号。                                      |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **创建一个或多个云硬盘。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: CreateDisks
<Common Request Params>

Response:

```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                        | 说明                |
| ------- | ------------------------------------------ | ----------------- |
| **400** | INVALID\_ILLEGAL\_DISK\_SIZE               | 云硬盘大小超出最大（小）值限制。  |
| **404** | INVALID\_REGION\_NOT\_FOUND                | 区域不存在。            |
| **400** | INVALID\_REGION\_MISMATCH                  | 云硬盘区域与需挂载的实例区域不符。 |
| **400** | EXCEED\_INSTANCE\_DISK\_AMOUNT\_LIMITATION | 超出实例还能挂载的数据盘数量。   |
| **404** | INVALID\_INSTANCE\_NOT\_FOUND              | 需要挂载的实例不存在。       |
