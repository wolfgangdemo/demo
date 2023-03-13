# 公共错误码

对于请求HTTP状态码不是200的，表示API接口调用失败。

## 错误码

| HTTP状态码 | 错误码                                            | 语义                                       |
| ------- | ---------------------------------------------- | ---------------------------------------- |
| 500     | INTERNAL\_SERVER\_ERROR                        | 服务端内部错误。                                 |
| 503     | SERVICE\_TEMPORARY\_UNAVAILABLE                | 服务端暂时不可用，请稍后操作。                          |
| 503     | REQUEST\_TIMED\_OUT                            | 请求超时。                                    |
| 401     | AUTHFAILURE\_INVALID\_AUTHORIZATION            | 请求头部的 Authorization 不符合Zenalyer Cloud标准。 |
| 401     | AUTHFAILURE\_SIGNATURE\_FAILURE                | 签名计算错误。请对照调用方式中的签名方法文档检查签名计算过程。          |
| 401     | AUTHFAILURE\_UNAUTHORIZED\_OPERATION           | 请求未授权，请确认接口存在或者有授予了访问权限。                 |
| 401     | AUTHFAILURE\_SIGNATURE\_EXPIRED                | 签名过期。Timestamp和服务器时间不得相差超过五分钟。           |
| 400     | MISSING\_PARAMETER                             | 缺少必须的参数。                                 |
| 400     | INVALID\_PARAMETER\_TYPE                       | 参数类型不合法。                                 |
| 400     | INVALID\_PARAMETER\_EXCEED\_MAXIMUM            | 参数值大小超过了限制。                              |
| 400     | INVALID\_PARAMETER\_LESS\_MINIMUM              | 参数值小于了最低限制。                              |
| 400     | INVALID\_PARAMETER\_EXCEED\_LENGTH             | 参数值数量超过了允许的最大长度。                         |
| 400     | INVALID\_PARAMETER\_LESS\_LENGTH               | 参数值数量小于了最低要求的长度。                         |
| 400     | INVALID\_PARAMETER\_PATTERN\_ERROR             | 参数值所要求的格式不匹配。                            |
| 400     | INVALID\_PARAMETER\_DATE\_FORMAT\_ERROR        | 参数值的日期格式不正确。                             |
| 400     | INVALID\_PARAMETER\_VALUE                      | 参数值没在规定的值里面。                             |
| 403     | OPERATION\_FAILED\_FOR\_RECYCLE\_RESOURCE      | 对于回收中的资源进行操作是不被允许的。                      |
| 404     | OPERATION\_FAILED\_RESOURCE\_GROUP\_NOT\_FOUND | 对于指定操作的资源组不存在。                           |
| 404     | OPERATION\_FAILED\_RESOURCE\_NOT\_FOUND        | 指定的资源不存在导致操作失败。                          |

