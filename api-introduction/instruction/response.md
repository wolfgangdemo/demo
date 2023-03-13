# 返回结果

对于成功的请求，HTTP 状态码返回的为200。 对于请求调用失败的，HTTP 状态码返回的不是200，为4xx或5xx。4xx一般代表参数的不合法或者操作不允许，5xx则为服务系统遇到了一些问题。

{% hint style="info" %}
Zenlayer Cloud API的许多接口为异步操作， 请求成功并不代表着操作完成并且成功。
{% endhint %}



## 成功的返回结果

以裸机云的接口创建实例 (CreateInstances) 为例，若调用成功，其可能的返回如下：

```
{
    "requestId": "T67723B59-F4D1-42EA-BDC1-5E67167FD8CC",
    "response": {
       "requestId": "T67723B59-F4D1-42EA-BDC1-5E67167FD8CC",
       "instanceIdSet" : ["1234567654321"],
       "orderNumber": "1234567654321"
    }
}
```

* **requestId：**一次 API 请求的唯一标识，如果 API 出现异常，可以联系我们，并提供该 ID 来解决问题。
* **response：**成功返回的数据部分，其内容结构见每个接口的返回结果。
* response其内部的 RequestId 也是固定的字段，其值和外部的requestId一致。

## 失败的返回结果

若调用失败，其返回值如如下示例：

```json
{
    "requestId": "T67723B59-F4D1-42EA-BDC1-5E67167FD8CC",
    "code": "INVALID_ZONE_NOT_FOUND",
    "message": "The specified zoneId `SEL--A` is not found"
}
```

* **requestId：**一次 API 请求的唯一标识，如果 API 出现异常，可以联系我们，并提供该 ID 来解决问题。
* **code：**错误码，具体错误码见每个接口的错误码部分。
* **message：**描述错误发生的具体原因，随着业务发展或体验优化，此文本可能会发生变化，用户不应依赖这个返回值。
