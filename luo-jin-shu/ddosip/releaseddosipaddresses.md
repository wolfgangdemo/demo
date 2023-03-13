# ReleaseDdosIpAddresses

## 1. 接口描述

调用本接口用于释放一个或多个Ddos IP。

{% hint style="info" %}
#### 注意事项

* 回收站的Ddos IP默认保留24小时。
* 只有在回收站中的Ddos IP（即状态是 **RECYCLE**）才支持该操作。
* 支持批量操作，每次请求批量Ddos IP的上限为100。
{% endhint %}



## 2. 请求参数

以下请求参数列表仅列出了接口中需要的请求参数

| 参数名称      | 必选 | 类型              | 描述                                                                                                      |
| --------- | -- | --------------- | ------------------------------------------------------------------------------------------------------- |
| ddosIpIds | 是  | Array of String | <p>一个或多个待操作Ddos IP ID。</p><p>可通过<code>DescribeDdosIpAddresses</code>接口返回值中的<code>ddosIpId</code>获取。</p> |



## 3. 响应结果

| 参数名称      | 类型     | 描述                                                       |
| --------- | ------ | -------------------------------------------------------- |
| requestId | String | <p>唯一请求 ID。</p><p>每次请求都会返回。定位问题时需要提供该次请求的 RequestId。</p> |



## 4. 代码示例

{% tabs %}
{% tab title="示例" %}
#### 1. 批量释放Ddos IP

释放2个Ddos IP。

```json
POST / HTTP/1.1
Host: console.zenlayer.com/api/v2/bmc
Content-Type: application/json
X-ZC-Action: ReleaseDdosIpAddresses
<Common Request Params>

Request：
{
    "ddosIpIds": ["ddosIpId1","ddosIpId2"]
}

Response：
{
  "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3",
  "response": { 
    "requestId": "T05992D0C-7E8B-4047-B0C0-780F2CD549D3"
  }
}
```
{% endtab %}
{% endtabs %}



## 5. 开发者工具

Zenlayer Cloud API 2.0 提供了配套的[开发工具集（SDK）](../../api-introduction/sdk/)，未来会陆续支持更多开发语言，方便快速接入和使用Zenlayer的产品和服务。



## 6. 错误码

下面包含业务逻辑中遇到的错误码，其他错误码见[公共错误码](../../api-introduction/instruction/commonerrorcode.md)

| HTTP状态码 | 错误码                                   | 说明               |
| ------- | ------------------------------------- | ---------------- |
| 403     | OPERATION\_DENIED\_EIP\_NOT\_RECYCLED | 指定的Ddos IP不在回收站。 |
