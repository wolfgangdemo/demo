# DescribeDisks

## 1. 接口描述

本接口DescribeDisks用于查询云硬盘列表。

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称       | 必选 | 类型                                                                                                                                    | 描述                                                                                                                                                                                         |
| ---------- | -- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| diskIds    | 否  | Array of String                                                                                                                       | 云硬盘ID集合。                                                                                                                                                                                   |
| diskName   | 否  | String                                                                                                                                | 云硬盘名称。                                                                                                                                                                                     |
| diskStatus | 否  | [Diskstatus](https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/\~/changes/236/xu-ni-ji/shu-ju-jie-gou#diskstatus) | 云硬盘状态。                                                                                                                                                                                     |
| diskType   | 否  | String                                                                                                                                | <p>云硬盘类型。</p><ul><li>System-系统盘。</li><li>Data-数据盘。</li></ul>                                                                                                                               |
| diskSize   | 否  | Integer                                                                                                                               | 云硬盘大小，单位GB。                                                                                                                                                                                |
| portable   | 否  | Boolean                                                                                                                               | 是否可拔插。                                                                                                                                                                                     |
| instanceId | 否  | String                                                                                                                                | 实例ID。                                                                                                                                                                                      |
| regionId   | 否  | String                                                                                                                                | <p>区域ID。<br>可从<a href="https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/~/changes/271/xu-ni-ji/gong-gong-xin-xi/describeregions">DescribeRegions</a>的regionId中获取。</p> |
| pageSize   | 否  | Integer                                                                                                                               | <p>返回的分页大小。</p><p>默认为20，最大为1000。</p>                                                                                                                                                       |
| pageNum    | 否  | Integer                                                                                                                               | <p>返回的分页数。</p><p>默认为1。</p>                                                                                                                                                                 |

## 3. 响应结果

| 参数名称      | 类型                                                                                                                          | 描述                                         |
| --------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| requestId | String                                                                                                                      | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |
| disks     | Array of [DiskInfo](https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/xu-ni-ji/shu-ju-jie-gou#diskinfo) | 结果集。                                       |

## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **查询云硬盘列表。**

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/vm
Content-Type: application/json
X-TC-Action: DescribeDisks
<Common Request Params>

Response:

```
{% endtab %}
{% endtabs %}

## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                         | 说明        |
| ------- | --------------------------- | --------- |
| **404** | INVALID\_REGION\_NOT\_FOUND | 指定的区域不存在。 |
