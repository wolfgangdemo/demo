# 签名方法 v2

### 申请安全凭证

本文使用的安全凭证为密钥，密钥包括 accessKeyId 和 accessKeyPassword。

* AccessKeyId：用于标识 API 调用者身份，可以简单类比为用户名。
* AccessKeyPassword：用于验证 API 调用者的身份，可以简单类比为密码。
* **用户必须严格保管安全凭证，避免泄露，否则将危及财产安全。如已泄漏，请立刻禁用该安全凭证。**

你可以根据[Zenlayer的用户指南文档](https://support.zenlayer.com/s/reference-page?language=en\_US\&article=Obtain-Use-Access-Key)来获取你的安全凭证。



### 签名过程v2

Zenlayer Open API V2 支持 Post 请求，仅支持 `Content-Type: application/json`。 接口使用json格式进行调用。

下面以裸机云查询实例列表为例：

{% code overflow="wrap" %}
```url
curl -X POST https://console.zenlayer.com/api/v2/bmc \
-H "Authorization: ZC2-HMAC-SHA256 Credential=***Dz8krbsJ5yKBZQpn74WFkmLPx3*******, SignedHeaders=content-type;host, Signature=4281c8845a9b817e6226108ca93e68d64227d70da26999a4ee8938d14599ea33" \
-H "Content-Type: application/json; charset=utf-8" \
-H "X-ZC-Action: DescribeInstances" \
-H "X-ZC-Timestamp: 1673361177" \
-H "X-ZC-Signature-Method: ZC2-HMAC_SHA256" \
-H "X-ZC-Version: 2022-11-20" \
-d '{"pageSize":10,"pageNum":1,"zoneId":"HKG-A"}'
```
{% endcode %}

**Request Headers:**

| **Key**               | **说明**      | **示例**              |
| --------------------- | ----------- | ------------------- |
| X-ZC-Timestamp        | 请求的时间戳，精确到秒 | `1669205699`        |
| X-ZC-Version          | 请求的API版本    | `2022-11-20`        |
| X-ZC-Action           | 请求的动作       | `DescribeInstances` |
| X-ZC-Signature-Method | 签名方法        | `ZC2-HMAC_SHA256`   |
| Authorization         | 签名认证        |                     |

#### 1. 拼接规范请求串

按如下伪代码格式拼接规范请求串（CanonicalRequest）：

{% code overflow="wrap" %}
```
CanonicalRequest = 
  HTTPRequestMethod + '\n' + 
  CanonicalURI + '\n' + 
  CanonicalQueryString + '\n' + 
  CanonicalHeaders + '\n' + 
  SignedHeaders + '\n' + 
  HexEncode(Hash(RequestPayload))
```
{% endcode %}

| 字段名称                 | 解释                                                                                                                                                                                                                                                                    |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HTTPRequestMethod    | <p>HTTP 请求方法。</p><p>固定为POST。</p>                                                                                                                                                                                                                                      |
| CanonicalURI         | <p>URI 参数。</p><p>API 固定为正斜杠（/）。</p>                                                                                                                                                                                                                                   |
| CanonicalQueryString | <p>发起 HTTP 请求 URL 中的查询字符串。</p><p>对于 POST 请求，固定为空字符串""。</p>                                                                                                                                                                                                            |
| CanonicalHeaders     | <p>参与签名的头部信息，可加入自定义的头部参与签名以提高自身请求的唯一性和安全性。 </p><p>拼接规则：头部 key 和 value 统一转成小写，并去掉首尾空格，按照 key:value\n 格式拼接；多个头部，按照头部 key（小写）的 ASCII 升序进行拼接。此示例计算结果是 <code>content-type:application/json; charset=utf-8\nhost:example.com</code>。</p>                                    |
| SignedHeaders        | <p>参与签名的头部信息。</p><p>说明此次请求有哪些头部参与了签名，和 CanonicalHeaders 包含的头部内容是一一对应的。content-type 和 host 为必选头部。 拼接规则：头部 key 统一转成小写；多个头部 key（小写）按照 ASCII 升序进行拼接，并且以分号（;）分隔。此示例为<code>content-type;host</code>。</p>                                                                    |
| HashedRequestPayload | <p>请求正文（payload，即 body。</p><p>此示例为<code>{"pageSize":10,"pageNum":1,"zoneId":"HKG-A"}</code>）的哈希值，计算伪代码为 HexEncode(Hash(RequestPayload))，即对 HTTP 请求正文做 SHA256 哈希，然后十六进制编码。此示例的计算结果是 <code>5f714687ba91c606d503467766151206392474accd137ffea6dce2420b67c29a</code>。</p> |

#### 2. 拼接待签字符串

```
StringToSign =
    Algorithm + \n +           # 指定签名算法。对于 SHA256，算法为 ZC2-HMAC-SHA256。
    RequestDateTime + \n +     # 指定请求时间戳。
    HashedCanonicalRequest 
```

| 字段名称                   | 解释                                                                                                                                                                                 |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Algorithm              | <p>签名算法。</p><p>目前固定为 <code>ZC2-HMAC-SHA256</code>。</p>                                                                                                                             |
| RequestTimestamp       | <p>请求时间戳。</p><p>即请求头部的公共参数 X-ZC-Timestamp 取值，取当前时间 UNIX 时间戳，精确到秒。此示例取值为 <code>1551113065</code>。</p>                                                                               |
| HashedCanonicalRequest | <p>前述步骤拼接所得规范请求串的哈希值。</p><p>计算伪代码为 Lowercase(HexEncode(Hash.SHA256(CanonicalRequest)))。此示例计算结果是 <code>36c8692f0d1104c0624b2e4dddbc446baa97f1cbb0acfbb9f5cc3b6f41ce2b3c</code>。</p> |

根据以上规则，示例中得到的待签名字符串如下：

```
ZC2-HMAC-SHA256
1675318358
36c8692f0d1104c0624b2e4dddbc446baa97f1cbb0acfbb9f5cc3b6f41ce2b3c
```

#### 3. 基于 AK 和 StringToSign 计算出签名

计算签名，伪代码如下：

```
Signature = HexEncode(HMAC_SHA256(SecretKey, StringToSign))
```

| 字段名称         | 解释                                                                           |
| ------------ | ---------------------------------------------------------------------------- |
| SecretKey    | <p>原始的 SecretKey。</p><p>即 <code>Gu5t9xGARNpq86cd98joQYCN3*******</code>。</p> |
| StringToSign | 步骤三中根据以上方法。                                                                  |

#### **4. 拼接 Authorization**

按如下格式拼接 Authorization：

```
Authorization =
    Algorithm + ' ' +
    'Credential=' + AccessKeyId +  ', ' +
    'SignedHeaders=' + SignedHeaders + ', ' +
    'Signature=' + Signature
```

| 字段名称          | 解释                                                                                                               |
| ------------- | ---------------------------------------------------------------------------------------------------------------- |
| Algorithm     | <p>签名算法。</p><p>目前为 <code>ZC2-HMAC-SHA256</code>。</p>                                                             |
| AccessKeyId   | <p>密钥对中的 SecretId。</p><p>即 <code>0D9UtpyKYcHxms5v</code>。</p>                                                    |
| SignedHeaders | <p>见上文，参与签名的头部信息。</p><p>此示例取值为 <code>content-type;host</code>。</p>                                               |
| Signature     | <p>签名值。</p><p>根据以上方法，此示例计算结果是 <code>4281c8845a9b817e6226108ca93e68d64227d70da26999a4ee8938d14599ea33</code>。</p> |

