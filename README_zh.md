# 此仓已废弃，请前往新仓 [developtool_hapsigner](https://gitee.com/openharmony/developtools_hapsigner)

# 签名工具仓<a name="ZH-CN_TOPIC_0000001086718894"></a>

-   [简介](#section11660541593)
-   [目录](#section161941989596)
-   [约束](#section119744591305)
-   [说明](#section1312121216216)
-   [常见问题](#section1312121216343)

## 简介<a name="section11660541593"></a>

在OpenHarmony构建中需要对应用进行签名，以此保证应用完整性和来源可靠。本仓提供二进制签名工具（hapsigntoolv2.jar），用于OpenHarmony应用签名。

## 目录<a name="section161941989596"></a>

```
/prebuilts/signcenter
├── NOTICE                     # 开源NOTICE
├── hapsigntool                # 签名工具存放目录
│   └── hapsigntoolv2.jar     # OpenHarmony应用签名工具
```

## 约束<a name="section119744591305"></a>

运行环境约束：JDK8

## 说明<a name="section1312121216216"></a>

签名命令示例：

```
java -jar hapsigntoolv2.jar sign -mode localjks -privatekey "OpenHarmony Software Signature" -inputFile camera.hap -outputFile signed_camera.hap -signAlg SHA256withECDSA -keystore OpenHarmony.jks -keystorepasswd 123456 -keyaliaspasswd 123456 -profile camera_release.p7b -certpath OpenHarmony.cer -profileSigned 1
```

关键字段说明：

```
hapsigntoolv2.jar ：OpenHarmony签名工具
-mode ：签名模式。OpenHarmony签名密钥存放于本地keystore文件，因此签名模式选择localjks
-privatekey：密钥对别名
-inputFile ：待签名的应用
-outputFile：签名后的应用
-signAlg : 签名算法
-keystore：keystore文件路径
-keystorepasswd：keystore的密码，OpenHarmony.jks的默认密码为123456
-keyaliaspasswd：签名密钥的密码，密钥（OpenHarmony Software Signature）的默认密码为123456
-profile ：应用能力授权文件
-certpath：签名证书文件路径
-profileSigned：指示profile文件是否带有签名，1表示有签名，0表示没有签名，缺省值为1。
```

## 常见问题<a name="section1312121216343"></a>

**1.密钥对别名参数不正确**

- **现象描述**

执行命令后提示 "error:Key Alias is not right"。

- **可能原因**
 
密钥对别名参数不正确。
 
- **解决办法**
 
填写生成应用证书对应的正确的密钥对别名。


**2.profile文件被篡改**

- **现象描述**

执行命令后提示 "error:Verify profile pkcs7 failed! Profile is invalid"。

- **可能原因**
 
profile文件被篡改。
 
 - **解决办法**
 
检查profile文件是否被篡改。

**3.签名算法填写不正确**

- **现象描述**

执行命令后提示 "error:Invalid parameter:Sign Alg"。

- **可能原因**
 
签名算法填写不正确。
 
- **解决办法**
 
应用证书密钥对推荐使用ECC生成，hap签名算法修改为ECC对应的SHA256withECDSA,SHA384withECDSA


**4.签名密钥口令或密钥库口令错误或密钥库文件格式错误**

- **现象描述**

执行命令后提示 "error:Store File error，possible reason：1.please check whther Store Password or key Password is right,2.Sign Alg does not match with Alg of private key,etc"。

- **可能原因**
 
签名密钥口令或密钥库口令错误或密钥库文件格式错误

 
- **解决办法**
 
检查并修正签名密钥口令或密钥库口令；检查密钥库文件格式是否正确，填写正确格式的密钥库文件

**5.密钥库文件、原始包文件、证书文件不存在或文件名填写不正确**

- **现象描述**

执行命令后提示 "java.io.FileNotFoundException: （文件名）(系统找不到指定的文件)"。

- **可能原因**

 密钥库文件、原始包文件、证书文件不存在或文件名填写不正确


 
- **解决办法**
 
根据报错提示检查具体文件名是否存在或是否填写正确。

**6.证书文件格式错误**

- **现象描述**

执行命令后提示 "No certificates configured for signer"。

- **可能原因**

 证书文件格式错误


- **解决办法**
 
检查证书文件的格式是否正确，填写正确的证书文件。


