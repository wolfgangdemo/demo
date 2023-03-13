# CreateInstances

## 1. 接口描述

调用本接口用于创建一个或多个指定配置的实例。

#### 准备工作

* 查询库存：调用[`DescribeAvailableResources`](../../luo-jin-shu/bmc/describeavailableresources.md)查看指定地区的资源供给情况。
* 查询机型规格：调用[`DescribeInstanceTypes`](../../luo-jin-shu/bmc/describeinstancetypes.md) 可以查询到区域支持的规格信息。
* 查询镜像：调用[`DescribeImages`](../../luo-jin-shu/bmc/describeimages.md)可以查询到镜像信息。
* 成本估算：了解裸机云的的计费方式。更多详情，请参见[计费方式概述](https://docs.console.zenlayer.com/welcome/pricing/bare-metal-cloud-pricing/billing-method)。

{% hint style="info" %}
**注意事项**

* 实例创建成功后将自动开机启动，实例状态变为`RUNNING`(运行中)。
* 预付费实例的购买会预先扣除本次实例购买所需金额，如果余额不足，请求将会失败。后付费实例购买时需要确保账户账号状态正常。
* 调用本接口创建实例，支持代金券自动抵扣，详情请参考代金券选用规则。
* 本接口为异步接口，当创建实例请求下发成功后会返回一个实例`ID`列表，此时创建实例操作并未立即完成。在此期间实例的状态将会处于`PENDING`或`CREATING`，实例创建结果可以通过调用`DescribeInstances` 接口查询，如果实例状态(instanceStatus)由`CREATING`(创建中)或`PENDING`(等待创建）变为`RUNNING`(运行中)，则代表实例创建成功，`CREATE_FAILED`代表实例创建失败，创建过程中不可对实例进行任何操作。
* 单次最多能创建**100**台实例。
{% endhint %}

## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称                    | 必选 | 类型                                                                 | 描述                                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------- | -- | ------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| zoneId                  | 是  | String                                                             | 实例所属的可用区ID。                                                                                                                                                                                                                                                                                                                                                                              |
| instanceChargeType      | 是  | String                                                             | <p>付费类型。</p><p>PREPAID：预付费，即包年包月 POSTPAID：后付费</p>                                                                                                                                                                                                                                                                                                                                        |
| instanceChargePrepaid   | 否  | [ChargePrepaid](../../luo-jin-shu/datastructure.md#chargeprepaid)  | <p>预付费模式。<br>即包年包月相关参数设置。通过该参数可以指定包年包月实例的购买时长等属性。若指定实例的付费模式为预付费则该参数必传。</p>                                                                                                                                                                                                                                                                                                               |
| instanceTypeId          | 是  | String                                                             | <p>实例机型ID。<br>具体取值可通过调用接口DescribeInstanceTypes来获得最新的规格表。</p>                                                                                                                                                                                                                                                                                                                             |
| imageId                 | 否  | String                                                             | <p>指定有效的镜像ID。<br>可通过以下方式获取可用的镜像ID：通过调用接口 <code>DescribeImages</code> ，传入InstanceType获取当前机型支持的镜像列表，取返回信息中的<code>ImageId</code>字段。 也可以不指定镜像，如果不指定镜像，后续可以通过IPMI进行安装。</p>                                                                                                                                                                                                                    |
| resourceGroupId         | 否  | String                                                             | 实例所在的资源组ID。                                                                                                                                                                                                                                                                                                                                                                              |
| instanceName            | 否  | String                                                             | <p>实例显示名称。</p><p>不得超过64个字符。仅支持输入字母、数字、-和英文句点(.)。</p><p>购买多台实例，可以指定模式串<code>[begin_number,bits]</code>。begin_number：有序数值的起始值，取值支持[0,99999]，默认值为0。bits：有序数值所占的位数，取值支持[1,6]，默认值为6。注意模式串中不得有空格。购买1台时，例如<code>server_[3,3]</code>实例显示为<code>server003</code>；购买2台时，实例显示名分别为<code>server003</code>，<code>server004</code>。支持指定多个模式串，如<code>server_[3,3]_[1,1]</code>。</p><p>默认值为 instance。</p> |
| hostname                | 否  | String                                                             | <p>实例的主机名。</p><p>不得超过64个字符。仅支持输入字母、数字、-和英文句点(.) 。</p><p>购买多台实例，可以指定模式串<code>[begin_number,bits]</code>。begin_number：有序数值的起始值，取值支持[0,99999]，默认值为0。bits：有序数值所占的位数，取值支持[1,6]，默认值为6。注意模式串中不得有空格。购买1台时，例如<code>server_[3,3]</code>主机名为<code>server003</code>；购买2台时，实例主机名分别为<code>server003</code>，<code>server004</code>。支持指定多个模式串，如<code>server_[3,3]_[1,1]</code>。</p><p>默认值为hostname。</p>  |
| amount                  | 否  | Integer                                                            | <p>指定创建实例的数量。</p><p>取值范围：1~100。 默认值：1。</p>                                                                                                                                                                                                                                                                                                                                               |
| password                | 否  | String                                                             | <p>实例的密码。</p><p>必须是 8-16 个字符，包含大写字母、小写字母、数字和特殊字符。特殊符号可以是：<code>1~!@$^*-_=+。</code>该密码也是作为IPMI登录的密码。请妥善保管。<br>如果未指定密码，且未设置sshKeys，那么系统将生成一个随机密码并在机器安装成功后发送至创建者的邮箱。</p>                                                                                                                                                                                                                    |
| sshKeys                 | 否  | Array of String                                                    | <p>密钥列表。 </p><p>密钥与密码不能同时指定。 使用了密钥登录，密码登录将会被禁止。 密钥最多支持5个。 Windowsh和exsi操作系统的实例 ，忽略该参数。默认为空。即使填写了该参数，仍旧只执行<code>password</code>的内容。<br><code>如果imageId未指定，则会忽略该参数。</code></p>                                                                                                                                                                                                             |
| internetChargeType      | 是  | String                                                             | <p>网络计费类型。</p><p>取值范围请看<a href="../../luo-jin-shu/datastructure.md#internetchargetype">InternetChargeType</a>。</p>                                                                                                                                                                                                                                                                       |
| internetMaxBandwidthOut | 否  | Integer                                                            | <p>公网出带宽上限。</p><p>单位：Mbps。默认值：1Mbps。不同机型带宽上限范围不一致，具体限制详见购买网络带宽。</p>                                                                                                                                                                                                                                                                                                                      |
| trafficPackageSize      | 否  | Float                                                              | <p>流量包订购大小。</p><p>单位为TB。该值仅限当 <code>internetChargeType</code> = <code>ByTrafficPackage</code> 生效。<br>如果没有传则会默认以赠送的流量包大小</p>                                                                                                                                                                                                                                                              |
| subnetId                | 否  | String                                                             | <p>虚拟子网ID 。</p><p>您可以调用<code>DescribeVpcSubnets</code>查询已创建的交换机的相关信息。</p>                                                                                                                                                                                                                                                                                                                |
| raidConfig              | 否  | [RaidConfig](../../luo-jin-shu/datastructure.md#raidconfig)        | 磁盘阵列配置。                                                                                                                                                                                                                                                                                                                                                                                  |
| partitions              | 否  | Array of [Partition](../../luo-jin-shu/datastructure.md#partition) | <p>分区配置。<br>如果未安装操作系统，将不能设置分区</p>                                                                                                                                                                                                                                                                                                                                                        |
| nic                     | 否  | [Nic](../../luo-jin-shu/datastructure.md#nic)                      | 网卡配置。                                                                                                                                                                                                                                                                                                                                                                                    |



## 3. 响应结果

| 参数名称          | 类型              | 描述                                                                                                                                                                                                                                                                                                          |
| ------------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| instanceIdSet | Array of String | <p>实例ID列表。</p><p>当通过本接口来创建实例时会返回该参数，表示一个或多个实例<code>ID</code>。返回实例<code>ID</code>列表并不代表实例创建成功，可根据 <code>DescribeInstances</code> 接口查询返回的dataSet中对应实例的状态来判断创建是否完成：如果实例状态由<code>CREATING</code>(创建中)或<code>PENDING</code>变为<code>RUNNING</code>(运行中)，则为创建成功；如果实例找不到或状态变为<code>CREATE_FAILED</code>，表示创建失败。</p> |
| orderNumber   | String          | 订单编号。                                                                                                                                                                                                                                                                                                       |
| requestId     | String          | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p>                                                                                                                                                                                                                                                    |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
**1. 用最简单的参数创建一台后付费的实例**\
****在Seoul A创建一台后付费实例，规格为M6C，其带宽计费为固定带宽，密码随机生成，不安装任何镜像，带宽大小为默认的1Mbps。

<pre class="language-json"><code class="lang-json">POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: CreateInstances
&#x3C;Common Request Params>

Request:
<strong>{
</strong>    "instanceChargeType": "POSTPAID",
    "instanceTypeId": "M6C",
    "internetChargeType": "ByBandwidth",
    "zoneId": "SEL-A"
}

Response:
{
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
    "response": {
        "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
        "instanceIdSet": ["instanceId1"],
        "orderNumber" : "orderNumber1"
    }
}
</code></pre>

**2. 创建2台预付费的实例**\
****在Seoul A 创建2台预付费付费实例，规格为M6C，两台实例的名称分别为：SEL-M6C-01, SEL-M6C-02,  密码`Password-12345~`，镜像ID: 5ace1756-2230-4d1d-8fc6-84f1897ef397，指定了公网和内网网卡名称wan0和lan0,  带宽计费为固定带宽，带宽大小为10Mbps。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: CreateInstances
<Common Request Params>

Request:
{
    "instanceChargeType": "PREPAID",
    "amount": 2, 
    "instanceChargePrepaid":{
        "period": 2
    },
    "instanceName": "SEL-M6C-[1,2]",
    "hostname": "SEL-M6C-[1,2]",
    "internetMaxBandwidthOut": 10,
    "password": "Password-12345~",
    "nic": {
        "wanName": "wan0",
        "lanName": "lan0"
    },
    "instanceTypeId": "M6C",
    "internetChargeType": "ByBandwidth",
    "zoneId": "SEL-A", 
    "imageId": "5ace1756-2230-4d1d-8fc6-84f1897ef397"
}

Response:
{
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D4",
    "response": {
        "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D4",
        "instanceIdSet": ["instanceId3", "instanceId4"],
        "orderNumber" : "orderNumber2"
    }
}
```

**3. 创建2台预付费的实例，其网络计费方式为流量包**\
****和2类似， 不同的是本次创建的网络计费方式是流量包， 其流量包大小为 10TB。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: CreateInstances
<Common Request Params>

Request:
{
    "instanceChargeType": "PREPAID",
    "amount": 2, 
    "instanceChargePrepaid":{
        "period": 2
    },
    "instanceName": "SEL-M6C-[1,2]",
    "hostname": "SEL-M6C-[1,2]",
    "internetMaxBandwidthOut": 10,
    "password": "Password-12345~",
    "nic": {
        "wanName": "wan0",
        "lanName": "lan0"
    },
    "instanceTypeId": "M6C",
    "internetChargeType": "ByBandwidth",
    "zoneId": "SEL-A", 
    "imageId": "5ace1756-2230-4d1d-8fc6-84f1897ef397",
    "trafficPackageSize": 10 
}

Response:
{
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D4",
    "response": {
        "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D4",
        "instanceIdSet": ["instanceId5", "instanceId6"],
        "orderNumber" : "orderNumber3"
    }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                                    | 说明                                            |
| ------- | ------------------------------------------------------ | --------------------------------------------- |
| 400     | INVALID\_PARAMETER\_HOSTNAME\_EXCEED                   | 参数hostname超过了长度限制，请注意模式串中的bits总和不要超过指定长度。     |
| 400     | INVALID\_PARAMETER\_HOSTNAME\_MALFORMED                | 参数hostname格式不正确，请注意输入值在规定的字符内。                |
| 400     | INVALID\_PARAMETER\_INSTANCE\_NAME\_EXCEED             | 参数instanceName超过了长度限制，请注意模式串中的bits总和不要超过指定长度。 |
| 400     | INVALID\_PARAMETER\_INSTANCE\_NAME\_EXCEED             | 参数instanceName格式不正确，请注意输入值在规定的字符内。            |
| 403     | OPERATION\_FILED\_INTERNET\_CHARGE\_TYPE\_NOT\_SUPPORT | 指定的网络计费类型在当前区域不支持。                            |
| 404     | INVALID\_IMAGE\_NOT\_FOUND                             | 未找到指定的镜像。                                     |
| 404     | INVALID\_ZONE\_NOT\_FOUND                              | 指定的可用区不存在。                                    |
| 404     | INVALID\_INSTANCE\_TYPE\_NOT\_FOUND                    | 未找到指定的实例规格。                                   |
| 403     | INVALID\_PARTITION\_IMAGE\_NOT\_SET                    | 自定义分区必须指定操作系统才可以进行。                           |
| 403     | OPERATION\_DENIED\_INSTANCE\_QUOTA\_EXCEED             | 机器创建数量超过了当前Team的总配额。                          |
| 400     | INVALID\_BANDWIDTH\_VALUE\_EXCEED\_MAXIMUM             | 指定的带宽大小超过了机型允许的最大范围限制。                        |
| 400     | INVALID\_PARAMETER\_VALUE\_PASSWORD\_MALFORMED         | 无效密码。指定的密码不符合密码复杂度限制。例如密码长度不符合限制等。            |
| 400     | INVALID\_PARAMETER\_INSTANCE\_LOGIN\_CONFLICT          | 不能同时指定密码登录和SSH Key登录。                         |
| 400     | INVALID\_PARAMETER\_SSH\_KEY\_MALFORMED                | 输入的ssh key格式不正确，一般以rsa开头。                     |
| 400     | INVALID\_RAID\_CONFIG\_FAST\_CUSTOM\_CONFLICT          | 自定义raid和快速raid只能选择其中一种。                       |
| 400     | INVALID\_INSTANCE\_TYPE\_RAID\_NOT\_SUPPORT            | 当前机型不支持指定的raid级别。                             |
| 400     | INVALID\_PARAMETER\_NIC\_NAME\_CONFLICT                | 公网网卡名称和内网网卡不能相同。                              |
| 400     | INVALID\_PARAMETER\_NIC\_NAME\_MALFORMED               | 公网网卡或内网网卡名称不符合规范，请注意字符是否在规定的范围内。              |
| 400     | INVALID\_PARTITION\_SIZE\_NOT\_FULL                    | 分区大小没有到达应分区的规定容量。                             |
| 400     | INVALID\_PARTITION\_DUPLICATE\_FILE\_PATH              | 分区的文件路径或盘符有重复。                                |
| 400     | INVALID\_PARTITION\_MISSING\_REQUIRED\_FILE\_PATH      | 分区时缺少必须的文件路径（盘符），windos必须包含c，linux必须包含/。      |
| 400     | INVALID\_PARTITION\_MALFORMED                          | 分区文件类型或路径有格式问题。                               |
| 400     | INVALID\_PARTITION\_NO\_TYPE                           | 分区文件类型错误。                                     |
| 400     | INVALID\_PARTITION\_INVALID\_ORDER                     | windows 分区时盘符必须按字母顺序以此填写，比如CDEFG。             |
| 400     | INVALID\_PARAMETER\_VALUE\_RAID\_DISK\_MISMATCH        | 自定义raid配置时传的硬盘数量和Raid等级所要求的硬盘数量不匹配。           |
| 400     | INVALID\_PARAMETER\_VALUE\_RAID\_DISK\_DISORDER        | 自定义raid配置时硬盘的序号必须按顺序填写，比如\[1,2,3]。            |
| 400     | RESOURCE\_INSUFFICIENT\_PRODUCT\_SOLD\_OUT             | 所选资源未售卖。                                      |
| 403     | OPERATION\_DENIED\_CHARGE\_TYPE\_NOT\_SUPPORT          | 该区域所选择的付费类型不支持。                               |
| 400     | RESOURCES\_SOLDOUT\_INSTANCE\_TYPE                     | 指定的实例机型已售罄。                                   |

##
