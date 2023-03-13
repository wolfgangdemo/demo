# 数据结构

## RegionInfo

| 名称         | 类型     | 描述    |
| ---------- | ------ | ----- |
| regionId   | String | 区域ID。 |
| regionName | String | 区域名称。 |

## ImageInfo

镜像相关信息。

| 名称               | 类型     | 描述                                                                                              |
| ---------------- | ------ | ----------------------------------------------------------------------------------------------- |
| imageId          | String | 镜像ID。                                                                                           |
| imageName        | String | 镜像名称。                                                                                           |
| imageType        | String | <p>镜像类型。</p><ul><li>PUBLIC_IMAGE-公共镜像。</li><li>CUSTOM_IMAGE-自定义镜像。</li></ul>                    |
| imageSize        | String | 镜像大小，单位为GB。                                                                                     |
| imageDescription | String | 镜像描述。                                                                                           |
| imageVersion     | String | 镜像版本。                                                                                           |
| imageStatus      | String | <p>镜像状态。</p><ul><li>CREATING-创建中。</li><li>AVAILABLE-可用。</li><li>UNAVAILABLE-不可用。</li></ul>      |
| category         | String | <p>镜像所属分类。</p><p>可能值：</p><ul><li>CentOS</li><li>Windows</li><li>Ubuntu</li><li>Debian</li></ul> |
| osType           | String | <p>操作系统类型。</p><p>可能值：</p><ul><li>windows</li><li>linux</li></ul>                                |
| regionId         | String | 区域ID。                                                                                           |

## ImageQuotaInfo

镜像的区域信息

| 名称       | 类型      | 描述            |
| -------- | ------- | ------------- |
| regionId | String  | 支持创建镜像的区域。    |
| count    | Integer | 当前已配置镜像数。     |
| maxCount | Integer | 本区域可配置的最大镜像数。 |

## DiskInfo

云硬盘信息

| 名称           | 类型                                                                                                                                    | 描述                                                           |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| diskId       | String                                                                                                                                | 云硬盘ID。                                                       |
| diskName     | String                                                                                                                                | 云硬盘名称。                                                       |
| regionId     | Integer                                                                                                                               | 云硬盘所属区域。                                                     |
| diskType     | String                                                                                                                                | <p>云硬盘类型。</p><ul><li>System-系统盘。</li><li>Data-数据盘。</li></ul> |
| portable     | Boolean                                                                                                                               | 是否可拔插。                                                       |
| diskCategory | String                                                                                                                                | <p>磁盘种类。</p><ul><li>cloud_efficiency-⾼效云盘。</li></ul>         |
| diskSize     | Integer                                                                                                                               | 云硬盘大小，单位GB。                                                  |
| diskStatus   | [diskstatus](https://app.gitbook.com/o/Rd15U4uRjRmyN7R1SiQh/s/q4kkSWfFMDdA8LtynnfE/\~/changes/236/xu-ni-ji/shu-ju-jie-gou#diskstatus) | 云硬盘状态。                                                       |
| instanceId   | String                                                                                                                                | 所绑定的实例ID。                                                    |
| instanceName | String                                                                                                                                | 所绑定的实例名字。                                                    |
| chargeType   | String                                                                                                                                | <p>付费类型。<br>prepaid-预付费。<br>postpaid-后付费。</p>                |
| createTime   | Timestamp                                                                                                                             | <p>创建时间。</p><p>格式为：<code>YYYY-MM-DDThh:mm:ssZ</code>。</p>    |
| expiredTime  | Timestamp                                                                                                                             | <p>到期时间。</p><p>格式为：<code>YYYY-MM-DDThh:mm:ssZ</code>。</p>    |
| period       | Integer                                                                                                                               | <p>购买实例的时长。</p><p>单位：月。</p><p>后付费实例该字段为null。</p>             |

## DiskStatus

| 状态值         | 状态说明 |
| ----------- | ---- |
| To\_product | 待创建  |
| Creating    | 创建中  |
| Available   | 待挂载  |
| Attaching   | 挂载中  |
| Detaching   | 卸载中  |
| In\_use     | 使⽤中  |
| Deleting    | 释放中  |



### SecurityGroupInfo

SecurityGroup Info信息。

| 名称                  | 类型                                              | 描述                                                        |
| ------------------- | ----------------------------------------------- | --------------------------------------------------------- |
| securityGroupId     | String                                          | securityGroup唯一ID。                                        |
| securityGroupName   | String                                          | securityGroup名称。                                          |
| securityGroupStatus | String                                          | [securityGroup状态。](shu-ju-jie-gou.md#securitygroupstatus) |
| createTime          | Timestamp                                       | <p>创建时间。</p><p>格式为：<code>YYYY-MM-DDThh:mm:ssZ</code>。</p> |
| instanceIds         | Array of String                                 | 已绑定的实例ID集合。                                               |
| ingressRuleInfos    | Array of [RuleInfo](shu-ju-jie-gou.md#ruleinfo) | 入方向规则集合。                                                  |
| egressRuleInfos     | Array of [RuleInfo](shu-ju-jie-gou.md#ruleinfo) | 出方向规则集合。                                                  |



### SecurityGroupStatus

| 状态值            | 状态说明 |
| -------------- | ---- |
| AVAILABLE      | 可用   |
| CREATE\_FAILED | 创建失败 |
|                |      |



### RuleInfo

Rule Info信息。

| 名称           | 类型      | 描述                                                                                                                                                                                                                                                                                             |
| ------------ | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ruleId       | Integer | 规则ID。                                                                                                                                                                                                                                                                                          |
| direction    | String  | <p>规则方向。取值：</p><ul><li><strong>ingress</strong>：入方向。</li><li><strong>egress</strong>：出方向。</li></ul><p>默认值：<strong>ingress</strong>。</p>                                                                                                                                                        |
| policy       | String  | <p>设置访问权限。取值：</p><ul><li><strong>accept</strong>：接受访问。</li><li><strong>drop</strong>：拒绝访问，不返回拒绝信息。</li></ul><p>默认值：<strong>accept</strong>。</p>                                                                                                                                                |
| priority     | Integer | <p>安全组规则优先级。取值范围：<strong>1</strong>~<strong>100</strong>，数值越小，代表优先级越高。</p><p>默认值：<strong>1</strong>。</p>                                                                                                                                                                                       |
| ipProtocol   | String  | <p>传输层协议。取值大小写敏感。取值范围：</p><ul><li>tcp</li><li>udp</li><li>icmp</li><li>all：支持所有协议</li></ul>                                                                                                                                                                                                    |
| portRange    | String  | <p>目的端安全组开放的传输层协议相关的端口范围。取值范围：</p><ul><li>TCP/UDP协议：取值范围为<strong>1</strong>~<strong>65535</strong>。使用斜线（/）隔开起始端口和终止端口。正确示范：<strong>1/200</strong>；错误示范：<strong>200/1</strong>。</li><li>ICMP协议：<strong>-1/-1</strong>。</li><li><p>IpProtocol取值为</p><p>all：<strong>-1/-1。</strong></p></li></ul> |
| sourceCidrIp | String  | 目的端IP地址范围。支持CIDR格式和IPv4格式的IP地址范围。                                                                                                                                                                                                                                                              |



### InstanceAvailableSecurityGroup

| 名称                | 类型     | 描述                |
| ----------------- | ------ | ----------------- |
| securityGroupId   | String | SecurityGroup ID。 |
| securityGroupName | String | SecurityGroup的名称。 |

