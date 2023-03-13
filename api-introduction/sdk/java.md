# Java

## 依赖环境 <a href="#title-6g8-ghg-nk5" id="title-6g8-ghg-nk5"></a>

* JDK 7 版本及以上。
* 获取Access Key ID 和 Access Key Password。使用 Zenlayer Cloud SDK，您需要在云平台拥有一个云账号，并在 Zenlayer 云平台控制台中创建和查看您的 Access Key ID 以及 Access Key Password。如何获取详见[帮助文档](https://docs.console.zenlayer.com/welcome/platform/team-management/generate-an-api-access-key)。
* 获取服务域名。目前Zenlayer Cloud API服务域名为**`console.zenlayer.com`**。



## 安装SDK

### 方式一、通过 Maven 安装（推荐）

如果您使用Maven来管理Java项目，只需在项目的pom.xml文件的`<dependencies>`标签中加入相应的依赖项即可。您可以在 [Maven 仓库](https://search.maven.org/search?q=zenlayercloud-java-sdk) 上找到最新的版本。您只需在pom.xml中声明以下依赖：

```
<dependency>
    <groupId>com.zenlayer</groupId>
    <artifactId>zenlayercloud-sdk-java</artifactId>
    <!-- 请到https://search.maven.org/search?q=zenlayercloud-java-sdk查询所有版本，最新版本如下 -->
    <version>0.6.0</version>
</dependency>
```

### 方式二、通过源码包安装

1. 前往 [Github 代码托管地址](http://www.baidu.com) 下载源码压缩包。
2. 解压源码包到您项目合适的位置。
3. 将解压后的 jar 包放在 java 可找到的路径中。
4. 引用方法可参考示例。



## 使用示例 <a href="#title-6g8-ghg-nk5" id="title-6g8-ghg-nk5"></a>

以创建实例接口`CreateInstances`为例，示例代码中的下列参数需要您根据实际情况自行填写。

* \<AccessKey>：您的Access Key ID。获取方式请参见[获取AccessKey](../instruction/sign.md#shen-qing-an-quan-ping-zheng)。
* \<AccessSecret>：您的Access Key Password。获取方式请参见[获取AccessKey](../instruction/sign.md#shen-qing-an-quan-ping-zheng)。

{% code lineNumbers="true" %}
```java
import com.zenlayercloud.bmc20221120.BmcClient;
import com.zenlayercloud.bmc20221120.models.request.CreateInstancesRequest;
import com.zenlayercloud.bmc20221120.models.response.CreateInstancesResponse;
import com.zenlayercloud.common.Credential;
import com.zenlayercloud.common.ZenlayerSdkException;

public class Example {

    public static void main(String[] args) {
        // 1. 初始化client
        Credential credential = new Credential("<AccessKey>", "<AccessSecret>");
        BmcClient client = new BmcClient(credential);
        
        // 2. 设置API请求参数
        CreateInstancesRequest createInstancesRequest = new CreateInstancesRequest();
        createInstancesRequest.instanceChargeType = "PREPAID";
        createInstancesRequest.internetChargeType = "ByBandwidth";
        createInstancesRequest.zoneId = "SEL-A";
        createInstancesRequest.instanceTypeId = "M8C";

        try {
            // 3. 发起API请求并获得响应结果
            CreateInstancesResponse instances = client.createInstances(createInstancesRequest);

        } catch (ZenlayerSdkException e) {
            // 4. 处理应答异常
        }
    }
    
}
```
{% endcode %}

