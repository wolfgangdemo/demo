# 数据结构

## ChargePrepaid

描述预付费模式，即包年包月相关参数。包括购买时长等逻辑。

| 名称     | 类型      | 必选 | 描述                          |
| ------ | ------- | -- | --------------------------- |
| period | Integer | 是  | <p>购买实例的时长。</p><p>单位：月。</p> |

## RaidConfig

实例磁盘阵列配置， 包括自定义raid的配置。

| 名称          | 类型                                                 | 必选 | 描述                                                                                |
| ----------- | -------------------------------------------------- | -- | --------------------------------------------------------------------------------- |
| raidType    | Integer                                            | 否  | <p>Raid类型。<br>该配置进行快捷raid配置，支持0, 1, 5, 10。<br>raidType和customRaids只能指定其中一个参数。</p> |
| customRaids | Array of [CustomRaid](datastructure.md#customraid) | 否  | <p>自定义Raid配置。<br>自定义磁盘进行raid的配置。<br>raidType和customRaids只能指定其中一个参数。</p>           |

## CustomRaid

进行自定义Raid配置时需要的raid级别和指定的磁盘序号。

| 名称           | 类型               | 必选 | 描述                                                |
| ------------ | ---------------- | -- | ------------------------------------------------- |
| raidType     | Integer          | 是  | <p>Raid类型。<br>支持0, 1, 5, 10。</p>                  |
| diskSequence | Array of Integer | 是  | <p>磁盘序号。<br>根据机型里的磁盘从1开始顺序编号。如果是多个磁盘序号，则必须连续。</p> |

## Partition

分区配置信息。包括文件类型, 分区大小等。

| 名称     | 类型      | 必选 | 描述                                                                                      |
| ------ | ------- | -- | --------------------------------------------------------------------------------------- |
| fsType | Integer | 是  | <p>分区的文件类型。</p><p>linux系统：支持的值ext2,ext3, ext4, ext类型必须要有。</p><p>windows系统: 只能为NTFS。</p> |
| fsPath | String  | 是  | <p>分区盘符。</p><p>linux系统：必须为/开头，且第一个为系统分区必须为/。</p><p>windows系统：支持C~H，第一个系统分区必须指定为C。</p>   |
| size   | Integer | 是  | <p>分区大小。<br>单位为GB。</p>                                                                  |

## Nic

网卡的相关配置，目前包括公网和内网的网卡名称。

| 名称      | 类型     | 必选 | 描述                                                                                                                                   |
| ------- | ------ | -- | ------------------------------------------------------------------------------------------------------------------------------------ |
| wanName | String | 否  | <p>公网网卡名称。<br>只能是数字和大小写字母，且必须以字母开头，长度限制为4-10。<br>非高可用机型，默认的公网网卡名称为wan0。且不能为lan开头。<br>高可用机型，默认的公网网卡名称为bond0。<br>公网名称和内网名称不能相同。</p>    |
| lanName | String | 否  | <p>内网网卡名称。<br>只能是数字和大小写字母，且必须以字母开头，长度限制为4-10。<br>非高可用机型，默认的内网网卡名称为lan0。且不能包含wan或lan。<br>高可用机型，默认的内网网卡名称为bond1。<br>公网名称和内网名称不能相同。</p> |

## InstanceType

机型的配置信息。包括机型的cpu、内存、是否支持组内网等等。&#x20;

| 参数名称             | 类型                                                    | 描述                                 |
| ---------------- | ----------------------------------------------------- | ---------------------------------- |
| instanceTypeId   | String                                                | 实例机型ID。                            |
| description      | String                                                | <p>机型描述。</p><p>一般包括内存大小，硬盘。</p>    |
| cpuCoreCount     | Integer                                               | CPU内核数目。                           |
| memorySize       | Integer                                               | <p>内存大小。</p><p>单位：GB。</p>          |
| supportRaids     | Array of Integer                                      | 机型支持的raid。                         |
| supportSubnet    | Boolean                                               | 是否支持内网组网。                          |
| maximumBandwidth | Integer                                               | <p>机型支持的最大出口带宽。</p><p>单位：Mbps。</p> |
| diskInfo         | [InstanceDiskInfo](datastructure.md#instancediskinfo) | <p>硬盘配置。</p><p>单位：GB。</p>          |
| imageIds         | Array of String                                       | 机型支持的镜像ID。                         |

## InstanceDiskInfo

机型硬盘信息。

| 参数名称            | 类型                                     | 描述                                                                                                        |
| --------------- | -------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| totalDiskSize   | Integer                                | <p>机型的硬盘总大小。<br>单位：GB。<br>totalDiskSize的大小一般小于描述的信息，系统为了分区能够成功预留了一小部分。如果采用自定义分区，最后的一个分区将会获得剩余的所有磁盘大小。</p> |
| diskDescription | String                                 | 机型硬盘的描述信息。                                                                                                |
| disks           | Array of [Disk](datastructure.md#disk) | <p>可用于raid和分区的磁盘信息。<br>按顺序标号。比如880 x 2、 220 x2，其磁盘序号1,2,3,4 分别对应的磁盘大小为880，880，220，220。</p>                |

## AvailableResource

可售卖的实例资源信息。描述了哪些可用区有哪些机型可以售卖。

| 参数名称                      | 类型              | 描述                                                                                                                        |
| ------------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------- |
| zoneId                    | String          | 可用区ID。                                                                                                                    |
| sellStatus                | String          | <p>售卖的状态。</p><ul><li>SELL：表示实例可购买，且库存>10。</li><li>SELL_SHORTAGE: 表示可购买，但是库存&#x3C;10台。</li><li>SOLD_OUT：表示实例已售罄。</li></ul> |
| internetChargeTypes       | Array of String | <p>网络计费类型。</p><p>取值范围请看<a href="datastructure.md#internetchargetype">InternetChargeType</a>。</p>                          |
| instanceTypeId            | String          | 机型ID。                                                                                                                     |
| maximumBandwidthOut       | Integer         | <p>最大的公网出口带宽限制。<br>单位：Mbps。</p>                                                                                           |
| defaultBandwidthOut       | Integer         | <p>固定带宽计费方式时默认赠送公网带宽。<br>单位：GB。</p>                                                                                       |
| defaultTrafficPackageSize | Float           | <p>流量包计费方式时默认增送的流量包大小。<br>单位：TB。</p>                                                                                      |

## Disk

硬盘块信息。

| 参数名称      | 类型      | 描述                      |
| --------- | ------- | ----------------------- |
| diskSize  | Integer | <p>硬盘的大小。<br>单位：GB。</p> |
| diskCount | Integer | 该硬盘大小的硬盘的数量。            |

## InstanceStatus

实例状态。

| 状态值             | 状态说明  |
| --------------- | ----- |
| PENDING         | 待创建   |
| CREATING        | 创建中   |
| CREATE\_FAILED  | 创建失败  |
| INSTALLING      | 安装中   |
| INSTALL\_FAILED | 安装失败  |
| RUNNING         | 运行中   |
| STOPPED         | 关机    |
| BOOTING         | 启动中   |
| STOPPING        | 关机中   |
| RECYCLE         | 在回收站中 |

## InternetChargeType

网络计费类型。

| 类型                    | 说明       |
| --------------------- | -------- |
| ByBandwidth           | 按固定带宽计费  |
| ByTrafficPackage      | 购买流量包计费  |
| ByInstanceBandwidth95 | 单个实例95计费 |
| ByClusterBandwidth95  | 合并95计费   |

## EipAddress

Eip信息。

| 参数名称              | 类型        | 描述                                                                                                                                 |
| ----------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| eipId             | String    | EIP唯一ID。                                                                                                                           |
| zoneId            | String    | EIP所属的可用区ID。                                                                                                                       |
| ipAddress         | String    | IP地址。                                                                                                                              |
| instanceId        | String    | 实例ID。                                                                                                                              |
| instanceName      | String    | 实例名称。                                                                                                                              |
| eipChargeType     | String    | <p>付费类型。</p><p>PREPAID：预付费，即包年包月。POSTPAID：后付费。</p>                                                                                 |
| period            | Integer   | <p>购买EIP的时长。</p><p>单位：月。</p><p>后付费EIP该字段为null。</p>                                                                                 |
| createTime        | Timestamp | <p>创建时间。</p><p>按照<code>ISO8601</code>标准表示，并且使用<code>UTC</code>时间。格式为：<code>YYYY-MM-DDThh:mm:ssZ。</code></p>                        |
| expiredTime       | Timestamp | <p>到期时间。</p><p>按照<code>ISO8601</code>标准表示，并且使用<code>UTC</code>时间。格式为：<code>YYYY-MM-ddThh:mm:ssZ</code>。</p><p>注意：后付费模式本项为null。</p> |
| eipStatus         | String    | [EIP状态](datastructure.md#eipstatus)。                                                                                               |
| resourceGroupId   | String    | 资源组ID。                                                                                                                             |
| resourceGroupName | String    | 资源组名称。                                                                                                                             |

## EipAvailable

购买EIP资源区域。

| 名称     | 类型     | 描述                                                                                                                                         |
| ------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| zoneId | String | EIP所属的可用区ID。                                                                                                                               |
| status | String | <p>EIP是否售卖。</p><p>取值范围：</p><ul><li>SELL：表示EIP可购买，且库存>10台。</li><li>SELL_SHORTAGE: 表示可购买，但是库存&#x3C;10台。</li><li>SOLD_OUT：表示EIP已售罄。</li></ul> |

## InstanceAvailableEip

EIP信息。

| 名称        | 类型     | 描述                                                                                      |
| --------- | ------ | --------------------------------------------------------------------------------------- |
| eipId     | String | <p>一个EIP ID。</p><p>可通过<code>DescribeEipAddresses</code>接口返回值中的<code>eipId</code>获取。</p> |
| ipAddress | String | IP地址。                                                                                   |

## DdosIpAddress

Ddos IP信息。

| 参数名称              | 类型        | 描述                                                                                                                                 |
| ----------------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| ddosIpId          | String    | Ddos IP唯一ID。                                                                                                                       |
| zoneId            | String    | Ddos IP所属的可用区ID。                                                                                                                   |
| ipAddress         | String    | IP地址。                                                                                                                              |
| instanceId        | String    | 实例ID。                                                                                                                              |
| instanceName      | String    | 实例名称。                                                                                                                              |
| ddosIpChargeType  | String    | <p>付费类型。</p><p>PREPAID：预付费，即包年包月。 POSTPAID：后付费。</p>                                                                                |
| period            | Integer   | <p>购买Ddos IP的时长。</p><p>单位：月。</p><p>后付费Ddos IP该字段为null。</p>                                                                         |
| createTime        | Timestamp | <p>创建时间。</p><p>按照<code>ISO8601</code>标准表示，并且使用<code>UTC</code>时间。格式为：<code>YYYY-MM-DDThh:mm:ssZ。</code></p>                        |
| expiredTime       | Timestamp | <p>到期时间。</p><p>按照<code>ISO8601</code>标准表示，并且使用<code>UTC</code>时间。格式为：<code>YYYY-MM-ddThh:mm:ssZ</code>。</p><p>注意：后付费模式本项为null。</p> |
| ddosIpStatus      | String    | [Ddos IP状态](datastructure.md#ddosipstatus)。                                                                                        |
| resourceGroupId   | String    | 资源组ID。                                                                                                                             |
| resourceGroupName | String    | 资源组名称。                                                                                                                             |

## DdosIpAvailable

购买Ddos IP资源区域。

| 名称     | 类型     | 描述                                                                                                                                                     |
| ------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| zoneId | String | Ddos IP所属的可用区ID。                                                                                                                                       |
| status | String | <p>Ddos IP是否售卖。</p><p>取值范围：</p><ul><li>SELL：表示Ddos IP可购买，且库存>10台。</li><li>SELL_SHORTAGE: 表示可购买，但是库存&#x3C;10台。</li><li>SOLD_OUT：表示Ddos IP已售罄。</li></ul> |

## InstanceAvailableDdosIp

Ddos IP信息。

| 名称        | 类型     |                                                                                                   |
| --------- | ------ | ------------------------------------------------------------------------------------------------- |
| ddosIpId  | String | <p>一个Ddos IP ID。</p><p>可通过<code>DescribeDdosIpAddresses</code>接口返回值中的<code>ddosIpId</code>获取。</p> |
| ipAddress | String | IP地址。                                                                                             |

## Price

价格。描述了购买资源的预付费或后付费价格信息。

| 名称                | 类型                                               | 描述                                                                                                                |
| ----------------- | ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| OriginalPrice     | Float                                            | <p>预付费的原价。</p><p>预付费模式使用，后付费该值为 null。</p>                                                                         |
| discountPrice     | Float                                            | <p>预付费的折扣价。</p><p>预付费模式使用，后付费该值为 null。</p>                                                                        |
| discount          | Float                                            | <p>折扣大小。<br>如80.0代表8折。</p>                                                                                        |
| unitPrice         | Float                                            | <p>后付费的单元原始价格。<br>后付费模式使用，如果价格为阶梯价格，该项为null。</p>                                                                  |
| discountUnitPrice | Float                                            | <p>后付费的单元折后价格。</p><p>后付费模式使用，如果价格为阶梯价格，该项为null。</p>                                                               |
| chargeUnit        | String                                           | <p>后付费计价单元。<br>后付费模式使用，可取值范围：<br>HOUR: 表示计价单元是按每小时来计算。<br>DAY: 表示计价单元是按天来计算。<br>MONTH: 表示计价单元是按月来计算，95计费则是这种。</p> |
| stepPrices        | Array of [StepPrice](datastructure.md#stepprice) | <p>后付费阶梯价格。<br>后付费模式使用，如果非阶梯价格，该项为null。</p>                                                                       |

## StepPrice

后付费阶梯价格。描述了价格的一个阶梯的信息。

| 名称                | 类型    | 描述                              |
| ----------------- | ----- | ------------------------------- |
| stepStart         | Float | 阶梯用量的开始。                        |
| stepEnd           | Float | 阶梯用量的结束。                        |
| unitPrice         | Float | <p>当前阶梯的单元原始价格。<br>后付费模式使用。</p> |
| discountUnitPrice | Float | <p>当前阶梯的单元折后价格。<br>后付费模式使用。</p> |



## ImageInfo

镜像相关信息。

| 名称        | 类型     | 描述                                                                                                           |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------ |
| imageId   | String | 镜像ID。                                                                                                        |
| imageName | String | 镜像名称。                                                                                                        |
| catalog   | String | <p>镜像所属分类。</p><p>可能值：</p><ul><li>centos</li><li>windows</li><li>ubuntu</li><li>debian</li><li>esxi</li></ul> |
| imageType | String | <p>镜像类型。</p><p>PUBLIC_IMAGE: 公共镜像。</p><p>CUSTOM_IMAGE：自定义镜像。</p><p>目前不支持自主的创建自定义镜像，可联系support沟通。</p>         |
| osType    | String | <p>操作系统类型。</p><p>可能值：</p><ul><li>windows</li><li>linux</li></ul>                                             |

## InstanceInfo

实例相关信息。

| 名称                     | 类型                                               | 描述                                                                                               |
| ---------------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| instanceId             | String                                           | 实例唯一ID。                                                                                          |
| zoneId                 | String                                           | 实例所属的可用区ID。                                                                                      |
| instanceName           | String                                           | 实例显示名称。                                                                                          |
| hostname               | String                                           | 实例的主机名。                                                                                          |
| instanceTypeId         | String                                           | 实例机型ID。                                                                                          |
| imageId                | String                                           | 镜像ID。                                                                                            |
| imageName              | String                                           | 镜像名称。                                                                                            |
| instanceChargeType     | String                                           | <p>实例计费类型。</p><p>PREPAID：预付费，即包年包月。 POSTPAID：后付费。</p>                                            |
| bandwidthOutMbps       | Integer                                          | <p>公网出口带宽。</p><p>单位：Mbps。</p><p>0 代表无限制，但是不会超过机型的最大上限。</p>                                       |
| internetChargeType     | String                                           | <p>网络计费类型。</p><p>取值范围请看<a href="datastructure.md#internetchargetype">InternetChargeType</a>。</p> |
| period                 | Integer                                          | <p>购买实例的时长。</p><p>单位：月。</p><p>后付费实例该字段为null。</p>                                                 |
| publicIpAddresses      | Array of String                                  | <p>实例公网IPv4列表。</p><p>如果机器的主IP未加入到公网组网接口，那么主IP将无法使用，且该字段也不会返回该IP。</p>                             |
| privateIpAddresses     | Array of String                                  | 实例内网IP列表。                                                                                        |
| ipv6Addresses          | Array of String                                  | <p>实例的IPv6地址。</p><p>注意：此字段可能返回null，表示取不到有效值。</p>                                                 |
| subnetIds              | Array of String                                  | 实例所属的内网组网ID列表。                                                                                   |
| createTime             | Timestamp                                        | <p>创建时间。</p><p>格式为：<code>YYYY-MM-DDThh:mm:ssZ</code>。</p>                                        |
| expiredTime            | Timestamp                                        | <p>到期时间。</p><p>格式为：<code>YYYY-MM-DDThh:mm:ssZ</code>。</p>                                        |
| resourceGroupId        | String                                           | 实例所属资源组的ID。                                                                                      |
| resourceGroupName      | String                                           | 实例所属资源组的名称。                                                                                      |
| instanceStatus         | String                                           | <p>实例状态。</p><p>状态类型详见<a href="datastructure.md#instancestatus">实例状态</a>。</p>                     |
| primaryPublicIpAddress | String                                           | 实例的母IP。                                                                                          |
| trafficPackageSize     | Double                                           | <p>流量包订购大小。</p><p>单位为TB。</p>                                                                     |
| raidConfig             | [RaidConfig](datastructure.md#raidconfig)        | 磁盘阵列配置。                                                                                          |
| partitions             | Array of [Partition](datastructure.md#partition) | 分区配置。                                                                                            |
| nic                    | [Nic](datastructure.md#nic)                      | 网卡配置。                                                                                            |

## EipStatus

EIP状态。

| 状态值            | 状态说明  |
| -------------- | ----- |
| CREATING       | 创建中   |
| CREATE\_FAILED | 创建失败  |
| ASSOCIATING    | 绑定中   |
| UNASSOCIATING  | 解绑中   |
| INUSE          | 已分配   |
| AVAILABLE      | 可用    |
| RELEASING      | 释放中   |
| RECYCLE        | 在回收站中 |

## DdosIpStatus

Ddos IP状态。

| 状态值            | 状态说明  |
| -------------- | ----- |
| CREATING       | 创建中   |
| CREATE\_FAILED | 创建失败  |
| ASSOCIATING    | 绑定中   |
| UNASSOCIATING  | 解绑中   |
| INUSE          | 已分配   |
| AVAILABLE      | 可用    |
| RELEASING      | 释放中   |
| RECYCLE        | 在回收站中 |

## CidrBlockInfo

| 名称                | 类型              | 描述                                                        |
| ----------------- | --------------- | --------------------------------------------------------- |
| cidrBlockId       | String          | Cidr Block唯一ID。                                           |
| cidrBlockType     | String          | <p>CIDR的类型。</p><p>取值范围：IPV4、IPV6。</p>                     |
| cidrBlockName     | String          | Cidr Block名称。                                             |
| zoneId            | String          | Cidr Block所属的可用区ID。                                       |
| cidrBlock         | String          | CIDR。                                                     |
| gateway           | String          | 网关地址。                                                     |
| availableIpStart  | String          | 可用IP的开头。                                                  |
| availableIpEnd    | String          | 可用IP的结尾。                                                  |
| availableIpCount  | Integer         | 可用IP的数量。                                                  |
| instanceIds       | Array of String | 已绑定的实例ID列表。                                               |
| status            | String          | [Cidr Block状态](datastructure.md#cidrblockstatus)。         |
| chargeType        | String          | <p>计费类型。</p><p>PREPAID：预付费，即包年包月。</p><p>POSTPAID：后付费。</p> |
| createTime        | Timestamp       | <p>创建时间。</p><p>格式为：<code>YYYY-MM-DDThh:mm:ssZ</code>。</p> |
| expireTime        | Timestamp       | <p>到期时间。</p><p>格式为：<code>YYYY-MM-DDThh:mm:ssZ</code>。</p> |
| resourceGroupId   | String          | 所属资源组的ID。                                                 |
| resourceGroupName | String          | 所属资源组的名称。                                                 |

## CidrBlockStatus

Cidr Block的状态。

| 状态值            | 状态说明  |
| -------------- | ----- |
| CREATING       | 创建中   |
| CREATE\_FAILED | 创建失败  |
| RECYCLING      | 回收中   |
| RECYCLE        | 在回收站中 |
| AVAILABLE      | 可用    |

## AvailableIpv4Resource

可用的Ipv4 Cidr Block资源。

| 名称         | 类型      | 描述                                                                                                                        |
| ---------- | ------- | ------------------------------------------------------------------------------------------------------------------------- |
| zoneId     | String  | Cidr Block所属的可用区ID。                                                                                                       |
| netmask    | Integer | 掩码。                                                                                                                       |
| sellStatus | String  | <p>售卖的状态。</p><ul><li>SELL：表示实例可购买，且库存>10。</li><li>SELL_SHORTAGE: 表示可购买，但是库存&#x3C;10台。</li><li>SOLD_OUT：表示实例已售罄。</li></ul> |

## AvailableIpv6Resource

可用的Ipv6 Cidr Block资源。

| 名称         | 类型     | 描述                                                                                                                        |
| ---------- | ------ | ------------------------------------------------------------------------------------------------------------------------- |
| zoneId     | String | Cidr Block所属的可用区ID。                                                                                                       |
| sellStatus | String | <p>售卖的状态。</p><ul><li>SELL：表示实例可购买，且库存>10。</li><li>SELL_SHORTAGE: 表示可购买，但是库存&#x3C;10台。</li><li>SOLD_OUT：表示实例已售罄。</li></ul> |

## InstanceAvailableCidrBlock

实例可用的Cidr Block。

| 名称               | 类型              | 描述                                    |
| ---------------- | --------------- | ------------------------------------- |
| cidrBlockId      | String          | Cidr Block唯一ID。                       |
| zoneId           | String          | Cidr Block所属的可用区ID。                   |
| cidrBlockIpType  | String          | <p>CIDR的类型。</p><p>取值范围：IPV4、IPV6。</p> |
| cidrBlock        | String          | CIDR。                                 |
| availableIps     | Array of String | 可用的IP列表。                              |
| availableIpCount | Integer         | 可用的IP数量。                              |



## CidrBlockIp

| 名称            | 类型     | 描述                                           |
| ------------- | ------ | -------------------------------------------- |
| cidrBlockId   | String | Cidr Block唯一ID。                              |
| cidrBlockType | String | <p>CIDR的类型。</p><p>取值范围：IPV4、IPV6。</p>        |
| ip            | String | IP。                                          |
| instanceId    | String | 绑定的实例ID。                                     |
| status        | String | [IP的状态](datastructure.md#cidrblockipstatus)。 |

## CidrBlockIpStatus

Cidr Block的IP状态。

| 状态值       | 状态说明 |
| --------- | ---- |
| BINDED    | 已绑定  |
| BINDING   | 绑定中  |
| UNBINDING | 解绑中  |
| AVAILABLE | 可用   |



## VpcRegionInfo

VPC 节点的信息

| 名称            | 类型               | 描述          |
| ------------- | ---------------- | ----------- |
| vpcRegionId   | String           | VPC的节点ID。   |
| vpcRegionName | String           | VPC的节点名称。   |
| zoneIds       | Array of String  | Zone ID 列表。 |



## VpcInfo

Vpc Info的信息

| 名称                | 类型        | 描述                                                        |
| ----------------- | --------- | --------------------------------------------------------- |
| vpcId             | String    | VPC的实例ID。                                                 |
| vpcRegionId       | String    | VPC的节点ID。                                                 |
| vpcRegionName     | String    | VPC的节点名称。                                                 |
| vpcName           | String    | VPC的实例名称。                                                 |
| cidrBlock         | String    | VPC的CIDR。                                                 |
| createTime        | Timestamp | <p>创建时间。</p><p>格式为：<code>YYYY-MM-DDThh:mm:ssZ</code>。</p> |
| resourceGroupId   | String    | 资源组ID。                                                    |
| resourceGroupName | String    | 资源组名称。                                                    |
| vpcStatus         | String    | [VPC的状态。](datastructure.md#vpcstatus)                     |



## VpcStatus

Vpc 状态

| 状态值            | 状态说明 |
| -------------- | ---- |
| CREATING       | 创建中  |
| CREATE\_FAILED | 创建失败 |
| AVAILABLE      | 可用   |
| DELETING       | 删除中  |



## SubnetStatus

Subnet 状态

|  状态值           | 状态说明 |
| -------------- | ---- |
| CREATING       | 创建中  |
| CREATE\_FAILED | 创建失败 |
| AVAILABLE      | 可用   |
| DELETING       | 删除中  |



## VpcSubnetStatus

Vpc subnet状态

| 状态值      | 状态说明 |
| -------- | ---- |
| BINDED   | 已绑定  |
| BINDDING | 绑定中  |
|          |      |





## SubnetInfo

Subnet Info的信息

| 名称                | 类型                                                         | 描述                                                           |
| ----------------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| subnetId          | String                                                     | Subnet实例ID。                                                  |
| subnetName        | String                                                     | Subnet的名称                                                    |
| zoneId            | String                                                     | Subnet所属的可用区ID。                                              |
| availableIpCount  | Integer                                                    | Subnet下可用的IP数量。                                              |
| cidrBlock         | String                                                     | Subnet的CIDR。                                                 |
| subnetStatus      | String                                                     | [Subnet的状态。](datastructure.md#subnetstatus)                  |
| createTime        | Timestamp                                                  | 创建时间。按照`ISO8601`标准表示，并且使用`UTC`时间。格式为：`YYYY-MM-DDThh:mm:ssZ`。 |
| vpcSubnetStatus   | String                                                     | [VPC与Subnet的绑定状态。](datastructure.md#vpcsubnetstatus)         |
| vpcId             | String                                                     | VPC实例ID。                                                     |
| vpcName           | String                                                     | VPC的名称。                                                      |
| resourceGroupId   | String                                                     | 资源组ID。                                                       |
| resourceGroupName | String                                                     | 资源组名称。                                                       |
| subnetInstanceSet | Array of [SubnetInstance](datastructure.md#subnetinstance) | Subnet下实例集合。                                                 |



## SubnetInstance

Subnet Instance信息

| 名称               | 类型     | 描述            |
| ---------------- | ------ | ------------- |
| instanceId       | String | 实例ID。         |
| privateIpAddress | String | 私网IP。         |
| privateIpStatus  | String | 私网IP与实例的绑定状态。 |



## IpBindParam

Cidr Block Ip绑定参数。

| 名称         | 类型     | 描述                                                                                                     |
| ---------- | ------ | ------------------------------------------------------------------------------------------------------ |
| instanceId | String | 实例ID。                                                                                                  |
| ip         | String | <p>IP。</p><p>可通过<code>DescribeInstanceAvailableCidrBlock</code>接口返回值中的<code>availableIps</code>获取。</p> |



## AssociateSubnetInstance

Subnet绑定实例。

| 名称               | 类型     | 描述                                                            |
| ---------------- | ------ | ------------------------------------------------------------- |
| instanceId       | String | 实例ID。                                                         |
| privateIpAddress | String | 内网IPv4地址。该地址必须在子网的CIDR范围内。 如果不指定内网地址，系统会会寻找CIDR中未用的内网地址下发到实例。 |
|                  |        |                                                               |

