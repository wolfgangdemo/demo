---
description: DescribeSecurityGroups
---

# DescribeSecurityGroups

## 1. 接口描述

本接口用于查询一个或多个指定SecurityGroup的信息。用户可以根据SecurityGroup ID、SecurityGroup名称等信息来搜索SecurityGroup信息。



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称              | 必选 | 类型              | 描述                                                                       |
| ----------------- | -- | --------------- | ------------------------------------------------------------------------ |
| securityGroupIds  | 否  | Array of String | <p>SecurityGroup ID。</p><p>取值可以由多个SecurityGroup ID组成一个。最多支持100个ID查询。</p> |
| securityGroupName | 否  | String          | SecurityGroup的名称。                                                        |
| pageSize          | 否  | Integer         | <p>返回的分页大小。</p><p>默认为20，最大为1000。</p>                                     |
| pageNum           | 否  | Integer         | <p>返回的分页数。</p><p>默认为1。</p>                                               |



## 3. 响应结果

| 参数名称       | 类型                                                                   | 描述                                         |
| ---------- | -------------------------------------------------------------------- | ------------------------------------------ |
| requestId  | String                                                               | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |
| dataSet    | Array of [SecurityGroupInfo](../shu-ju-jie-gou.md#securitygroupinfo) | SecurityGroup结果集。                          |
| totalCount | Integer                                                              | 符合条件的数据总数。                                 |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
1. **分页查询SecurityGroup列表**

不带任何参数查询所有的SecurityGroup。

```json
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
