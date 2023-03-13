# ReinstallInstance

## 1. 接口描述

本接口用于重装一个实例。

#### 准备工作

* 查询镜像：调用`DescribeImages`可以查询到镜像信息。

{% hint style="info" %}
**注意事项**

* 如果指定了`imageId`参数，则使用指定的镜像重装；否则按照实例当前使用的镜像进行重装。
* 在回收站中或者正在安装中的实例不支持该操作。
* 系统盘将会被格式化并重置，请确保系统盘中无重要文件。
* 如果密码不指定将会通过邮箱下发随机密码。
* 重装实例后进入`INSTALLING`(安装中)的状态。如果实例的最新状态变为`RUNNING`(运行中)，则代表操作成功；如果实例的状态为`INSTALL_FAILED`，则代表安装失败。如果出现安装失败，请联系Support进行解决。实例的状态可以通过调用 `DescribeInstances` 接口查询。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称       | 必选 | 类型                                                  | 描述                                                                                                                                                                       |
| ---------- | -- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| instanceId | 是  | String                                              | <p>待操作的实例ID。</p><p>可通过<code>DescribeInstances</code>接口返回值中的<code>instanceId</code>获取。</p>                                                                                |
| imageId    | 否  | String                                              | <p>指定有效的镜像ID。<br>可通过以下方式获取可用的镜像ID：通过调用接口 <code>DescribeImages</code> ，传入instanceTypeId获取当前机型支持的镜像列表，取返回信息中的<code>imageId</code>字段；也可以不指定镜像，如果不指定镜像，后续可以通过IPMI进行安装。</p>   |
| hostname   | 否  | String                                              | <p>实例的主机名。</p><p>不得超过64个字符。仅支持输入字母、数字、-和英文句点(.)。</p><p>默认值为hostname。</p>                                                                                                 |
| password   | 否  | String                                              | <p>实例的密码。</p><p>必须是 8-16 个字符，包含大写字母、小写字母、数字和特殊字符。特殊符号可以是：<code>1~!@$^*-_=+。</code>该密码也是作为IPMI登录的密码，请妥善保管。<br>如果未指定密码，且未设置sshKeys，那么系统将生成一个随机密码并在机器安装成功后发送至创建者的邮箱。</p>    |
| sshKeys    | 否  | Array of String                                     | <p>密钥列表。</p><p>密钥与密码不能同时指定。 使用了密钥登录，密码登录将会被禁止。 密钥最多支持5个。 Windowsh和exsi操作系统的实例 ，忽略该参数。默认为空。即使填写了该参数，仍旧只执行<code>password</code>的内容。 如果<code>imageId</code>未指定，则会忽略该参数。</p> |
| raidConfig | 否  | [RaidConfig](../datastructure.md#raidconfig)        | 磁盘阵列配置。                                                                                                                                                                  |
| partitions | 否  | Array of [Partition](../datastructure.md#partition) | <p>分区配置。</p><p>如果未安装操作系统，将不能设置分区。</p>                                                                                                                                    |
| nic        | 否  | [Nic](../datastructure.md#nic)                      | 网卡配置。                                                                                                                                                                    |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                         |
| --------- | ------ | ------------------------------------------ |
| requestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 requestId。 |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1.默认重装指定ID的实例**

用默认值重装ID为`instanceId`的实例。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: ReinstallInstance
<Common Request Params>

Request：
{
    "instanceId": "instanceId"
}

Response:
{
  "requestId": "TC1748D3E-452D-4F74-8485-7AA73718E453",
  "response": {
    "requestId": "TC1748D3E-452D-4F74-8485-7AA73718E453"
  }
}
```



**2.自定义重装指定ID的实例**

重装ID为`instanceId`的实例，并且指定了镜像为`bd5faa16-39d2-4bbf-a5c8-b95a193b1626`，hostname为`myhostname`，密码为`Aa_12345`，磁盘阵列配置为raid0，并且进行两个分区，公网网卡名称配置为`wan0`，内网网卡名称配置为`lan0`。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-TC-Action: ReinstallInstance
<Common Request Params>

Request：
{
    "instanceId": "instanceId",
    "imageId": "bd5faa16-39d2-4bbf-a5c8-b95a193b1626",
    "hostname": "myhostname",
    "password": "Aa_12345"
    "raidConfig": {
        raidType": 0
    },
    "partitions": [
        {
            "fsPath": "/",
            "fsType": "ext2",
            "size": 1100
        },
        {
            "fsPath": "/a",
            "fsType": "ext2",
            "size": 1100
        }
    ],
    "nic": {
        "wanName": "wan0",
        "lanName": "lan0"
    }
}

Response:
{
  "requestId": "TC1748D3E-452D-4F74-8485-7AA73718E453",
  "response": {
    "requestId": "TC1748D3E-452D-4F74-8485-7AA73718E453"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                               | 说明                                            |
| ------- | ------------------------------------------------- | --------------------------------------------- |
| 400     | INVALID\_PARAMETER\_HOSTNAME\_EXCEED              | 参数hostname超过了长度限制，请注意模式串中的bits总和不要超过指定长度。     |
| 400     | INVALID\_PARAMETER\_HOSTNAME\_MALFORMED           | 参数hostname格式不正确，请注意输入值在规定的字符内。                |
| 400     | INVALID\_PARAMETER\_INSTANCE\_NAME\_EXCEED        | 参数instanceName超过了长度限制，请注意模式串中的bits总和不要超过指定长度。 |
| 400     | INVALID\_PARAMETER\_INSTANCE\_NAME\_EXCEED        | 参数instanceName格式不正确，请注意输入值在规定的字符内。            |
| 404     | INVALID\_INSTANCE\_NOT\_FOUND                     | 指定的实例不存在。                                     |
| 404     | INVALID\_IMAGE\_NOT\_FOUND                        | 未找到指定的镜像。                                     |
| 403     | INVALID\_PARTITION\_IMAGE\_NOT\_SET               | 自定义分区必须指定操作系统才可以进行。                           |
| 400     | INVALID\_PARAMETER\_VALUE\_PASSWORD\_MALFORMED    | 无效密码。指定的密码不符合密码复杂度限制。例如密码长度不符合限制等。            |
| 400     | INVALID\_PARAMETER\_INSTANCE\_LOGIN\_CONFLICT     | 不能同时指定密码登录和SSH Key登录。                         |
| 400     | INVALID\_PARAMETER\_SSH\_KEY\_MALFORMED           | 输入的ssh key格式不正确，一般以rsa开头。                     |
| 400     | INVALID\_RAID\_CONFIG\_FAST\_CUSTOM\_CONFLICT     | 自定义raid和快速raid只能选择其中一种。                       |
| 400     | INVALID\_INSTANCE\_TYPE\_RAID\_NOT\_SUPPORT       | 当前机型不支持指定的raid级别。                             |
| 400     | INVALID\_PARAMETER\_NIC\_NAME\_CONFLICT           | 公网网卡名称和内网网卡不能相同。                              |
| 400     | INVALID\_PARAMETER\_NIC\_NAME\_MALFORMED          | 公网网卡或内网网卡名称不符合规范，请注意字符是否在规定的范围内。              |
| 400     | INVALID\_PARTITION\_SIZE\_NOT\_FULL               | 分区大小没有到达应分区的规定容量。                             |
| 400     | INVALID\_PARTITION\_DUPLICATE\_FILE\_PATH         | 分区的文件路径或盘符有重复。                                |
| 400     | INVALID\_PARTITION\_MISSING\_REQUIRED\_FILE\_PATH | 分区时缺少必须的文件路径（盘符），windos必须包含c，linux必须包含/。      |
| 400     | INVALID\_PARTITION\_MALFORMED                     | 分区文件类型或路径有格式问题。                               |
| 400     | INVALID\_PARTITION\_NO\_TYPE                      | 分区文件类型错误。                                     |
| 400     | INVALID\_PARTITION\_INVALID\_ORDER                | windows 分区时盘符必须按字母顺序以此填写，比如CDEFG。             |
| 400     | INVALID\_PARAMETER\_VALUE\_RAID\_DISK\_MISMATCH   | 自定义raid配置时传的硬盘数量和Raid等级所要求的硬盘数量不匹配。           |
| 400     | INVALID\_PARAMETER\_VALUE\_RAID\_DISK\_DISORDER   | 自定义raid配置时硬盘的序号必须按顺序填写，比如\[1,2,3]。            |

