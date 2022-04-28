---
title: OTT PAY HK跨境支付API文档

language_tabs: # must be one of https://git.io/vQNgJ
  - 代码示例
  
toc_footers:
  - Copyright © 2022-OTTPay HK

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the OTTPay HK API
---
# OTT PAY HK跨境支付API文档
# 1. 概述
## 1.1 编写目的
目的是约定商户与Ottpayhk付款系统间的业务接口。包括通讯协议、交易接口规范、文件格式、加密和摘要规范。指
导商户开发人员依据本规范开发，并与Ottpayhk付款系统对接。
## 1.2 定义和缩略语
UML时序图

 ![UML时序图](https://docs.hksd.ottpayhk.com/uml.png "UML时序图")


## 1.3 平台测试/上线准备事项
 
### 测试联调阶段
平台开发完成进行系统联调测试前，需要准备如下事项：  
1. 平台生成测试环境的**RSA**密钥对，并将公钥发提供给Ottpayhk；  
2. 申请开通测试环境平台号；  

### 上线阶段
3. 平台生成生产环境的RSA密钥对，并将公钥提供给Ottpayhk；
4. 向Ottpayhk提供平台服务器IP地址
5. 申请开通生产环境平台号


## 1.4 更新日志
**1.0.35  【待补充】  2022-04-27**  
1. 【待补充】

**1.0.34  新增一级商户入网接口  2022-03-04**  
1. 新增商户入网接口

**1.0.33  人名币付款接口更新还原材料字段  2022-01-17**  
1. 人民币付款接口更新字段

**1.0.32  牌价查询接口增加T2锁汇类型  2022-01-07**  
1. 牌价查询接口增加T2锁汇类型 

**1.0.31  贸易合同申请接口更新  2021-09-07**  
1. 贸易订单申请新增服务贸易字段信息TP1012  

**1.0.30  追加退款通知接口  2021-08-06**  
1. 新增人民币和国际汇款的退款通知接口(tp2010)

**1.0.29  新增贸易收款相关接口  2021-06-23**  
1. 新增贸易订单申请tp1012/收款流水和贸易订单关联tp1013/回调地址设置tp1014
2. 贸易收款到账通知tp2007/贸易订单申请结果通知tp2008/收款流水和贸易订单关联结果通知tp2009
3. 新增贸易订单申请信息查询接口tp3013/新增收款流水和贸易订单关联查询接口tp3014/贸易收款VA入账查询接口tp3015
4. 人民币付款tp1001增加手机号必填项

**1.0.28  修改5.1.7 商户入网  2021-06-18**  
1. 修改商户入网字段

**1.0.27  修改tp1001接口请求字段  2021-06-01**  
1. 新增payReduceList还原材料字段（仅限游戏、电商、一般贸易时填写）

**1.0.26  增加5.1.10 VA账户开户申请tp1011和5.3.16 VA账户查询tp3012  2021-05-31**  
1. 新增5.1.10 VA账户开户申请tp1011。
2. 新增5.3.16 VA账户查询tp3012。

**1.0.25  增加5.1.9商户间转账接口tp1010  2021-04-21**  
1. 新增5.1.9商户间转账接口tp1010，支持同为OTT注册的商户完成内部转账。

**1.0.24  修改tp1004接口请求字段  2021-03-17**  
1. tp1004国际汇款，新增debitAmount扣款金额，可支持锁定扣款金额或付款金额2种。

**1.0.23  修改tp3005接口返回字段  2021-03-15**  
1. 更新purpose汇款目的

**1.0.22  修改tp3005接口返回字段  2021-03-09**  
1. 增加selectOption枚举值返回

**1.0.21  修改tp1001接口请求字段  2021-01-12**  
1. PayOrderRequest内新增必填字段payeeName收款方姓名
2. cNAPSCode改为唯一必填项

**1.0.20  修改tp3006接口返回字段  2020-11-12**  
1. tp3006返回code和message修改为resCode和resMessage

**1.0.19  增加一天一价牌价查询接口  2020-10-12**  
1. 新增5.3.15 一天一价牌价查询

**1.0.18  增加商户查询充值流水列表、账务流水列表以及手续费流水列表  2020-08-06**  
1. 新增5.3.12 充值交易历史查询
2. 新增5.3.13 账务流水交易查询
3. 新增5.3.14 手续费交易历史查询

**1.0.17  增加商户入网接口&人民币接口修改   2020-07-31**  
1. 新增5.1.7商户入网/5.1.8商户入网信息完善/5.2.4商户入网结果通知
2. 5.1.1人民币付款请求参数增加feeFlag，返回参数增加feeCurrency/feeAmount/actualPayAmount
3. 5.3.1人民币付款查询，返回参数增加feeCurrency/feeAmount/actualPayAmount

**1.0.16  新增tp2006国际汇款付款凭证通知   2020-06-04**  

**1.0.15  tp3005增加银行列表字段   2020-04-22**  

**1.0.14  国际汇款修改   2020-03-20**  
1. 国际汇款增加汇款附言
2. 更新 purpose 汇款目的
3. 更新 purpose 汇款目的

**1.0.13  国际汇款增加关联fx订单字段   2020-03-17**  

**1.0.12  修改人民币付款接口字段   2020-03-01**  

**1.0.11  FX和国际汇款修改   2020-02-28**  
1. FX 接口增加支持 T0 T1 锁汇
2. 对国际汇款相关接口字段修改：增加汇款目的

**1.0.10  人民币下发申请字段修改   2020-02-13**  
1. 人民币下发申请接口新增字段
2. 首次收款人提交营业执照和法人照片

**1.0.9   人民币下发回调新增字段respCode   2020-01-22**  

**1.0.8   增加国际汇款相关接口   2020-01-17**  

**1.0.7   增加联行号查询接口   2020-01-16**  

**1.0.6 人民币付款添加受理状态   2019-12-30**  

**1.0.5 修改批量付款请求   2019-12-26**  

**1.0.4 增加FX相关接口   2019-12-18**  

**1.0.3 修改批量上传接口参数   2019-12-17**  

**1.0.2 修改批量上传接口   2019-12-16**  

**1.0.1 增加5.3.1和6.1   2019-05-13**  

**1.0.0 新建   2019-04-29**  


# 2. 通讯协议

## 2.1 协议约定

1. 平台与Ottpayhk之间基于**HTTPS1.2**协议通讯，报文组织形式采用 **json** 规范。
2. 双方的报文都密文形式发送，必须同时将报文的密文、会话密钥密文和签名传输给对方。
3. 平台和Ottpayhk双方互为客户端和服务端。根据应用的要求，可以由平台作为客户端主动发起交易请求，Ottpayhk
来做应答。也可以由Ottpayhk主动发起交易请求，平台来做应答，平台在开户时需提前设置接收Ottpayhk的请求地址。
4. 客户端提交请求使用POST表单方式 **(Content-Type:application/json)** 提交，内容采用**UTF-8**编码。
5. 请求和响应均由五个域：**merchantNo**=平台代码、**jsonEnc**=报文密文、**keyEnc**=会话密钥密文、**sign**=报文签名


# 3 交易接口规范
## 3.1 请求报文

> 交易报文遵循JSON规范。示例:

```json
{
    "head":{
        "version":"1.0.1",          //--报文版本号
        "tradeType":"00",           //--00请求报文
        "tradeTime":"1551341750",   //--请求时间，10位unix时间戳
        "tradeCode":"TP1001",       //–请求交易代码
        "language":"cn",            //–语言
    },
    "body":{
        //…
    }
}
```
1. 请求报文由两部分组成：请求报文头和请求报文体。其中请求报文头信息在报文头（head. 节点内，请求报文体信息
在报文体（body. 节点内。
2. 报文头是每个交易都相同的。请求报文头信息的填写标准请参看“公共报文头说明”章节。
3. 报文体根据每个交易的接口定义而各不相同。请求报文体的定义请参看“业务交易接口”章节。需按照每个交易的接
口定义组装和解析请求报文体。
4. 客户端请求报文上送时，POST提交四个参数：**merchantNo**=平台代码;**jsonEnc**=报文密文；**keyEnc**=会话密钥密
文；**sign**=报文签名，其中**merchantNo**为Ottpayhk为合作平台分配的商户号明文，**jsonEnc**参数的内容就是整个报文加
密以后的**十六进制字符串**，**keyEnc**参数为报文加密会话密钥的密文，**sign**参数的内容是本次报文的签名。<br>

服务器端收到请求后按照HTTPS的方式获取参数后，按如下步骤处理：<br>
 步骤1：使用解密会话密钥<br>
 步骤2：对密文报文解密，得到报文明文；<br>
 步骤3：验证签名，签名通过后在解析报文内容。<br>
 
报文加密、签名和校验方式请参看“加密及签名规范”章节

<aside class="notice">
**注意：业务交易接口中定义的字段，无论其值是否为空都需要上送字段的json标签。**
</aside>

## 3.2 响应报文

> 交易报文遵循JSON规范。示例:

```json
{
    "head":{
        "version":"1.0.0",          //--报文版本号
        "tradeType":"01",           //--01响应报文
        "tradeTime":"1551341750",   //--响应时间，10位unix时间戳
        "tradeCode":"TP1001",       //--对应请求的交易代码
        "respCode":"S00000",        //--请求返回码
        "respDesc":"请求成功"        //--请求返回码
    },
    "body":{
        //…
    }
}
```
1. 交易应答报文由两部分组成：应答报文头和应答报文体。其中应答报文头信息在报文头（head）节点内，应答报文体
信息在报文体（body）节点内。
2. 报文头是每个交易都相同的。应答报文头信息的填写标准请参看"公共报文头说明”章节。
3. 报文体根据每个交易的接口定义而各不相同。应答报文体的定义请参看"交易报文接口”章节。需按照每个交易的接口
定义组装和解析应答报文体。
4. 交易成功时的应答报文，报文头的respCode为S00000，respDesc为"交易成功”,此时报文体（body）节点根据
实际业务需要为空也可以不为空。
5. 交易错误时的应答报文，错误码和错误信息填写在报文头的respCode（返回码）和respDesc（返回信息描述）域
中；报文体（body）节点为空。
1. 服务器端响应报文返回时，将商户号、报文密文、会话密钥和签名以标准json字符串返回 **{"merchantNo”:"",jsonEnc":"","keyEnc":"","sign":""}**，然后将字符串的字节流写入http的返回对象。客户端收到服务器端的响应时将HTTP服务方返回的字节流按照相应格式的字符串进行报文和摘要参数的获取，参数获
取后，先要进行摘要校验，校验通过后在解析报文内容。

报文摘要生成和校验方式请参看"[加密及签名规范](#4)”章节。 

# 4 加密及签名规范

## 4.1 原则
 
1. 交易报文传输都需要进行加密、签名和校验。
2. 无论是请求端还是响应端接收到报文后，都需要进行签名验证，即按照约定算法重新生成签名，然后和收到的签名进
行对比，对比通过后才能进行报文内容的解析，否则报文或文件内容可能出现篡改、部分丢失、伪造的问题。
3. 报文加密算法：DES/CBC/PKCS5Padding
4. 会话密钥生成：KeyGenerator生成
5. 会话密钥加密算法：RSA/ECB/PKCS1Padding
6. 签名算法：SHA1withRSA

## 4.2 RSA密钥对获得
 
```shell
openssl genrsa –out rsa_private_key_2048.pem2048 
#生成rsa私钥，以X509编码，指定生成的密钥的位数:2048

openssl pkcs8 –topk8 –in rsa_private_key_2048.pem –out pkcs8_rsa_private_key_2048.pem –nocrypt
#将上一步生成的rsa私钥转换成PKCS#8编码

openssl rsa –in rsa_private_key_2048.pem –out rsa_public_key_2048.pem –pubout
#导出rsa公钥，以X509编码商户需要按上面步骤生成商户的公钥pem发给Ottpayhk，
#或商户直接可以向Ottpayhk索要密钥对的生成脚本，生成商户所需的公私钥。
#Ottpayhk也需要把Ottpayhk生成的对应的公钥pem发给商户。
```

对于商户来说，需要生成商户自己的RSA密钥对（包含公钥和私钥），其中，私钥合作方自己保留，同时公钥提供给Ottpayhk。

对于Ottpayhk来说，需要为每个商户生成对应的公私钥对。其中，私钥Ottpayhk自己保留，公钥需要提供给商户。



## 4.3 报文加密及签名

 ![加密及签名](https://docs.hksd.ottpayhk.com/sign.png "加密及签名")

1. 对请求或响应**Json**报文明文（**UTF-8编码**. 使用发送方的私钥进行签名（**SHA1withRSA**. ，并将签名结果转换为**HEX字符串**，得到sign域。
2. 使用**KeyGenerator**生成器，生成**DES**加密会话密钥**SK**；
3. 使用**SK**对**Json**明文进行加密（**DES/CBC/PKCS5Padding**. ，并将加密结果转换为**HEX字符串**，得到**jsonEnc**
域。
4. 使用接收方公钥对会话密钥SK加密（**RSA/ECB/PKCS1Padding**. ，并将结果转换为**HEX字符串**，得到**keyEnc**
域。

## 4.4 报文解密及验签


![解密及验签](https://docs.hksd.ottpayhk.com/checkSign.png "解密及验签")


1. 将**keyEnc**域转换为二进制byte数组，使用接收方放的私钥对会话密钥，得到明文**SK**；
2. 将**jsonEnc**与转换为二进制byte数组，使用上一步得到的会话密钥**SK**解密，得到明文json；
3. 使用上一步解密得到的明文、发送方公钥和sign域数据验证签名的有效性。


#  5 业务接口

本章节描述商户接入Ottpayhk相关业务接口。<br>
M表示必输字段，O表示可选字段

## 5.1 商户入网
### 5.1.1 一级商户入网

**1 功能描述**

|          |                                                                |
| -------- |----------------------------------------------------------------|
| 交易代码 | TP1007                                                         |
| 功能名称 | 一级商户入网申请                                                       |
| 功能描述 | 收集商户资料，完成商户入网                                                  |
| 调用方式 | 实时接口                                                           |
| 调用流程 | --                                                             |
| 应用场景 | 本指引目的为OTTPAY HK收集商户资料信息，<br/>OTTPAY HK方资质审查后，予以商户资质审批通过，可为商户提供后续服务。 |

**2 请求地址**

**Url：** `https://{baseUrl}/api/tp1007`

> 请求示例:

```json
{
        "email": "one_0022@ott.com",
        "phoneAreaCode": "86",
        "phoneNum": "12524151321",
        "referralChannel": "文强哥推荐",
        "recommender": "ahaha",
        "countryCode": "CN",
        "merNameEn": "personone15",
        "parentRemark": "0",
        "ownerShipPath": ["uploadFile/abc.jpeg"], 
        "parentCertificate": ["uploadFile/abc.jpeg"],
        "parentCompany": [{
            "name": "",
            "country": ""
        }],
        "branchRemark": "0",
        "branchCompany": [{
            "name": "",
            "country": ""
        }],
        "certificate": ["uploadFile/abc.jpeg"],
        "nnc1Path": [],
        "nar1Path1": [],
        "mermorandum": [],
        "customerIdentity": "0",
        "customerId": [{
            "type": "1",
            "issuPlace": "CN",
            "certificates": ["uploadFile/abc.jpeg"]
        }],
        "shareholder": [{
            "type": "1",
            "issuPlace": "CN",
            "certificates": ["uploadFile/abc.jpeg"]
        }],
        "director": [{
            "type": "1",
            "issuPlace": "CN",
            "certificates": ["uploadFile/abc.jpeg"]
        }],
        "legalPerson": [{
            "type": "1",
            "issuPlace": "CN",
            "certificates": ["uploadFile/abc.jpeg"]
        }],
        "authorization": ["uploadFile/abc.jpeg"],
        "sourceFunds": ["1","2"],
        "paymentPurpose": ["0","1"],
        "riskCountryTransaction": "0",
        "riskCountries": [{
            "name": "ada",
            "country": "US"
        }],
        "addMaterial": "0",
        "reMaterial": {
            "financialStatements": [],
            "questionnaire": [],
            "bestCustomer": [{
                "name": "",
                "country": ""
            }],
            "bestPartner": [{
                "name": "",
                "country": ""
            }]
        },
	    "callBackUrl": "http://www.baidu.com"
    }
```

**3 请求参数**

| 名称        | Json标签              | 类型        | 属性  | 取值说明                                                     |
|-----------| --------------------- | ----------- |-----|----------------------------------------------------------|
| 入网邮箱      | email           | string(255) | M   | 入网邮箱                                                     |
| 手机区号      | phoneAreaCode   | string(10)  | O   | 手机号区号  默认86                                              |
| 手机号       | phoneNum       | string(32) | M   | 入网手机号                                                    |
| 推荐渠道      | referralChannel  | string(64) | O   | 注册推荐渠道                                                   |
| 推荐码       | recommender         | string(10)   | O   | 入网推荐人编码,根据当时OTT介绍人获取                                     |
| 商户注册国家    | countryCode     | string(2) | M   | 注册国家 iso 二字码                                             |                                                        |
| 商户英文名     | merNameEn | string(255) | M   | 入网商户的英文名                                                 |
| 是否具有母公司   | parentRemark | string(2) | M   | 是否具有母公司 0：无 1：有                                          |
| 股权架构图     | ownerShipPath | `List<String>` | C   | 当具有母公司时，该值必传                                             |
| 母公司注册证明   | parentCertificate | `List<String>` | C   | 当具有母公司时，该值必传                                             |
| 母公司信息     | parentCompany | `List<companyInfo>` | C   | 当具有母公司时，该值必传                                             |
| 是否具有子公司   | branchRemark | String(2) | M   | 是否具有子公司或分公司 0：无 1：有                                      |
| 分公司/子公司信息 | branchCompany | `List<companyInfo>` | C   | 当有子公司或者分公司时必传                                            |
| 商户注册文件    | certificate | `List<String>` | M   | 商户注册证明，CN 提供营业执照，HK提供商业登记证 ，境外传公司注册证明                    | 
| 周年年报      | nnc1Path | `List<String>` | O   | 当公司属于境外时                                                 |
| 法团成立表     | nar1Path1 | `List<String>` | C   | 当公司为境外公司必传                                               |
| 公司章程      | mermorandum | `List<String>` | C   | 当公司为境外公司必传                                               |
| 客户身份      | customerIdentity | String(4) | M   | 入网客户的身份 [参数详见6.1.10字段说明](#6-1-10-customeridentity) |
| 客户个人证件    | customerId | `List<personInfo>` | M   | 客户的身份证件照                                                 |
| 持股25%以上股东 | shareholder | `List<personInfo>` | M   | 持股25%以上股东的信息                                             |
| 公司董事      | director | `List<personInfo>` | C   | 公司董事信息，非CN国家必传                                           |
| 法人        | legalPerson | `List<personInfo>` | C   | 法人信息，国家为CN时必传                                            |
| 董事会议授权书   | authorization | `List<String>` | M   | 董事会议授权书                                                  |
| 资金来源      | sourceFunds | `List<String>` | M   | 资金主要来源 [参数详见6.1.8字段说明](#6-1-8-sourcefunds)         |
| 付款目的      | paymentPurpose | `List<String>` | M   | 付款主要目的 [参数详见6.1.9字段说明](#6-1-9-paymentpurpose)      |
| 风险交易国家    | riskCountryTransaction | String(2) | M   | 0：无 1：有 是否有伊朗、朝鲜、古巴地区有任何直接或间接的业务                         |
| 风险国家信息    | riskCountries | `List<companyInfo>` | C   | 当有和以上风险国家企业交易时，提供企业信息                                    |
| 是否为补充请求   | addMaterial | String(2) | O   | 0：否 1：是 当回调code为80000时，需要请求加上补充材料                        |
| 补充材料      | reMaterial | `reMaterial` | O   | 回调code为80000时，需要传参                                       |
| 回调地址      | callBackUrl | String(255) | M   | 用于接收商户入网结果                                               |

**reMaterial**

| 名称                    | Json标签  | 类型                  | 属性  | 取值说明                |
|-----------------------|---------|---------------------|-----|---------------------|
| 财务报表或公司税务申报表/完税证明     | financialStatements    | `List<String>`      | M   | 财务报表或公司税务申报表/完税证明   |
| 调查表                   | questionnaire | `List<String>`        | M   | 调查表                 |
| 表现最好的3家客户             | bestCustomer | `List<companyInfo>` | M   | 表现最好的3家企业信息         |
| 表现最好的3家供应商/合作伙伴公司     | bestPartner | `List<companyInfo>` | M   | 表现最好的3家供应商/合作伙伴公司信息 |

**personInfo**

| 名称     | Json标签 | 类型           | 属性  | 取值说明            |
|--------| -------- |--------------|-----|-----------------|
| 证件类型   |    type    | String(2)    | M   | 证件类型 0 身份证 1 护照 |
| 证件签发国家 |    issuPlace    | String(2)    | M   | 国家ISO 二字码       |
| 证件文件   |     certificates   | List<String> | M   | 证件sftp地址        |


**companyInfo**

| 名称      | Json标签  | 类型         | 属性  | 取值说明   |
|-----------|---------|------------|-----|--------|
| 公司名称    | name    | String(64) | M   | 公司注册名称 |
| 公司注册国家  | country | String (2) | M   | 公司所在国家 |


> 返回示例:

```json
{
        "bizFlow":"210622162803810002",
        "status": "ACCEPT",
        "code":"S00001",
        "message":"ACCEPT"
}
```
**4 响应字段**

| 名称       | Json标签 | 类型        | 属性 | 取值说明                                                          |
| ---------- | -------- | ----------- | ---- | ----------------------------------------------------------------- |
| 业务流水号 | bizFlow  | string(32)  | M    | 入网申请唯一订单号                                                |
| 状态 | status  | string(6)  | M    | 申请状态码 ACCEPT:接受成功，等待回调                                              |
| 结果码     | code     | string(6)   | M    | 响应结果代码，S00001 代表已接收成功，<br/>等待OTTPAY HK审核后回调 |
| 结果描述   | message  | string(255) | M    | 响应描述                                                          |




###  5.1.2 商户入网结果通知

**1 功能描述**

|          |                                                                                                                                                               |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 交易代码 | TP2004                                                                                                                                                        |
| 功能名称 | 商户入网结果通知                                                                                                                                              |
| 功能描述 | 商户入网结果异步通知                                                                                                                                          |
| 调用方式 | 通知接口                                                                                                                                                      |
| 调用流程 | --                                                                                                                                                            |
| 应用场景 | [商户入网信息完善](#5-1-1)发起成功且交易处理完毕后，<br/>将根据[商户入网信息完善](#5-1-1)参数内的回调Url进行回调通知最终结果。 |

<aside class="success">
本通知将按照间隔时间渐长的方式持续通知24小时.<br>商户应当以http 200返回，若通知持续时间结束仍未正常返回，则不再通知。
</aside>

**2 请求地址**

**Url：** [商户入网信息完善](#5-1-1)中的 **callbackUrl**

**Method：** `POST`

> 请求示例:

```json
{
        "bizFlow":"87200408378515100071",
        "code":"S00000",
        "message":"SUCCESS",
        "merchantNo":"005703100153",
        "merNameEn":"Demo Company Limited"
}
```
**3 请求字段**

| 名称         | Json标签      | 类型        | 属性 | 取值说明                          |
| ------------ | ------------- | ----------- | ---- | --------------------------------- |
| 业务流水号   | bizFlow       | string(32)  | M    | 入网申请唯一订单号                |
| 结果码       | code          | string(6)   | M    | 响应结果代码，S00000 代表入网成功 |
| 结果描述     | message       | string(255) | M    | 响应描述                          |
| 商户号       | merchantNo    | string(32)  | M    | 商户号，为商户的唯一标识号码      |
| 商户英文名称 | merNameEn     | string(255) | M    | 商户英文名称                      |
| 授权码       | authorizeCode | string(32)  | M    | 授权码                            |



## 5.2 授权
### 5.2.1 申请授权
**1 功能描述**

|          |                                                                |
| -------- |----------------------------------------------------------------|
| 交易代码 | TP9001                                                         |
| 功能名称 |申请授权                                                   |
| 功能描述 | 【待补充】                                                  |
| 调用方式 | 实时接口                                                           |
| 调用流程 | --                                                             |
| 应用场景 | 【【待补充】】 |


**2 请求地址**

**Url：** `https://{baseUrl}/api/TP9001`

**Method：** `POST`

> 请求示例:

```json
{
        "redirectUrl":"xxxxxxxxxxxxx",
        "merchantNo":"005703100153"
}
```    


**3 请求字段**

| 名称                     | Json标签              | 类型        | 属性 | 取值说明                                                                     |
| ------------------------ | --------------------- | ----------- | ---- | ---------------------------------------------------------------------------- |
| 重定向URL                   | redirectUrl               | string(255)  | M    | 重定向 url，仅接受 https url号                                                                       |
| 商户编号             |  merchantNo   | string(255) | M    | 代理商的商户号                                                                |



> 返回示例:

```json
{
     "authorizeCode": "e10adc3949ba59abbe56e057f20f883e"
 
}
```

**4 响应字段**


| 名称       | Json标签 | 类型        | 属性 | 取值说明                                                          |
| ---------- | -------- | ----------- | ---- | ----------------------------------------------------------------- |
| 授权码 | authorizeCode  | string(32)  | M    | 授权码                                                |



### 5.2.2 申请token
【待补充】

**1 功能描述**

|          |                                                                |
| -------- |----------------------------------------------------------------|
| 交易代码 | TP9002                                                         |
| 功能名称 |申请token                                                  |
| 功能描述 | 【待补充】                                                  |
| 调用方式 | 实时接口                                                           |
| 调用流程 | --                                                             |
| 应用场景 | 【【待补充】】 |


**2 请求地址**

**Url：** `https://{baseUrl}/api/TP9002`

**Method：** `POST`

> 请求示例:

```json
{
    "authorizeCode": "e10adc3949ba59abbe56e057f20f883e"
}
```    


**3 请求字段**

| 名称                     | Json标签              | 类型        | 属性 | 取值说明                                                                     |
| ------------------------ | --------------------- | ----------- | ---- | ---------------------------------------------------------------------------- |
| 授权码                   |  authorizeCode               | string(32)  | M    | 授权码                                                            |



> 返回示例:

```json
{
     "accessToken": "7c4a8d09ca3762af61e59520943dc26494"
 
}
```

**4 响应字段**


| 名称       | Json标签 | 类型        | 属性 | 取值说明                                                          |
| ---------- | -------- | ----------- | ---- | ----------------------------------------------------------------- |
| 授权token | accessToken  | string(32)  | M    | 授权 Token(目前 Token 永久有效)                                                |



## 5.3 收款

### 5.3.1 VA开户申请

**1 功能描述**

|          |                                              |
| -------- | -------------------------------------------- |
| 交易代码 | TP1011                                       |
| 功能名称 | VA开户申请                         |
| 功能描述 | 商户发起VA开户申请，等待OTT审核后，商户可通过VA查询接口查询具体VA账户信息                 |
| 调用方式 | 异步接口                                     |
| 调用流程 | --                                           |
| 应用场景 | 商户发起VA开户申请 |

**2 请求地址**

**Url：** `https://{baseUrl}/api/tp1011`

**Method：** `POST`

> 请求示例:

```json
{
        "merOrderNo":"150",
        "bankType":"00"
}
```                                                                 

**3 请求字段**

| 名称                     | Json标签              | 类型        | 属性 | 取值说明                                                                     |
| ------------------------ | --------------------- | ----------- | ---- | ---------------------------------------------------------------------------- |
| 商户订单号                   | merOrderNo               | string(32)  | M    | 商户自定义的唯一订单号                                                                       |
| 开户银行             | bankType   | string(2) | M    | 开户银行选择                                                                |


> 返回示例:

```json
{
        "bizFlow": "70210415775519090003",
        "status": "ACCEPT"
}
```

**4 响应字段**


| 名称       | Json标签 | 类型        | 属性 | 取值说明                                                          |
| ---------- | -------- | ----------- | ---- | ----------------------------------------------------------------- |
| 业务流水号 | bizFlow  | string(32)  | M    | OTT侧唯一业务订单号                                                |
| 结果状态     | status     | string(6)   | M    | 结果状态 ACCEPT:接收成功 FAIL：失败 |



### 5.3.2 VA开户查询

**1 功能描述**

|          |                                                    |
| -------- | -------------------------------------------------- |
| 交易代码 | TP3012                                             |
| 功能名称 | VA开户查询接口                                |
| 功能描述 | VA开户查询接口，提交VA申请后，通过此接口查询账户具体信息                                   |
| 调用方式 | 实时接口                                           |
| 调用流程 | --                                                 |
| 应用场景 | VA开户查询接口 |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3012`

**Method：** `POST`

> 请求示例:

```json
{
    "bizFlow":"7123498239859278274"
}
```                                             
**3 请求字段**


| 名称         | Json标签   | 类型   | 属性 | 取值说明                             |
| ------------ | ---------- | ------ | ---- | ------------------------------------ |
| 查询起始时间 | startTime  | Long(13)   | O    | Unix13位时间戳，查询开始时间，闭区间 |
| 查询结束时间 | endTime    | Long(13)   | O    | Unxi13位时间戳，查询结束时间，闭区间 |
| OTT侧业务订单号       | bizFlow    | String(32)   | O    | VA开户时返回的订单号                               |
| 商户订单号   | merOrderNo | String(32) | O    | 商户订单号                           |

<aside class="success">
若startTime与endTime没填，则bizFlow和merOrderNo中必填其一。若bizFlow和merOrderNo都没填，则startTime与endTime为必填，且间隔不能超过24小时。根据startTime和endTime的查询，最多显示100条。
</aside>       

> 返回示例:

```json
{
"list": [
            {
                "merOrderNo":"8793478374",
                "bizFlow":"7123498239859278274",
                "vaInfos": [
                    {
                        "accountName":"OTT-FinalTest",
                        "accountNo":"7983648348",
                        "swiftCode":"DHBKHKHH",
                        "bankName":"China Bank(Hong Kong) Limited",
                        "bankAddress":"11th Floor, The Center, 99 Queen’s Road Central, Central, Hong Kong",
                        "area":"Hong Kong, CHINA",
                        "bankCode":"016",
                        "branchCode":"478",
                        "currency":"SGD|NZD|JPY|HKD|GBP|EUR|CAD|AUD|USD|CNY|CHF|SEK|DKK|NOK|EGP",
                        "status":"OPENING",
                        "remark":"",
                        "createTime":"1622453954000",
                        "updateTime":"1622453954000"
                    }
                ]
            }
        ] 
}
```

**4 响应字段**



| 名称     | Json标签     | 类型       | 属性 | 取值说明 |
| -------- | ------------ | ---------- | ---- | -------- |
| 商户订单号 | merOrderNo | String(32)  | M    | 商户订单号 |
| OTT侧业务订单号    | bizFlow    | String(32)   | M    | VA开户时返回的订单号   |
| VA详细信息     | vaInfos         | List | M    | VA详细信息 |



**VaInfo 的字段**

| 名称             | Json标签         | 类型          | 属性 | 取值说明                   |
| ---------------- | ---------------- | ------------- | ---- | -------------------------- |
| VA账户名称       | accountName       | string(255)    | O    | VA账户名称 |
| VA账户号             | accountNo         | string(64)     | O    | VA账户号  |
| SwiftCode             | swiftCode           | string(11) | O    | 银行的SwiftCode                   |
| 银行名称     | bankName  | string(128)    |   O  | 银行名称               |
| 银行地址    | bankAddress    | string(255)    | O   | 银行地址         |
| 国家/地区         | area         | string(64)    | O    | 国家/地区               |
| 银行Code         | bankCode      | string(12)   | O    | 银行Code             |
| 分行号       | branchCode        | string(12)    | O   | 分行号       |
| 支持币种       | currency    | string(255)    | O    | 支持币种，多币种之间按照|分隔                 |
| VA账户状态     | status           | string(8)     | M    | VA账户状态, ON:启用，OFF：禁用/拒绝 OPENING：开户中               |
| 备注       | remark             | string(8)     | O    | 当为OFF时，会展示具体禁用/拒绝原因                 |
| 申请时间     | createTime       | long          | M    | VA开户的申请时间               |
| 修改时间     | updateTime       | long          | M    | VA开户的修改时间               |


### 5.3.3 贸易收款到账通知

**1 功能描述**

| 交易代码 | TP2007                                                                                                                                   |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 功能名称 | 贸易收款到账通知                                                                                                                     |
| 功能描述 | 贸易收款到账通知                                                                                                                     |
| 调用方式 | 通知接口                                                                                                                                 |
| 调用流程 | --                                                                                                                                       |
| 应用场景 | 在商户的VA子账户收款收到后，OTTPAYHK会向商户发送贸易收款资金到账的通知 |

<aside class="success">
本通知将按照间隔时间渐长的方式持续通知24小时.<br>商户应当以http 200返回，若通知持续时间结束仍未正常返回，则不再通知。   
</aside>

**2 请求地址**

**Url：** 【待补充】**callbackUrl**

**Method：** `POST`

> 请求示例:

```json
{
    "flowNo":"624348793478374",
    "receiveAmount": 10000.00,
    "receiveCurrency": "USD",
    "vaAccount": "789432134",
    "senderName": "ERUIEG Limited",
    "senderAccount": "84956984598234923",
    "receiveTime":"1624358032"
}
```
**3 请求字段**

| 名称       | Json标签 | 类型   | 属性 | 取值说明                                        |
| ---------- | -------- | ------ | ---- | ----------------------------------------------- |
| 到账流水号 | flowNo  | string(32) | M    | 贸易收款到账唯一流水号     |
| 到账金额       | receiveAmount | decimal(18,2) | M    | VA到账金额                    |
| 到账币种       | receiveCurrency | string(3) | M    | VA到账币种                     |
| 入账VA账户号       | vaAccount  | string(16) | M    | 入账的VA账户号        |
| 付款方名称       | senderName | string(64) | O    | 付款方名称                    |
| 付款方账号       | senderAccount | string(32) | O    | 付款方账号                   |
| 入账时间       | receiveTime | string(10) | M    | 入账时间，10位unix时间戳                |



### 5.3.4 贸易收款VA入账查询接口

**1 功能描述**

|          |                                                    |
| -------- | -------------------------------------------------- |
| 交易代码 | TP3015                                             |
| 功能名称 | 贸易收款VA入账查询接口                               |
| 功能描述 | 贸易收款VA入账查询接口                                   |
| 调用方式 | 实时接口                                           |
| 调用流程 | --                                                 |
| 应用场景 | 可以查询VA账户具体的到账流水 |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3015`

**Method：** `POST`

> 请求示例:

```json
{
       "flowNo":"62291060316483300005"
}
```                                             

**3 请求字段**


| 名称         | Json标签   | 类型   | 属性 | 取值说明                             |
| ------------ | ---------- | ------ | ---- | ------------------------------------ |
| 查询起始时间 | startTime  | Long(13)   | O    | Unix13位时间戳，查询开始时间，闭区间 |
| 查询结束时间 | endTime    | Long(13)   | O    | Unxi13位时间戳，查询结束时间，闭区间 |
| VA入账订单号 | flowNo  | string(32)          | O    | VA入账订单号    |

<aside class="success">
startTime与endTime，间隔不能超过24小时。根据startTime和endTime的查询，最多显示100条。若startTime和endTime未填写，则bizFlow为必填。
</aside>       

> 返回示例:

```json
{
  "list":
        [
           {
               "flowNo":"624348793478374",
               "receiveAmount": 10000.00,
               "receiveCurrency": "USD",
               "vaAccount": "789432134",
               "senderName": "ERUIEG Limited",
               "senderAccount": "84956984598234923",
               "receiveTime":"1624358032"
           },
           {
               "flowNo":"6245498990028374",
               "receiveAmount": 20000.00,
               "receiveCurrency": "EUR",
               "vaAccount": "789432452",
               "senderName": "ERUIEGdw Limited",
               "senderAccount": "84950094592334923",
               "receiveTime":"1622138032"
           }
        ]
}
```
**4 响应字段**


| 名称       | Json标签 | 类型   | 属性 | 取值说明                                        |
| ---------- | -------- | ------ | ---- | ----------------------------------------------- |
| 交易流水号 | flowNo  | string(32) | M    | 贸易收款到账唯一流水号     |
| 到账金额       | receiveAmount | decimal(18,2) | M    | VA到账金额                    |
| 到账币种       | receiveCurrency | string(3) | M    | VA到账币种                     |
| 入账VA账户号       | vaAccount  | string(16) | M    | 入账的VA账户号        |
| 付款方名称       | senderName | string(64) | O    | 付款方名称                    |
| 付款方账号       | senderAccount | string(32) | O    | 付款方账号                   |
| 入账时间       | receiveTime | string(10) | M    | 入账时间，10位unix时间戳                |



### 5.3.5 贸易订单申请

**1 功能描述**

| 交易代码 | TP1012                                                                                                                                                                           |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 功能名称 | 商户创建贸易的订单合同                                                                                                                                                                         |
| 功能描述 | 收集订单信息                                                                                                                                                       |
| 调用方式 | 实时接口                                                                                                                                                                         |
| 调用流程 | 商户发送申请，ottpay返回合同订单号 |
| 应用场景 | 商户收集订单信息以及合规材料，提供商户新建贸易订单，并提供合同号  

**2 请求地址**

  **Url：** `https://{baseUrl}/api/tp1012`
  
  **Method：** `POST`

> 请求示例:

```json
 {
    "callbackUrl":"http://www.baidu.com",
    "merOrderNo":"23134141421414",
    "currency":"CNY",
    "amount":"7010.20",
    "tradeType": "00",
    "buyerName": "TX",
    "buyerArea":"中国",
    "goodsList":[
      {
          "orderName": "apple",
          "orderNum":"3"
      }
    ],
    "transcationDate":"2021-06-01",
    "transcationCert":["/src/iiii/a.png","/src/iiii/b.pdf","/src/iiii/c.png"],
    "logStatus":"0",
    "logNo":"983222231788743",
    "logCompany":"国际贸易物流公司",
    "annexUrl":["/src/iiii/a.png","/src/iiii/b.pdf","/src/iiii/c.png"],
    "serviceTrade": {
              "serviceCondition": "",
              "proveUrl": [],
              "conditionDate": "2021-09-02"
        }
}
```
**3 请求字段**

| 名称           | Json标签        | 类型              | 属性 | 取值说明                                                          |
| -------------- | --------------- | ----------------- | ---- | ----------------------------------------------------------------- |
| 回调接口地址   | callbackUrl     | string(60)        | M    | 用来通知订单状态                                                          |
| 商户唯一订单号 | merOrderNo      | string(32)        | M    | 商户唯一订单号  |
| 订单币种       | currency        | string(3)         | M    | 订单币种                                                          |
| 订单总金额     | amount          | Decimal(18,2)     | M    | 订单总金额                                                          |
| 贸易类型       | tradeType       | string(2)         | M    | 贸易类型 默认：00-货物贸易 01-服务贸易                                                        |
| 采购方名称     | buyerName       | string(64)        | M    | 采购方名称                                                         |
| 采购方所属地区 | buyerArea       | string(64)        | M    | 采购方所属地区                                                          |
| 物品信息       | goodsList       | `List<goodsList>` | M    | 物品信息 物品数量不超过10个                                                        |
| 交易日期       | transcationDate | string(10)        | M    | 交易日期 格式：yyyy-MM-dd                                                          |
| 交易凭证       | transcationCert | `Array`           | M    | 多个凭证文件地址数组  (文件大小不超过20M)                                                     |
| 物流状态       | logStatus       | string(1)         | O    | 当贸易类型为00-货物贸易时必填 0-未发货 1-已发货 如果是已发货logNo、logCompany、annexUrl三个字段必填                                                          |
| 物流单号       | logNo           | string(64)        | O    | 物流单号                                                       |
| 物流公司名称   | logCompany      | string(128)       | O    | 物流公司名称                                                       |
| 附件           | annexUrl        | `Array`           | O    | 多个附件文件地址数组 (文件大小不超过20M)                                                    |                                                      |
| 服务贸易信息   | serviceTrade    | `Object`      | O    | 当贸易类型为01-服务贸易时必填                                                    |

 **goodsList**
 
| 名称           | Json标签 | 类型        | 属性 | 取值说明                                                          |
| -------------- | -------- | ----------- | ---- | ----------------------------------------------------------------- |
| 交易物品名称   | orderName| string(64)  | M    | 交易物品名称                                                          |
| 交易物品数量   | orderNum | string(10)  | M    | 交易物品数量                                                          |

**serviceTrade**

| 名称           | Json标签         | 类型        | 属性 | 取值说明                                                          |
| -------------- | ---------------- | ----------- | ---- | ----------------------------------------------------------------- |
| 服务贸易状态   | serviceCondition | string(1)   | O    | 服务贸易完成状态 0-未完成 1-已完成                                                          |
| 证明文件       | proveUrl         | `Array`     | O    | 当服务贸易状态为1 此项必填                                                          |
| 预计完成时间   | conditionDate    | string(10)  | O    | 当服务贸易状态为0 此项必填  格式 yyyy-MM-dd                                            |


> 响应示例:

```json
{
     "contractNo": "2012042197287616"
}
```
**4 响应字段**

| 名称           | Json标签  | 类型        | 属性 | 取值说明                                                          |
| -------------- | --------- | ----------- | ---- | ----------------------------------------------------------------- |
| 贸易订单号     | contractNo| string(32)  | M    | 贸易订单号（唯一）                                                     |



### 5.3.6 贸易订单申请结果通知

**1 功能描述**

| 交易代码   | TP2008                                                                                                                                                            |
| --------   | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 功能名称   | 回传贸易订单结果状态通知                                                                                                                                              |
| 功能描述   | 运营审核后通知商户订单申请结果                                                                                                                                        |
| 调用方式   | 通知接口                                                                                                                                                          |
| 调用流程   | --                                                                                                                                                                |
| 应用场景   | [5.1.13 贸易订单申请]发起成功，根据回调Url进行回调通知最终结果。 |

<aside class="success">
本通知将按照间隔时间渐长的方式持续通知24小时.<br>商户应当以http 200返回，若通知持续时间结束仍未正常返回，则不再通知。<br>商户应当自行通过 [5.3.4 贸易收款VA入账查询接口]查询交易结果。
</aside>

**2 请求地址**

**Url：** [5.3.5 贸易订单申请]中的 **callbackUrl**

**Method：** `POST`

> 请求示例:

```json
{
    "contactNo": "20123910029181818",
    "merOrderNo": "1401203219391312",
    "status": "SUCC",
    "message": "成功"
}
```
**3 请求字段**

| 名称         | Json标签   | 类型      | 属性 | 取值说明                     |
| ------------ | ---------- | --------- | ---- | ---------------------------- |
| 贸易订单编号 | contactNo  | string(32)| M    | 贸易订单编号 (唯一)                                                                |
| 商户订单号   | merOrderNo | string(32)| M    | 商户订单号(唯一)                 |
| 状态         | status     | string(8) | M    | 'ACCEPT-处理中 SUCC-成功 FAIL-失败' |
| 结果描述     | message    | string(64)| M    | 交易结果描述               |
 



### 5.3.7 贸易订单申请信息查询

**1 功能描述**

|          |                                                    |
| -------- | -------------------------------------------------- |
| 交易代码 | TP3013                                             |
| 功能名称 | 贸易合同结果信息查询                               |
| 功能描述 | 提供商户查询贸易合同创建状态                       |
| 调用方式 | 实时接口                                           |
| 调用流程 | --                                                 |
| 应用场景 | 商户需要查询订单合同的状态                         |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3013`

**Method：** `POST`

> 请求示例:

```json
{
       "startTime":"168419019000",
       "endTime":"168419019000",
       "contractNo":"62291060316483300005",
       "merOrderNo":"23455560316483300005"
}
```                                             

**3 请求字段**


| 名称         | Json标签   | 类型   | 属性 | 取值说明                             |
| ------------ | ---------- | ------ | ---- | ------------------------------------ |
| 查询起始时间 | startTime  | Long(13)   | O    | Unix13位时间戳，查询开始时间，闭区间 |
| 查询结束时间 | endTime    | Long(13)   | O    | Unxi13位时间戳，查询结束时间，闭区间 |
| 贸易合同号   | contractNo | string(32) | O    | [5.1.13 贸易订单申请]返回贸易合同号    |
| 订单号       | merOrderNo | string(32) | O    | 商户提供的订单号        |

<aside class="success">
startTime与endTime，间隔不能超过24小时。根据startTime和endTime的查询，最多显示100条。若startTime和endTime未填写，则contractNo为必填。
</aside>       

> 响应示例:

```json
{
   "contractList":[
        {
            "contractNo":"2120319391838111181",
            "status":"SUCC",
            "message":"成功",
            "merOrderNo":"23134141421414",
            "orderNo":"2021062819217",
            "currency":"CNY",
            "amount":"7010.20",
            "tradeType": "00",
            "buyerName": "TX",
            "buyerArea":"中国",
            "goodsList":[
                {
                    "orderName": "apple",
                    "orderNum":"3"
                }
            ],
            "transcationDate":"2021-06-01",
            "transcationCert":["/src/iiii/a.png","/src/iiii/b.pdf","/src/iiii/c.png"],
            "logStatus":"0",
            "logNo":"983222231788743",
            "logCompany":"国际贸易物流公司",
            "annexUrl":["/src/iiii/a.png","/src/iiii/b.pdf","/src/iiii/c.png"],
            "serviceTrade": {
                "serviceCondition": "0",
                "proveUrl": [],
                "conditionDate": "2021-09-02"
            }

        }
    ]
}
```

**4 响应字段**


| 名称        | Json标签        | 类型                 | 属性 | 取值说明                                                          |
| ----------- | --------------- | -------------------- | ---- | ----------------------------------------------------------------- |
| 贸易订单    | contractList    | `List<contractList>` | M    | 贸易订单集合    |


**contractList**

| 名称           | Json标签        | 类型              | 属性 | 取值说明                                |
| -------------- | --------------- | ----------------- | ---- | ------------------------------------|
| 商户唯一订单号 | merOrderNo      | string(32)        | M    | 商户唯一订单号                             |
| 订单币种       | currency        | string(3)         | M    | 订单币种                                |
| 订单总金额     | amount          | Decimal(18,2)     | M    | 订单总金额                               |
| 贸易类型       | tradeType       | string(2)         | M    | 贸易类型 默认：00-货物贸易                     |
| 采购方名称     | buyerName       | string(64)        | M    | 采购方名称                               |
| 采购方所属地区 | buyerArea       | string(64)        | M    | 采购方所属地区                             |
| 物品信息       | goodsList       | `List<goodsList>` | M    | 物品信息 物品数不超过10个                      |
| 交易日期       | transcationDate | string(10)        | M    | 交易日期 格式：yyyy-MM-dd                       |
| 交易凭证       | transcationCert | `Array`           | M    | 多个凭证文件地址数组 (文件大小不超过20M)                  |
| 物流状态       | logStatus       | string(1)         | O    | 0-未发货 1-已发货                         |
| 物流单号       | logNo           | string(64)        | O    | 物流单号                                |
| 物流公司名称   | logCompany      | string(64)        | O    | 物流公司名称 |
| 物流附件       | annexUrl        | `Array`           | O    | 物流附件 (文件大小不超过20M) |
| 服务贸易信息   | serviceTrade    | `Object`          | O    | 服务贸易信息 |
| 贸易订单号     | contractNo      | string(32)        | M    | 贸易订单号（唯一）                           |
| 贸易订单状态   | status          | string(8)         | M    | 贸易订单状态 ACCEPT-处理中 SUCC-成功 FAIL-失败|
| 查询结果描述   | message         | string(128)       | M    | 查询结果描述|

**serviceTrade**

| 名称           | Json标签        | 类型            | 属性 | 取值说明                                                          |
| -------------- | --------------- | --------------- | ---- | ----------------------------------------------------------------- |
| 服务贸易状态   | serviceCondition| string(1)       | O    | 服务贸易完成状态 0-未完成 1-已完成                                          |
| 证明文件       | proveUrl        | `Array`         | O    | 证明文件路径 serviceCondition 为0时必填                                       |
| 预计完成时间   | conditionDate   | string(10)      | O    | serviceCondition 为1时必填 格式"yyyy-MM-dd"                                     |



### 5.3.8 收款流水和贸易订单关联

**1 功能描述**

|          |                                              |
| -------- | -------------------------------------------- |
| 交易代码 | TP1013                                       |
| 功能名称 | 收款流水和贸易订单关联                            |
| 功能描述 | 收款流水和贸易订单关联                   |
| 调用方式 | 实时接口                                     |
| 调用流程 | --                                           |
| 应用场景 | 商户的贸易收款订单被审核通过后，将收款流水和贸易订单做关联 |

**2 请求地址**

**Url：** `https://{baseUrl}/api/tp1013`

**Method：** `POST`

> 请求示例:

```json
{
        "contactNo":"62291060316483300005",
        "flowNo":"63291062211570000002",
        "callbackUrl":"https://xxxxx.xxxx.com/callback/inAcctNoticeUrl"
}
```          
**3 请求字段**

| 名称                     | Json标签              | 类型        | 属性 | 取值说明                                                                     |
| ------------------------ | --------------------- | ----------- | ---- | ---------------------------------------------------------------------------- |
| 贸易订单编码              | contactNo               | string(32)          | M    | 贸易订单编码，tp2008返回                                                                     |
| 收款流水编码              | flowNo               | string(32)          | M    | 收款流水编码，tp3015返回                                         |
| 入账通知地址              | callbackUrl            | string(255) | M    | 贸易收款入账成功后的通知地址 |

                                                       

> 返回示例:

```json
{
       "bizFlow":"652362763878"
}
```

**4 响应字段**


| 名称       | Json标签 | 类型        | 属性 | 取值说明                                                          |
| ---------- | -------- | ----------- | ---- | ----------------------------------------------------------------- |
| 业务流水号 | bizFlow  | string(32)  | M    | OTT侧唯一业务订单号                                                |



### 5.3.9 收款流水和贸易订单关联结果通知

**1 功能描述**

| 交易代码    | TP2009                                                                                                                                                            |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 功能名称  | 收款流水和贸易订单关联结果通知                                                                                                                                              |
| 功能描述   | 收款流水和贸易订单关联后，给商户发的通知                                                                                                                                        |
| 调用方式   | 通知接口                                                                                                                                                          |
| 调用流程   | --                                                                                                                                                                |
| 应用场景   | [5.3.8 收款流水和贸易订单关联]发起成功且交易处理完毕后，<br/>将根据[5.3.8 收款流水和贸易订单关联]参数内的回调Url进行回调通知最终结果。 |

<aside class="success">
本通知将按照间隔时间渐长的方式持续通知24小时.<br>商户应当以http 200返回，若通知持续时间结束仍未正常返回，则不再通知。<br>商户应当自行通过 [5.3.10 收款流水和贸易订单关联查询接口]查询接口查询交易结果。
</aside>

**2 请求地址**

**Url：** [5.3.8 收款流水和贸易订单关联]中的 **callbackUrl**

**Method：** `POST`

**3 请求字段**

| 名称         | Json标签       | 类型   | 属性 | 取值说明                     |
| ------------ | -------------- | ------ | ---- | ---------------------------- |
| 贸易订单编码   | contactNo               | string(32)          | M    | 贸易订单编码                                                                   |
| 收款流水编码   | flowNo               | string(32)          | M    | 收款流水编码 |
| 入账币种      | currency        | string | M    | 入账币种，3位标准货币代码  |
| 入账金额      | amount   | decimal(18,2) | M    | 收款金额                     |
| 手续费币种    | feeCurty    | String | M    | 手续费币种，3位标准货币代码                    |
| 手续费金额    | feeAmt           | decimal(18,2) | M    | OTT PAY收取手续费                        |
| 入账时间      | approveTime        | bigInt(13) | M    | 入账时间戳(毫秒) |
| 状态   | status    | string(2) | M    | '02-通过 03-驳回' |
| 结果描述         | message          | string(64)    | M    | 交易结果描述     



### 5.3.10 收款流水和贸易订单关联查询

**1 功能描述**

|          |                                                    |
| -------- | -------------------------------------------------- |
| 交易代码 | TP3014                                             |
| 功能名称 | 收款流水和贸易订单关联查询接口                                |
| 功能描述 | 提交收款流水和贸易订单关联申请后，通过此接口查询贸易收款是否入账                                   |
| 调用方式 | 实时接口                                           |
| 调用流程 | --                                                 |
| 应用场景 | 提交收款流水和贸易订单关联申请后（TP1013），通过此接口查询贸易收款是否入账 |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3014`

**Method：** `POST`

> 请求示例:

```json
{
       "contactNo":"62291060316483300005",
       "flowNo":"63291062211570000002"
}
```                                             
**3 请求字段**


| 名称         | Json标签   | 类型   | 属性 | 取值说明                             |
| ------------ | ---------- | ------ | ---- | ------------------------------------ |
| 查询起始时间 | startTime  | Long(13)   | O    | Unix13位时间戳，查询开始时间，闭区间 |
| 查询结束时间 | endTime    | Long(13)   | O    | Unxi13位时间戳，查询结束时间，闭区间 |
| 贸易订单编码 | contactNo  | string(32)          | O    | 贸易订单编码，tp2008返回                                                                     |
| 收款流水编码 | flowNo   | string(32)          | O    | 收款流水编码，tp3015返回                                 |
| 业务流水号 | bizFlow  | string(32)  | O    | OTT侧唯一业务订单号，tp1013返回                                                |

<aside class="success">
若startTime与endTime，间隔不能超过24小时。根据startTime和endTime的查询，最多显示100条。
</aside>       


**4 响应字段**


| 名称     | Json标签     | 类型       | 属性 | 取值说明 |
| -------- | ------------ | ---------- | ---- | -------- |
| 信息集合 | relateList     | `List<ConfirmRelatetionReq>` | M    | --       |

**ConfirmRelatetionReq 字段：**

| 名称     | Json标签     | 类型       | 属性 | 取值说明 |
| -------- | ------------ | ---------- | ---- | -------- |
| 贸易订单编码   | contactNo               | string(32)          | M    | 贸易订单编码                                                                   |
| 收款流水编码   | flowNo               | string(32)          | M    | 收款流水编码  |
| 入账币种      | currency        | string | M    | 入账币种，3位标准货币代码  |
| 入账金额      | amount   | decimal(18,2) | M    | 收款金额                     |
| 手续费币种    | feeCurty    | String | M    | 手续费币种，3位标准货币代码                    |
| 手续费金额    | feeAmt           | decimal(18,2) | O    | OTT PAY收取手续费                        |
| 入账时间      | approveTime        | bigInt(13) | M    | 入账时间戳(毫秒) |
| 状态   | status    | string(2) | M    | '01-审核中 02-通过 03-驳回' |
| 结果描述         | message          | string(64)    | M    | 交易结果描述               |


## 5.4 换汇

### 5.4.1 牌价查询

**1 功能描述**

|          |                            |
| -------- | -------------------------- |
| 交易代码 | TP1002                     |
| 功能名称 | 牌价查询                   |
| 功能描述 | 查询某币种的FX牌价         |
| 调用方式 | 实时接口                   |
| 调用流程 | --                         |
| 应用场景 | 在进行FX交易前，需要先询价 |

**2 请求地址**

**Url：** `https://{baseUrl}/api/tp1002`

**Method：** `POST`

> 请求示例:

 ```json
{
    "merOrderNo":"1734276289293",
    "sellCurrency":"USD",
    "buyCurrency":"CNY",
    "lockDirection":"SELL",
    "amount":"1000.00",
    "lockType":"T0"
}
```                       

**3 请求字段**

| 名称       | Json标签      | 类型       | 属性 | 取值说明                                                                 |
| ---------- | ------------- | ---------- | ---- | ------------------------------------------------------------------------ |
| 商户订单号 | merOrderNo    | String(32) | M    | 商户自定义的唯一订单号                                                   |
| 卖出币种   | sellCurrency  | String(3)  | O    | 卖出币种                                                                 |
| 买入币种   | buyCurrency   | String(3)  | M    | 买入币种                                                                 |
| 锁定方向   | lockDirection | String(4)  | M    | 锁定卖出或买入币种;传SELL则锁定卖出币种的金额，传BUY则锁定买入币种的金额 |
| 锁定金额   | amount        | String(20) | M    | 指定的FX金额                                                             |
| 锁汇类型   | lockType      | String(2)  | O    | 选填字段：目前支持可选T0、T1、T2                                             |

                                           
> 返回示例:

```json
{
    "sellCurrency":"USD",
    "buyCurrency":"CNY",
    "rate":"7.0102",
    "sellAmount":"1000.00",
    "buyAmount":"7010.20",
    "quoteId": 7843892398239,
    "expireTime": 1576560599598,
    "merOrderNo":"32894398349",
    "lockType":"T0"
}
```
**4 响应字段**


| 名称       | Json标签     | 类型       | 属性 | 取值说明                                                       |
| ---------- | ------------ | ---------- | ---- | -------------------------------------------------------------- |
| 卖出币种   | sellCurrency | String(3)  | M    | 卖出币种                                                       |
| 买入币种   | buyCurrency  | String(3)  | M    | 买入币种                                                       |
| 汇率       | rate         | String(18) | M    | 汇率报价                                                       |
| 卖出金额   | sellAmount   | String(18) | M    | 卖出金额                                                       |
| 买入金额   | buyAmount    | String(20) | M    | 买入金额                                                       |
| 报价ID     | quoteId      | Long       | M    | 报价ID                                                         |
| 报价有效期 | expireTime   | Long       | M    | unix时间戳，此次询价的有效时间。如若过了有效时间，此次询价作废 |
| 商户订单号 | merOrderNo   | String(32) | M    | 商户传入的订单号                                               |
| 锁汇类型   | lockType     | String(2)  | O    | 锁汇类型 T0、T1、T2                                                |


### 5.4.2 FX交易

**1 功能描述**

|          |                                                             |
| -------- | ----------------------------------------------------------- |
| 交易代码 | TP1003                                                      |
| 功能名称 | FX交易                                                      |
| 功能描述 | 根据询价后的牌价，发起FX交易                                |
| 调用方式 | 实时接口                                                    |
| 调用流程 | 在发起牌价查询接口后，根据所得到的quoteId，发起相应的FX交易 |
| 应用场景 | --                                                          |

**2 请求地址**

**Url：** `https://{baseUrl}/api/tp1003`

**Method：** `POST`

> 请求示例:

```json
{
    "quoteId": 7843892398239,
    "callbackUrl":"https://xxxx.xxxx.xxxx/xxxx/xxxx"
}

```
**3 请求字段**

| 名称    | Json标签    | 类型        | 属性 | 取值说明    |
| ------- | ----------- | ----------- | ---- | ----------- |
| 报价ID  | quoteId     | Long        | M    | 报价ID      |
| 回调url | callbackUrl | String(256) | M    | 回调通知Url |

                                                                   
> 返回示例:

```json
{
    "sellCurrency":"USD",
    "buyCurrency":"CNY",
    "rate":"7.0102",
    "sellAmount":"1000.00",
    "buyAmount":"7010.20",
    "quoteId": 7843892398239,
    "expireTime": 1576560599598,
    "merOrderNo":"32894398349",
    "lockType":"T0"
}
```
**4 响应字段**


| 名称       | Json标签     | 类型       | 属性 | 取值说明               |
| ---------- | ------------ | ---------- | ---- | ---------------------- |
| 卖出币种   | sellCurrency | String(3)  | M    | 卖出币种               |
| 买入币种   | buyCurrency  | String(3)  | M    | 买入币种               |
| 汇率       | rate         | String(18) | M    | 汇率报价               |
| 卖出金额   | sellAmount   | String(18) | M    | 卖出金额               |
| 买入金额   | buyAmount    | String(20) | M    | 买入金额               |
| 报价ID     | quoteId      | Long       | M    | 报价ID                 |
| 结果码     | code         | String     | M    | Fx交易结果码           |
| 结果描述   | message      | String     | M    | 交易结果描述           |
| 交易流水号 | bizFlow      | String(32) | M    | 对应Fx交易的唯一流水号 |
| 锁汇类型   | lockType     | String(2)  | O    | 锁汇类型 T0、T1        |



### 5.4.3 换汇历史交易查询

**1 功能描述**

| 交易代码 | TP3003                 |
| -------- | ---------------------- |
| 功能名称 | 换汇历史交易查询       |
| 功能描述 | 换汇历史交易查询       |
| 调用方式 | 实时接口               |
| 调用流程 | --                     |
| 应用场景 | 查询以往的换汇历史交易 |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3003`

**Method：** `POST`

**3 请求字段**


| 名称         | Json标签  | 类型 | 属性 | 取值说明                             |
| ------------ | --------- | ---- | ---- | ------------------------------------ |
| 查询起始时间 | startTime | Long | O    | Unix13位时间戳，查询开始时间，闭区间 |
| 查询结束时间 | endTime   | Long | O    | Unxi13位时间戳，查询结束时间，闭区间 |
| 报价ID       | quoteId   | Long | O    | 报价ID                               |

*说明： 若startTime与endTime没填，则quoteId为必填。若quoteId没填，则startTime与endTime为必填，且间隔不能超过24小时。*

                                                                   
> 返回示例:

```json
[
    {
        "sellCurrency":"USD",
        "buyCurrency":"CNY",
        "rate":"7.0102",
        "sellAmount":"1000.00",
        "buyAmount":"7010.20",
        "quoteId": 7843892398239,
        "code": "AR0021",
        "message":"not enough balance",
        "bizFlow":"983788743"
    },
    {
        "sellCurrency":"USD",
        "buyCurrency":"CNY",
        "rate":"7.0102",
        "sellAmount":"1000.00",
        "buyAmount":"7010.20",
        "quoteId": 7843892398240,
        "code": "S00000",
        "message":"success",
        "bizFlow":"983788743"
    }
]
```

**4 响应字段**

 接口返回对象为: **`List<ExchangeHistory>`**

**ExchangeHistory 字段：**

| 名称       | Json标签     | 类型       | 属性 | 取值说明           |
| ---------- | ------------ | ---------- | ---- | ------------------ |
| 卖出币种   | sellCurrency | String(3)  | M    | 卖出币种           |
| 买入币种   | buyCurrency  | String(3)  | M    | 买入币种           |
| 汇率       | rate         | String(18) | M    | 汇率报价           |
| 卖出金额   | sellAmount   | String(20) | M    | 卖出金额           |
| 买入金额   | buyAmount    | String(20) | M    | 买入金额           |
| 报价ID     | quoteId      | Int        | M    | 报价ID             |
| 结果码     | code         | String     | M    | Fx交易结果码       |
| 结果描述   | message      | String     | M    | 交易结果描述       |
| 业务流水号 | bizFlow      | String(32) | M    | 对应唯一业务流水号 |



### 5.4.4 FX交易结果通知

**1 功能描述**

|          |                                                                                                                                   |
| -------- | --------------------------------------------------------------------------------------------------------------------------------- |
| 交易代码 | TP2002                                                                                                                            |
| 功能名称 | FX交易结果通知                                                                                                                    |
| 功能描述 | Fx的交易结果异步通知                                                                                                              |
| 调用方式 | 通知接口                                                                                                                          |
| 调用流程 | --                                                                                                                                |
| 应用场景 | [5.4.2 Fx交易](#5-4-2-fx)发起成功且交易处理完毕后，<br/>将根据[5.4.2 Fx交易](#5-4-2-fx)参数内的回调Url进行回调通知最终结果。 |

<aside class="success">
 本通知将按照间隔时间渐长的方式持续通知24小时.<br>商户应当以http 200返回，若通知持续时间结束仍未正常返回，则不再通知。<br>商户应当自行通过 [5.4.3 换汇历史交易查询](#5-4-3)查询接口查询交易结果。
</aside>

**2 请求地址**

**Url：** [5.4.2 Fx交易](#5-4-2-fx)中的 **callbackUrl**

**Method：** `POST`

> 请求示例:

```json
 {
    "sellCurrency":"USD",
    "buyCurrency":"CNY",
    "rate":"7.0102",
    "sellAmount":"1000.00",
    "buyAmount":"7010.20",
    "quoteId": 7843892398239,
    "code": "AR0021",
    "message":"not enough balance",
    "bizFlow":"983788743"
}
```
**3 请求字段**

| 名称       | Json标签     | 类型       | 属性     | 取值说明     |
| ---------- | ------------ | ---------- | -------- | ------------ |
| 卖出币种   | sellCurrency | String(3)  | M        | 卖出币种     |
| 买入币种   | buyCurrency  | String(3)  | M        | 买入币种     |
| 汇率       | rate         | String(18) | M        | 汇率报价     |
| 卖出金额   | sellAmount   | String(20) | M        | 卖出金额     |
| 买入金额   | buyAmount    | String(20) | M        | 买入金额     |
| 报价ID     | quoteId      | Long       | M	   | 报价ID       |
| 结果码     | code         | String     | M        | Fx交易结果码 |
| 结果描述   | message      | String     | M        | 交易结果描述 |
| 业务流水号 | bizFlow      | String(32) | M        | 业务流水号   |



### 5.4.5 查询支持换汇币种对

**1 功能描述**

| 交易代码 | TP3002                                             |
| -------- | -------------------------------------------------- |
| 功能名称 | 查询换汇支持币种对                                 |
| 功能描述 | 查询换汇支持币种对，可在当前支持的币种内进行FX交易 |
| 调用方式 | 实时接口                                           |
| 调用流程 | --                                                 |
| 应用场景 | 需要查询目前已支持的FX币种                         |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3002`

**Method：** `POST`

**3 请求字段**


无
                                                                   

**4 响应字段**


 接口返回对象为: **`List<CurrencyPair>`**

**CurrencyPair字段：**

| 名称     | Json标签     | 类型      | 属性 | 取值说明 |
| -------- | ------------ | --------- | ---- | -------- |
| 卖出币种 | sellCurrency | String(3) | M    | 卖出币种 |
| 买入币种 | buyCurrency  | String(3) | M    | 买入币种 |



## 5.5 人民币付款

### 5.5.1 人民币付款

**1 功能描述**

|          |                                                              |
| -------- | ------------------------------------------------------------ |
| 交易代码 | TP1001                                                       |
| 功能名称 | 人民币付款                                                   |
| 功能描述 | 发起人民币付款请求，将收款人信息发送至Ottpayhk               |
| 调用方式 | 实时接口                                                     |
| 调用流程 | 先通过sftp将还原材料提交至Ottpayhk，再调用此接口发送付款信息 |
| 应用场景 | 需要将人民币付给国内持卡人                                   |

 **2 请求地址**

 **Url：** `https://{baseUrl}/api/tp1001`
  
 **Method：** `POST`

> 请求示例:

```json
{
    "merOrderNo":"KL123124124124124124124124",
    "fileUrlPath":"ftp://shahdsjgd.shaddja/jjafs?",
    "paymentType":"00",
    "callbackUr":"https://exmepdsa.com/sdgsge",
    "payOrderList":[
        {
            "merSingleNo":"SDF2551535",
            "payeeAccountNo":"EE2563461613461 ",
            "identity":"321461466413461436",
            "amount":1000000,
            "cNAPSCode":"dserqt",
            "tradeCodeType":"qe",
            "payMethod":"qerq",
            "declarationCurrency":"wtwerywyw",
            "advanceProportion":"ojfosjgjaoa",
            "settlementDate":"kadagodgj",
            "senderName":"Eege Esgg",
            "senderIncorporationNo":"wqthdfqr",
            "registrationRegion":"rywrsdgah sgsrg",
            "senderBankName":"ghtwjsht",
            "sourceFounds":"ergwr",
            "senderBankAccountNo":"fdrehwhwg",  
        }
    ],
}
```
**3 请求字段**  

| 名称         | Json标签     | 类型                    | 属性 | 取值说明                                                                                      |
| ------------ | ------------ | ----------------------- | ---- | --------------------------------------------------------------------------------------------- |
| 订单号       | merOrderNo   | String(32)              | M    | 本次交易唯一订单号                                                                            |
| 还原材料路径 | fileUrlPath  | String(128)             | O    | 上传至sftp文件服务器的还原材料路径                                                            |
| 交易类型     | paymentType  | String                  | M    | [参数详见字段说明](#6-1-1-paymenttype)                                              |
| 回调地址     | callbackUrl  | String                  | M    | 用于结果通知的地址                                                                            |
| 收款人列表   | payOrderList | `List<PayOrderRequest>` | M    | 收款信息                                                                                      |
| 手续费标识   | feeFlag      | String(1)               | O    | 当手续费为实时收取时，用户可自行选择内扣还是外扣。<br/>1：外扣，0：内扣                       |
| 还原材料列表 | payReduceList| `List<payReduceList>`   | O    | 当收款信息交易编码为游戏、电商、一般贸易填写[参数详见字段说明](#6-1-2-tradecodetype)|
**PayOrderRequest信息**

| 名称                      | Json标签              | 类型    | 属性 | 取值说明                                                                                                                          |
| ------------------------- | --------------------- | ------- | ---- | --------------------------------------------------------------------------------------------------------------------------------- |
| 单笔订单号                | merSingleNo           | String  | O    | 单个付款记录对应的订单号                                                                                                          |
| 收款方账号                | payeeAccountNo        | String  | M    | 收款方银行账号                                                                                                                    |
| 收款方姓名                | payeeName             | String  | M    | 收款方银行账户名                                                                                                                  |
| 身份证号/统一社会信用代码 | identity              | String  | M    | 若收款方账户类型为0，则填写身份证号，为1则填写统一社会信用代码                                                                    |
| 金额                      | amount                | Decimal | M    | 付款金额，单位为分，例：若付款200.00元，应填写20000最小为1                                                                        |
| 联行号                    | cNAPSCode             | String  | M    | 收款方银行联行号                                                                                                                  |
| 手机号                    | mobile                | String  | M    | 手机号                                                                        |
| 交易编码                  | tradeCodeType         | String  | M    | [参数详见字段说明](#6-1-2-tradecodetype)                                                                                |
| 付款方式                  | payMethod             | String  | O    | [参数详见字段说明](#6-1-3-paymethod),<br>tradeCodeType为TRADE并且paymentType为B2B时不能为空, <br>默认：cash_on_delivery |
| 报关币种                  | declarationCurrency   | String  | O    | payMethod值为cash_on_delivery不能为空，默认CNY                                                                                    |
| 预付比例                  | advanceProportion     | Float   | O    | payMethod值为advance ,0 < advanceProportion < 1 ,小数点后最多两位                                                                 |
| 结算账期                  | settlementDate        | String  | O    | payMethod值为advance结算账期不能为空单位天                                                                                        |
| 付款方名称                | senderName            | String  | M    | 真实付款方名称                                                                                                                    |
| 付款方公司注册号          | senderIncorporationNo | String  | M    | 付款方公司注册号                                                                                                                  |
| 付款方注册地              | registrationRegion    | String  | M    | 付款人住的区域swift国家地区                                                                                                       |
| 付款方银行名称            | senderBankName        | String  | M    | 付款方银行名称                                                                                                                    |
| 资金源                    | sourceFounds          | String  | O    | 选填                                                                                                                              |
| 付款方银行账户            | senderBankAccountNo   | String  | O    | 付款方银行账户选填                                                                                                                |
**payReduceList信息**

| 名称      | Json标签        | 类型    | 属性  | 取值说明                                                     |
|---------|---------------| ------- |-----|----------------------------------------------------------|
| 订单号     | orderNo       | String  | M   | 单个付款记录对应的订单号(不超过32位)                                     |
| 订单币种    | orderCurrency | String  | M   | 收款币种                                                     |
| 订单金额    | orderAmount   | Decimal | M   | 收款金额，单位为分，例：若付款200.00元，应填写20000最小为1                      |
| 订单日期    | orderDate     | String  | M   | 收款日期，格式为"yyyy-MM-dd"                                     |
| 收款人姓名   | sellerName    | String  | C   | 收款人姓名 (交易编码为游戏时必填)                                       |
| 收款人证件号  | sellerId      | String  | C   | 收款方证件号(长度不超过18位)(交易编码为游戏时必填)                             |
| 商品名     | goodsName     | String  | M   | 商品名                                                     |
| 商品种类    | goodsCategory | String  | C   | 商品种类 (交易编码为游戏时必填)                                                    |
| 商品数量    | goodNumber    | String  | M   | 商品数量                                                     |
| 物流公司    | wlName        | String  | C   | 物流公司名 (交易编码为一般贸易或者电商时必填)                                 |
| 物流单号    | wlSeqno       | String  | C   | 物流单号 (交易编码为一般贸易或者电商时必填)                                  |
| 店铺链接    | storeLink     | String  | C   | 店铺链接地址  (交易编码为一般贸易或者电商时必填)                               |
| 平台名称    | platformName  | String  | C   | 平台名称   (交易编码为一般贸易或者电商时必填)                                |
| 汇款用途    | purpose       | String  | C   | [汇款用途代码参数](#6-1-7-tradepurpose) (交易编码为一般贸易或者电商时必填) |
| 买家银行名   | buyerBankName | String  | O   | 买家银行名                                                    |
| 买家银行卡号  | buyerBankCard | String  | O   | 买家银行卡号                                                   |
| 交易方式    | sendType      | String  | O   | 发货方式                                                     |
| 快递金额    | sendAmount    | Decimal | O   | 快递金额，单位为分，例：若付款200.00元，应填写20000最小为1                      |
| 税费金额    | taxAmount     | Decimal | O   | 税费金额，单位为分，例：若付款200.00元，应填写20000最小为1                      |
| 其他金额    | otherAmount   | Decimal | O   | 其他金额，单位为分，例：若付款200.00元，应填写20000最小为1                      |
| 申报人类型   | applyType     | String  | O   | 申报人类型                                                    |


**4 响应字段**

若响应报文头内respCode为S00000，则为受理成功，请等待异步通知（见[5.5.3 系统通知商户付款结果](#5-5-3)）付款结果。报文体：当
respCode为S00000时：

| 名称         | Json标签        | 类型       | 属性 | 取值说明                                          |
| ------------ | --------------- | ---------- | ---- | ------------------------------------------------- |
| 订单号       | merOrderNo      | String(32) | M    | 原样返回                                          |
| 业务流水号   | bizFlowNo       | String(32) | M    | Ottpayhk生成的唯一业务流水号，与订单号一一对应    |
| 状态         | status          | String(1)  | M    | "0":"接受", "1":"成功", "2":"失败",  "3":"处理中" |
| 手续费币种   | feeCurrency     | String(3)  | O    | 所收取的手续费币种                                |
| 手续费币种   | feeAmount       | Decimal    | O    | 所收取的手续费金额                                |
| 实际付款金额 | actualPayAmount | Decimal    | O    | 实际付款金额    



### 5.5.2 人民币付款业务查询

**1 功能描述**

| 交易代码 | TP3001                                     |
| -------- | ------------------------------------------ |
| 功能名称 | 人民币付款业务查询                         |
| 功能描述 | 商户自行查询人民币付款最终结果             |
| 调用方式 | 实时接口                                   |
| 调用流程 | 商户发送人民币付款请求后，查询对应订单结果 |
| 应用场景 | 商户需要知晓人民币付款最终结果             |

**2 请求地址**

**Url：** `https://{baseUrl}/api/tp3001`

**Method：** `POST`

**3 请求字段**


| 名称       | Json标签   | 类型       | 属性 | 取值说明                                                                                                             |
| ---------- | ---------- | ---------- | ---- | -------------------------------------------------------------------------------------------------------------------- |
| 订单号     | merOrderNo | String(32) | O    | 付款发起时的订单号                                                                                                   |
| 业务流水号 | bizFlowNo  | String(32) | O    | Ottpayhk 生成的唯一业务流水号， 与订单号一一对应<br>注：订单号与业务流水号仅需填写一个，若同时填写，以业务流水号为准 |
                                                                   

**4 响应字段**



| 名称         | Json标签        | 类型          | 属性 | 取值说明                 |
| ------------ | --------------- | ------------- | ---- | ------------------------ |
| 订单号       | merOrderNo      | String(32)    | M    | 付款请求发起时的订单号   |
| 业务流水号   | bizFlowNo       | String(32)    | M    | 付款请求返回的业务流水号 |
| 结果代码     | respCode        | String(6)     | M    | 付款交易结果代码         |
| 结果描述     | respDesc        | String(50)    | M    | 付款交易结果详情描述     |
| 收款人列表   | payeeList       | `List<payee>` | M    | 收款人列表               |
| 手续费币种   | feeCurrency     | String(3)     | O    | 所收取的手续费币种       |
| 手续费币种   | feeAmount       | Decimal       | O    | 所收取的手续费金额       |
| 实际付款金额 | actualPayAmount | Decimal       | O    | 实际付款金额             |

**payee 的字段**

| 名称                           | Json标签              | 类型       | 属性 | 取值说明                                                                                                                |
| ------------------------------ | --------------------- | ---------- | ---- | ----------------------------------------------------------------------------------------------------------------------- |
| 单笔订单号                     | merSingleNo           | String(32) | M    | 单个付款记录对应的订单号                                                                                                |
| 收款方户名                     | payeeName             | String(64) | M    | 收款方银行账户户名                                                                                                      |
| 收款方账号                     | payeeAccountNo        | String(32) | M    | 收款方银行账号                                                                                                          |
| 收款方账户类型                 | acctType              | String(1)  | M    | 0 : 对私账户 1：对公账户                                                                                                |
| 身份证号/<br>统一 社会信用代码 | identity              | String(32) | M    | 若收款方账户类型为 **0**，则填写**身份证号**，<br>为 **1** 则填写**统一社会信用代码**                                   |
| 金额                           | amount                | String(18) | M    | 付款金额，单位为分，例：若付款 **200.00** 元，应填写 **20000**                                                          |
| 联行号                         | cNAPSCode             | String(64) | M    | 联行号                                                                                                                  |
| 手机号                     | mobile              | String(13) | M    | 手机号                                                                                                          |
| 开户行名称                     | bankName              | String(32) | M    | 收款方银行名称                                                                                                          |
| 开户行省份                     | bankProvince          | String(32) | M    | 收款方银行所在省份                                                                                                      |
| 开户行市名                     | bankCity              | String(32) | M    | 收款方银行所在市名                                                                                                      |
| 支行名称                       | bankBranchName        | String(32) | M    | 收款方银行支行名称                                                                                                      |
| 交易编码                       | tradeCodeType         | String(6)  | M    | 对应交易属性类型，参见[参数详见字段说明](#6-1-2-tradecodetype)                                                |
| 单笔结果代码                   | respCode              | String(6)  | M    | 单笔交易对应的结果代码                                                                                                  |
| 单笔结果描述                   | respDesc              | String(50) | M    | 单笔交易对应的结果描述                                                                                                  |
| 付款方式                       | payMethod             | String     | F    | **tradeCodeType**为 *TRADE*，并且 **paymentType** 为 *B2B* 时不能为空<br>[参数详见字段说明](#6-1-3-paymethod) |
| 报关币种                       | declarationCurrency   | String     | F    | **payMethod** 值为 *cash_on_delivery* 不能为空                                                                          |
| 预付比例                       | advanceProportion     | Float      | F    | **payMethod** 值为 advanc<br> 0 < advanceProportion < 1  小数点后最多两位                                               |
| 结算账期                       | settlementDate        | String     | F    | **payMethod** 值为 advance <br>结算账期不能为空   单位天                                                                |
| 付款方名称                     | senderName            | String     | M    | 真实付款方名称                                                                                                          |
| 付款方公司注册号               | senderIncorporationNo | String     | M    | 付款方公司注册号                                                                                                        |
| 付款方注册地                   | registrationRegion    | String     | M    | 付款人住的区域 swift 国家地区                                                                                           |
| 付款方银行名称                 | senderBankName        | String     | M    | 付款方银行名称                                                                                                          |
| 资金源                         | sourceFounds          | String     | F    | 选填                                                                                                                    |
| 付款方银行账户                 | senderBankAccountNo   | String     | F    | 付款方银行账户 选填                                                                                       


### 5.5.3 系统通知商户付款结果

**1 功能描述**

| 交易代码 | TP2001                                                                                                                                                                           |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 功能名称 | 付款回调                                                                                                                                                                         |
| 功能描述 | Ottpayhk 通知商户付款结果                                                                                                                                                        |
| 调用方式 | 实时接口                                                                                                                                                                         |
| 调用流程 | 商户先调用 [5.5.1 人民币付款](#5-5-1)向 Ottpayhk 发起人民币付款请求，Ottpayhk 将交易。<br>处理完毕后，通知商户。若规定时间内未及时回调通知商户，商户应该发起主动查询 |
| 应用场景 | 商户需要知晓人民币付款最终结果                                                                                                                                                   |

<aside class="success">
 本通知将按照间隔时间渐长的方式持续通知24小时.<br>商户应当以http 200返回，若通知持续时间结束仍未正常返回，则不再通知。<br>商户应当自行通过 [5.5.2 人民币付款业务查询](#5-5-2) 查询接口查询交易结果。
</aside>

**2 请求地址**

 **Url：** [5.1.1 人民币付款](#5-5-1) 中的 **callbackUrl** 
  
 **Method：** `POST`

**3 请求字段**

| 名称       | Json标签     | 类型          | 属性 | 取值说明                                        |
| ---------- | ------------ | ------------- | ---- | ----------------------------------------------- |
| 订单号     | merOrderNo   | String(32)    | M    | 原样返回                                        |
| 业务流水号 | bizFlowNo    | String(32)    | M    | Ottpayhk 生成的唯一业务流水号，与订单号一一对应 |
| 成功笔数   | successCount | Int           | M    | 返回成功笔数                                    |
| 失败笔数   | faultCount   | Int           | M    | 返回失败笔数                                    |
| 付款详情   | payeeList    | `List<payee>` | M    | 付款详情列表不分页                              |

**payee 字段:**

| 名称               | Json标签    | 类型         | 属性 | 取值说明                                       |
| ------------------ | ----------- | ------------ | ---- | ---------------------------------------------- |
| 单笔详情外部商户号 | merSingleNo | String       | M    | 商户传入的 管理商户系统的凭证号                |
| 系统订单号         | applyNo     | String       |      | M	Ottpayhk 生成的订单号                        |
| 金额               | Amount      | Number(18,2) | M    | 付款金额                                       |
| 状态               | Status      | Int          | M    | "0":"接受","1", "成功","2","失败","3","处理中" |
| 说明               | respDesc    | String       | M    | 交易具体说明                                   |
| 状态码             | respCode    | String       | M    | 交易具体的状态码                               |



### 5.5.4 查询总行

**1 功能描述**

| 交易代码 | TP6001               |
| -------- | -------------------- |
| 功能名称 | 总行查询             |
| 功能描述 | 分页查询总行信息接口 |
| 调用方式 | 实时接口             |
| 调用流程 | --                   |
| 应用场景 | 当前账户余额查询     |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp6001`

**Method：** `POST`

**3 请求字段**


| 名称     | Json标签 | 类型 | 属性 | 取值说明         |
| -------- | -------- | ---- | ---- | ---------------- |
| 页数     | pageNo   | Int  | O    | 分页页数，默认1  |
| 页显示数 | pageSize | Int  | O    | 页显示数，默认10 |


> 返回示例:

```json
{
    "pageNo": 1,
    "pageSize": 5,
    "totalRecord": 1,
    "results": [
        {
            "bankName": "国家开发银行",
            "bankId": 1,
            "bankNameEn": "xxx bank"
        }
    ]
}

```                                                                   

**4 响应字段**


| 名称         | Json标签    | 类型                  | 属性 | 取值说明 |
| ------------ | ----------- | --------------------- | ---- | -------- |
| 当前页数     | pageNo      | Int                   | M    | --       |
| 当前页显示数 | pageSize    | Int                   | M    | --       |
| 总记录数     | totalRecord | Int                   | M    | --       |
| 总行信息集合 | results     | `List<QueryBankResp>` | M    | --       |

**QueryBankResp 字段：**

| 名称         | Json标签   | 类型       | 属性 | 取值说明 |
| ------------ | ---------- | ---------- | ---- | -------- |
| 银行名称     | bankName   | String(64) | M    | --       |
| 银行Id       | bankId     | int        | M    | --       |
| 银行名称英文 | bankNameEn | String(64) | M    | --       |



### 5.5.5 查询总行下分行支持省份

**1 功能描述**

| 交易代码 | TP6002                     |
| -------- | -------------------------- |
| 功能名称 | 查询省份信息               |
| 功能描述 | 查询总行下支持分行所在省份 |
| 调用方式 | 实时接口                   |
| 调用流程 | --                         |
| 应用场景 | --                         |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp6002`

**Method：** `POST`

**3 请求字段**


| 名称   | Json标签 | 类型 | 属性 | 取值说明            |
| ------ | -------- | ---- | ---- | ------------------- |
| 总行Id | bankId   | Int  | M    | 必填 总行的银行编码 |

                                                                   
> 返回示例:

```json
{
    "bankCode": "101",
    "provinceList": [
        {
            "provinceCode": "513",
            "provinceName": "四川省",
            "provinceNameEn": "si chuan province"
        }
    ]
}

```
**4 响应字段**


| 名称         | Json标签     | 类型                 | 属性 | 取值说明       |
| ------------ | ------------ | -------------------- | ---- | -------------- |
| 总行Id       | bankId       | Int                  | M    | 总行的银行编码 |
| 省份信息集合 | provinceList | `List<ProvinceResp>` | M    | --             |

**ProvinceResp 字段：**

| 名称         | Json标签       | 类型       | 属性 | 取值说明 |
| ------------ | -------------- | ---------- | ---- | -------- |
| 省份编码     | provinceCode   | String(64) | M    | --       |
| 省份名称     | provinceName   | String(32) | M    | --       |
| 省份名称英文 | provinceNameEn | String(64) | M    | --       |



### 5.5.6 查询总行下分行支持城市

**1 功能描述**

| 交易代码 | TP6003                     |
| -------- | -------------------------- |
| 功能名称 | 查询城市信息               |
| 功能描述 | 查询总行下支持分行所在城市 |
| 调用方式 | 实时接口                   |
| 调用流程 | --                         |
| 应用场景 | --                         |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp6003`

**Method：** `POST`

**3 请求字段**


| 名称     | Json标签     | 类型       | 属性 | 取值说明            |
| -------- | ------------ | ---------- | ---- | ------------------- |
| 总行Id   | bankId       | Int        | M    | 必填 总行的银行编码 |
| 省份编码 | provinceCode | String(64) | M    | 必填 省份编码       |
                                                                   
> 返回示例:

```json
{
    "bankCode": "101",
    "provinceCode": "513",
    "cityList": [
        {
            "cityName": "阿坝藏族羌族自治州",
            "cityCode": "513225000000",
            "cityNameEn": "xxxx "
        }
    ]
}

```

**4 响应字段**


| 名称         | Json标签     | 类型             | 属性 | 取值说明 |
| ------------ | ------------ | ---------------- | ---- | -------- |
| 总行Id       | bankId       | Int              | M    | --       |
| 省份编码     | provinceCode | String(64)       | M    | --       |
| 城市信息集合 | cityList     | `List<CityResp>` | M    | --       |

**CityResp 字段：**

| 名称         | Json标签   | 类型       | 属性 | 取值说明 |
| ------------ | ---------- | ---------- | ---- | -------- |
| 城市编码     | cityCode   | String(64) | M    | --       |
| 城市名称     | cityName   | String(32) | M    | --       |
| 城市名称英文 | cityNameEn | String(32) | M    | --       |




### 5.5.7 查询总行下某城市所有分行

**1 功能描述**

| 交易代码 | TP6004                   |
| -------- | ------------------------ |
| 功能名称 | 查询分行信息             |
| 功能描述 | 查询总行下某城市所有分行 |
| 调用方式 | 实时接口                 |
| 调用流程 | --                       |
| 应用场景 | --                       |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp6004`

**Method：** `POST`

> 请求示例:

```json
{
    "pageNo": 1,
    "pageSize": 15,
    "query": {
            "bankId": 12,
            "cityCode": "513225000000",
        }
    
}

```

**3 请求字段**


| 名称         | Json标签 | 类型                     | 属性 | 取值说明 |
| ------------ | -------- | ------------------------ | ---- | -------- |
| 页数         | pageNo   | int                      | O    | 默认1    |
| 页显示数     | pageSize | int                      | O    | 默认 10  |
| 分行查询请求 | query    | `QueryBranchBankRequest` | M    | 不能为空 |

**QueryBranchBankRequest 的字段** 

| 名称     | Json标签 | 类型       | 属性 | 取值说明 |
| -------- | -------- | ---------- | ---- | -------- |
| 总行Id   | bankId   | Int        | M    | 不能为空 |
| 城市编码 | cityCode | String(64) | M    | 不能为空 |


                                                                   
> 返回示例:

```json
{
    "pageNo": 1,
    "pageSize": 5,
    "totalRecord": 1,
    "results": [
        {
            "bankLinkNo": "102100099996",
            "bankName": "中国工商银行股份有限公司九寨沟支行",
            "bankNameEn": "china gongshang bank",
            "bankProvinceCode": "513",
            "bankProvinceName": "四川省",
            "bankProvinceNameEn": "si chuan province",
            "bankCityCode": "513225000000",
            "bankCityName": "阿坝藏族羌族自治州",
            "bankCityNameEn": "a ba "
        }
    ]
}
```
**4 响应字段**


| 名称           | Json标签    | 类型                        | 属性 | 取值说明 |
| -------------- | ----------- | --------------------------- | ---- | -------- |
| 当前页码       | pageNo      | Int                         | M    | --       |
| 页显示数       | pageSize    | Int                         | M    | --       |
| 总数           | totalRecord | In                          | M    | --       |
| 分支行信息集合 | results     | `List<QueryBranchBankResp>` | M    | --       |


**QueryBranchBankResp 字段：**

| 名称         | Json标签           | 类型       | 属性 | 取值说明 |
| ------------ | ------------------ | ---------- | ---- | -------- |
| 联行号       | bankLinkNo         | String(64) | M    | --       |
| 银行名称     | bankName           | String(32) | M    | --       |
| 银行名称英文 | bankNameEn         | String(32) | M    | --       |
| 省份编码     | bankProvinceCode   | String(32) | M    | --       |
| 省份名称     | bankProvinceName   | String(32) | M    | --       |
| 省份名称英文 | bankProvinceNameEn | String(32) | M    | --       |
| 城市编码     | bankCityCode       | String(32) | M    | --       |
| 城市名称     | bankCityName       | String(32) | M    | --       |
| 城市名称英文 | bankCityNameEn     | String(32) | M    | --       |



## 5.6 国际汇款


### 5.6.1 查询国际付款字段

**1 功能描述**

| 交易代码 | TP3005                                 |
| -------- | -------------------------------------- |
| 功能名称 | 查询国际付款字段                       |
| 功能描述 | 查询向不同国家付款所需的字段           |
| 调用方式 | 实时接口                               |
| 调用流程 | --                                     |
| 应用场景 | 国际付款前查询向不同国家付款所需的字段 |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3005`

**Method：** `POST`

**3 请求字段**


| 名称         | Json标签       | 类型   | 属性 | 取值说明                    |
| ------------ | -------------- | ------ | ---- | --------------------------- |
| 收款国家     | countryCode    | string | M    | iso 3166-1标准2字代码       |
| 收款币种     | arriveCurrency | string | M    | 收款方币种，3位标准货币代码 |
| 扣款币种     | debitCurrency  | string | M    | 扣款币种，3位标准货币代码   |
| 付款方式     | payType        | string | M    | 可选值：local 或者 swift    |
| 收款账户类型 | accountType    | string | M    | 暂只支持输入 1（银行账户）  |

                                                                   
> 返回示例:

```json
{
	"payee": {
		"required": [
			"fullName",
			"payeeResidentAddress",
			"payeeResidentCountry",
			"payeeBankName",
			"payeeBankSwiftCode"
		],
		"optional": [
			
		]
	},
	"payer": {
		"required": [
			"payerName",
			"payerType"
		],
		"optional": [
			"payerCompanyName",
			"payerPersonName"
		]
	},
	"condition": {
		"payerType": {
			"01": [
				//当payerType==01时，payerPersonName为必填"payerPersonName"
			],
			"00": [
				//当payerType==00时，payerCompanyName为必填"payerCompanyName"
			]
		}
	},
    "selectOption": {
        "payerType": [
            {
                "code": "01",
                "value": "B"
            },
            {
                "code": "00",
                "value": "C"
            }
        ],
        "bankAcctType": [
            {
                "code": "01",
                "value": "company"
            },
            {
                "code": "00",
                "value": "customer"
            }
        ],
        "payeeIdType": [
            {
                "code": "1",
                "value": "工作证"
            },
            {
                "code": "2",
                "value": "国际护照"
            },
            {
                "code": "3",
                "value": "身份证"
            },
            {
                "code": "4",
                "value": "社会保障"
            },
            {
                "code": "5",
                "value": "居留许可证"
            },
            {
                "code": "6",
                "value": "公司注册号"
            }
        ]
    },
	"bankList": [
		"bank name 1",
		"bank name 2",
		"bank name 3"
	]
}
```

**4 响应字段**


| 名称         | Json标签  | 类型             | 属性 | 取值说明               |
| ------------ | --------- | ---------------- | ---- | ---------------------- |
| 付款方       | payer     | ParamField       | M    | 付款方所需字段要求     |
| 收款方       | payee     | ParamField       | M    | 收款方所需字段要求     |
| 枚举值字段     | selectOption | Object           | O    | 收付款方某些字段的枚举值，code为应传的值，value为对应的描述           |
| 选填条件     | condition | Object           | O    | 前置选填条件           |
| 支持银行列表 | bankList  | ` List<String> ` | O    | 支持的收款银行名称列表 |

**ParamField 的字段**

| 名称     | Json标签 | 类型           | 属性 | 取值说明 |
| -------- | -------- | -------------- | ---- | -------- |
| 必填字段 | required | `List<String>` | M    | 必填字段 |
| 选填字段 | optional | `List<String>` | M    | 选填字段 |



### 5.6.2 国际汇款接口

**1 功能描述**

|          |                                                                                                              |
| -------- | ------------------------------------------------------------------------------------------------------------ |
| 交易代码 | TP1004                                                                                                       |
| 功能名称 | 国际汇款接口                                                                                                 |
| 功能描述 | 发起国际汇款，向境外收款人发起汇款。                                                                         |
| 调用方式 | 实时接口                                                                                                     |
| 调用流程 | 调用[5.6.1 查询国际付款字段](#5-6-1)获取收款方所需字段后，依据相应字段，向收款人发起汇款。 |
| 应用场景 | 发起国际汇款，向境外收款人发起汇款                                                                           |

**2 请求地址**

**Url：** `https://{baseUrl}/api/tp1004`

**Method：** `POST`

> 请求示例:

```json
{
    "merOrderNo":"1245",
    "countryCode":"gb",
    "arriveCurrency": "gbp",
    "debitCurrency": "gbp",
    "payType": "local",
    "accountType": "1",
    "arriveAmount":"100",
    "purpose":"1",
    "payer": {
        "payerCompanyName":"demo company",
        "payerAddress":"No.2 Street",
        "payerCountry":"hk",
        "endSenderName":"fwefwe",
        "payerCompanyRegisterNo":"wegwefwef",
        "payerBankName":"fwef"
    },
    "payee": {
        "bankAcctType":"01",
        "payeeCompanyName":"payee company",
        "payeeAddress":"No.payee street",
        "payeeZipCode":"132423",
        "payeeCity":"London",
        "payeeBankName":"Center bank",
        "payeeBankAccountName":"payee company",
        "payeeBankAccountNo":"2323r23fwef",
        "payeeBankBranchCode":"sdfwe2d"
    },
    "fxBizFlow": "23434578432",
    "tradeComments":"trade remark"
}
```
**3 请求字段**

| 名称         | Json标签       | 类型   | 属性 | 取值说明                                                                               |
| ------------ | -------------- | ------ | ---- | -------------------------------------------------------------------------------------- |
| 商户订单号   | merOrderNo     | string | M    | 商户自定义订单号，需唯一                                                               |
| 收款国家     | countryCode    | string | M    | iso 3166-1标准2字代码                                                                  |
| 收款币种     | arriveCurrency | string | M    | 收款方币种，3位标准货币代码                                                            |
| 扣款币种     | debitCurrency  | string | M    | 扣款币种，3位标准货币代码                                                              |
| 付款方式     | payType        | string | M    | 可选值：local 或者 swift                                                               |
| 收款账户类型 | accountType    | string | M    | 暂只支持输入 1（银行账户）                                                             |
| 扣款金额     | debitAmount   | string | C    | 扣款金额，即扣款币种对应金额                                             |
| 收款金额     | arriveAmount   | string | C    | 收款金额（扣款金额和收款金额2选1填写，若同时填写，以收款金额为准）                     |
| 汇款目的     | purpose        | string | M    | 详见[6.1.4汇款目的列表](#6-1-4-purpose)                                      |
| 付款方字段   | payer          | object | M    | 按照相应国家tp3005返回的数据进行填写                                                   |
| 收款方字段   | payee          | Object | M    | 按照相应国家tp3005返回的数据进行填写                                                   |
| 关联fx流水号 | fxBizFlow      | String | O    | 关联fx流水号，若填写此字段，则本接口不校验余额，<br>但扣款金额不能大于对应fx订单的金额 |
| 汇款附言     | tradeComments  | String | O    | 汇款附言                                                                               |
| 汇款目的备注 | purposeRemark  | String | O    | 当purpose为99时，汇款目的以此为准                                                      |

                                                                
**4 响应字段**


| 名称         | Json标签       | 类型   | 属性 | 取值说明                         |
| ------------ | -------------- | ------ | ---- | -------------------------------- |
| 扣款币种     | debitCurrency  | String | M    | 扣款币种                         |
| 收款币种     | arriveCurrency | String | M    | 收款币种                         |
| 汇率         | rate           | String | M    | 汇率                             |
| 扣款金额     | debitAmount    | String | M    | 扣款金额                         |
| 收款金额     | arriveAmount   | String | M    | 收款金额                         |
| 报价ID       | quoteId        | long   | M    | 报价ID                           |
| 报价有效期   | expireTime     | long   | M    | unix时间戳，此次询价的有效时间。 |
| 商户订单号   | merOrderNo     | String | M    | 商户传入的订单号                 |
| 关联fx流水号 | fxBizFlow      | String | O    | 关联fx流水号  

                   |

### 5.6.3 国际汇款交易确认

**1 功能描述**

|          |                                                                                |
| -------- | ------------------------------------------------------------------------------ |
| 交易代码 | TP1005                                                                         |
| 功能名称 | 国际汇款交易确认                                                               |
| 功能描述 | 确认国际汇款交易，正式提交。                                                   |
| 调用方式 | 实时接口                                                                       |
| 调用流程 | 调用[5.6.2 国际汇款接口](#5-6-2)提交交易后，调用此接口确认交易。 |
| 应用场景 | 发起国际汇款，向境外收款人发起汇款后，确认国际汇款交易，正式提交。             |

**2 请求地址**

**Url：** `https://{baseUrl}/api/tp1005`

**Method：** `POST`

**3 请求字段**

| 名称    | Json标签    | 类型   | 属性 | 取值说明    |
| ------- | ----------- | ------ | ---- | ----------- |
| 报价ID  | quoteId     | Long   | M    | 报价ID      |
| 回调url | callbackUrl | String | M    | 回调通知Url |
                                                                   

**4 响应字段**


| 名称         | Json标签       | 类型   | 属性 | 取值说明                     |
| ------------ | -------------- | ------ | ---- | ---------------------------- |
| 报价ID       | quoteId        | long   | M    | 报价ID                       |
| 收款国家     | countryCode    | string | M    | iso 3166-1标准2字代码        |
| 收款币种     | arriveCurrency | string | M    | 收款方币种，3位标准货币代码  |
| 扣款币种     | debitCurrency  | string | M    | 扣款币种，3位标准货币代码    |
| 付款方式     | payType        | string | M    | 可选值：local 或者 swift     |
| 收款账户类型 | accountType    | string | M    | 暂只支持输入 1（银行账户）   |
| 付款金额     | arriveAmount   | string | M    | 收款金额                     |
| 扣款金额     | debitAmount    | String | M    | 扣款金额                     |
| 汇率         | rate           | String | M    | 汇率                         |
| 状态         | status         | String | M    | 订单状态                     |
| 结果码       | code           | String | M    | 交易结果码                   |
| 结果描述     | message        | String | M    | 交易结果描述                 |
| 交易流水号   | bizFlow        | String | M    | 对应国际汇款交易的唯一流水号 |
| 商户订单号   | merOrderNo     | String | M    | 商户订单号                   |
| 关联fx流水号 | fxBizFlow      | String | O    | 关联fx流水号     




###  5.6.4 国际汇款历史交易查询

**1 功能描述**

| 交易代码 | TP3006                     |
| -------- | -------------------------- |
| 功能名称 | 国际汇款历史交易查询       |
| 功能描述 | 国际汇款历史交易查询       |
| 调用方式 | 实时接口                   |
| 调用流程 | --                         |
| 应用场景 | 查询以往的国际汇款历史交易 |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3006`

**Method：** `POST`

**3 请求字段**


| 名称         | Json标签   | 类型   | 属性 | 取值说明                             |
| ------------ | ---------- | ------ | ---- | ------------------------------------ |
| 查询起始时间 | startTime  | Long   | O    | Unix13位时间戳，查询开始时间，闭区间 |
| 查询结束时间 | endTime    | Long   | O    | Unxi13位时间戳，查询结束时间，闭区间 |
| 报价ID       | quoteId    | Long   | O    | 报价ID                               |
| 商户订单号   | merOrderNo | String | O    | 商户订单号                           |

<aside class="success">
若startTime与endTime没填，则quoteId和merOrderNo中必填其一。若quoteId和merOrderNo都没填，则startTime与endTime为必填，且间隔不能超过24小时   
</aside>                                                              

**4 响应字段**


**返回对象是`List<RemittanceHistory>`**

**RemittanceHistory 的字段**

| 名称           | Json标签       | 类型   | 属性 | 取值说明                               |
| -------------- | -------------- | ------ | ---- | -------------------------------------- |
| 报价ID         | quoteId        | long   | M    | 报价ID                                 |
| 收款国家       | countryCode    | string | M    | iso 3166-1标准2字代码                  |
| 收款币种       | arriveCurrency | string | M    | 收款方币种，3位标准货币代码            |
| 扣款币种       | debitCurrency  | string | M    | 扣款币种，3位标准货币代码              |
| 付款方式       | payType        | string | M    | 可选值：local 或者 swift               |
| 收款账户类型   | accountType    | string | M    | 暂只支持输入 1（银行账户）             |
| 付款金额       | arriveAmount   | string | M    | 收款金额                               |
| 扣款金额       | debitAmount    | String | M    | 扣款金额                               |
| 汇率           | rate           | String | M    | 汇率                                   |
| 状态           | status         | string | M    | 状态码                                 |
| 结果码         | resCode           | String | M    | 交易结果码                             |
| 结果描述       | resMessage        | String | M    | 交易结果描述                           |
| 交易流水号     | bizFlow        | String | M    | 对应国际汇款交易的唯一流水号           |
| 商户订单号     | merOrderNo     | String | M    | 商户订单号                             |
| 付款和收款字段 | xxxxxx         | String | M    | 相应国家字段不同，根据tp3005返回的数据 |
| 关联fx流水号   | fxBizFlow      | String | O    | 关联fx流水号                           |


                                                        
### 5.6.5 国际汇款交易结果通知

**1 功能描述**

| 交易代码 | TP2003                                                                                                                                                            |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 功能名称 | 国际汇款交易结果通知                                                                                                                                              |
| 功能描述 | 国际汇款的交易结果异步通知                                                                                                                                        |
| 调用方式 | 通知接口                                                                                                                                                          |
| 调用流程 | --                                                                                                                                                                |
| 应用场景 | [5.6.3 国际汇款交易确认](#5-6-3)发起成功且交易处理完毕后，<br/>将根据[5.1.5 国际汇款交易确认](#5-6-3)参数内的回调Url进行回调通知最终结果。 |

<aside class="success">
 本通知将按照间隔时间渐长的方式持续通知24小时.<br>商户应当以http 200返回，若通知持续时间结束仍未正常返回，则不再通知。<br>商户应当自行通过 [5.4.3 换汇历史交易查询](#5-4-3)查询接口查询交易结果。
</aside>

**2 请求地址**

**Url：** [5.6.3 国际汇款交易确认](#5-6-3)中的 **callbackUrl**

**Method：** `POST`

**3 请求字段**

| 名称         | Json标签       | 类型   | 属性 | 取值说明                     |
| ------------ | -------------- | ------ | ---- | ---------------------------- |
| 报价ID       | quoteId        | long   | M    | 报价ID                       |
| 收款国家     | countryCode    | string | M    | iso 3166-1标准2字代码        |
| 收款币种     | arriveCurrency | string | M    | 收款方币种，3位标准货币代码  |
| 扣款币种     | debitCurrency  | string | M    | 扣款币种，3位标准货币代码    |
| 付款方式     | payType        | string | M    | 可选值：local 或者 swift     |
| 收款账户类型 | accountType    | string | M    | 暂只支持输入 1（银行账户）   |
| 付款金额     | arriveAmount   | string | M    | 收款金额                     |
| 扣款金额     | debitAmount    | String | M    | 扣款金额                     |
| 汇率         | rate           | String | M    | 汇率                         |
| 付款状态     | status         | string | M    | 订单状态                     |
| 结果码       | code           | String | M    | 交易结果码                   |
| 结果描述     | message        | String | M    | 交易结果描述                 |
| 交易流水号   | bizFlow        | String | M    | 对应国际汇款交易的唯一流水号 |
| 商户订单号   | merOrderNo     | String | M    | 商户订单号                   |
| 关联fx流水号 | fxBizFlow      | String | O    | 关联fx流水号                 |
      

## 5.7 内部转账

### 5.7.1 商户内部间转账

**1 功能描述**

|          |                                              |
| -------- | -------------------------------------------- |
| 交易代码 | TP1010                                       |
| 功能名称 | 商户内部间转账                             |
| 功能描述 | 同为在OTT注册的商户，向对方OTT账户进行转账                 |
| 调用方式 | 实时接口                                     |
| 调用流程 | --                                           |
| 应用场景 | 同为在OTT注册的商户，向对方OTT账户进行转账 |

**2 请求地址**

**Url：** `https://{baseUrl}/api/tp1010`

**Method：** `POST`

> 请求示例:

```json
{
        "merOrderNo":"150",
        "toAcctNo":"006804100255",
        "toAcctName":"TEST",
        "currency":"USD",
        "amount":"100",
        "purpose":"1",
        "remark":""
}
```                

**3 请求字段**

| 名称                     | Json标签              | 类型        | 属性 | 取值说明                                                                     |
| ------------------------ | --------------------- | ----------- | ---- | ---------------------------------------------------------------------------- |
| 商户订单号                   | merOrderNo               | string(32)  | M    | 商户自定义的唯一订单号                                                                       |
| 收款方账号             | toAcctNo   | string(32) | M    | 收款方账号                                                                 |
| 收款方账户名             | toAcctName        | string(255) | M    | 收款方账户名                                                                 |
| 转账币种               | currency         | string(3)   | M    | 转账币种 |
| 转账金额               | amount     | Decimal(18,2) | M    | 转账金额                                                                   |
| 汇款目的               | purpose | string(3) | M    | 汇款目的，参见附录6.1.4付款目的                                                             |
| 附言               | remark    | string(255) | O   | 附言                                                                   |

                                                 
> 返回示例:

```json
{
        "bizFlow": "70210415775519090003",
        "status": "SUCC",
        "feeCurrency": "USD",
        "feeAmount": "2.50"
}
```

**4 响应字段**


| 名称       | Json标签 | 类型        | 属性 | 取值说明                                                          |
| ---------- | -------- | ----------- | ---- | ----------------------------------------------------------------- |
| 业务流水号 | bizFlow  | string(32)  | M    | OTT侧唯一业务订单号                                                |
| 结果状态     | status     | string(6)   | M    | 结果状态 SUCC：成功 FAIL：失败 |
| 手续费币种   | feeCurrency  | string(3) | O    | 手续费币种，若手续费模式为实时收取时，则返回此字段                      |
| 手续费金额   | feeAmount  | string(22) | O    | 手续费金额，若手续费模式为实时收取时，则返回此字段                       |



## 5.8 充值

### 5.8.1 充值交易历史查询

**1 功能描述**

| 交易代码 | TP3008                 |
| -------- | ---------------------- |
| 功能名称 | 充值历史交易查询       |
| 功能描述 | 充值历史交易查询       |
| 调用方式 | 实时接口               |
| 调用流程 | --                     |
| 应用场景 | 查询以往的充值历史交易 |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3008`

**Method：** `POST`

**3 请求字段**


| 名称         | Json标签  | 类型          | 属性 | 取值说明                                               |
| ------------ | --------- | ------------- | ---- | ------------------------------------------------------ |
| 查询起始时间 | beginDate | Long          | O    | Unix13位时间戳，查询开始时间，闭区间                   |
| 查询结束时间 | endDate   | Long          | O    | Unix13位时间戳，查询开始时间，闭区间                   |
| 业务订单号   | batchNo   | String(32)    | O    | OTT生成的唯一流水号                                    |
| 充值银行     | bankCode  | String(8)     | O    | 充值银行代码                                           |
| 充值币种     | currency  | String(3)     | O    | 充值币种                                               |
| 查询最小金额 | minAmount | decimal(18,2) | O    | 查询最小金额                                           |
| 查询最大金额 | maxAmount | decimal(18,2) | O    | 查询最大金额                                           |
| 充值状态     | status    | String(3)     | O    | 充值状态 01: "待处理"; 02: "充值成功";  03: "充值拒绝" |
| 第几页       | pageNum   | Integer       | O    | 查询第几页                                             |
| 每页多少条   | pageSize  | Integer       | O    | 每页多少条，每页最多支持100条                          |

> 返回示例:

```json
{
	"pageNum": 1,
	"pageSize": 10,
	"total": 35,
	"list": [{
		"batchNo": "20180122SDC760719",
		"curType": "USD",
		"amount": "10000.00",
		"bank": "中国银行",
		"status": "02",
		"createTime": "2020-06-28 17:17:45",
		"updateTime": "2020-06-29 16:56:54",
		"account": "Company Name1"
	},{
		"batchNo": "11191226453692390002",
		"curType": "CNY",
		"amount": "240.06",
		"bank": "中国银行",
		"status": "02",
		"createTime": "2019-12-26 15:29:29",
		"updateTime": "2019-12-26 15:29:39",
		"account": null
	}]
}
```

**4 响应字段**


| 名称             | Json标签 | 类型                   | 属性 | 取值说明 |
| ---------------- | -------- | ---------------------- | ---- | -------- |
| 当前页码         | pageNum  | Int                    | M    | --       |
| 页显示数         | pageSize | Int                    | M    | --       |
| 总数             | total    | Int                    | M    | --       |
| 充值流水信息集合 | list     | `List<RechargeRecord>` | M    | --       |

**RechargeRecord 的字段**

| 名称         | Json标签   | 类型          | 属性 | 取值说明                                               |
| ------------ | ---------- | ------------- | ---- | ------------------------------------------------------ |
| 充值订单     | batchNo    | string(32)    | M    | 充值订单                                               |
| 币种         | curType    | string(3)     | M    | 充值币种，3位标准货币代码                              |
| 金额         | amount     | decimal(18,2) | M    | 充值金额                                               |
| 充值银行     | bank       | string(64)    | M    | 充值银行                                               |
| 充值账户     | account    | string(64)    | M    | 充值账户                                               |
| 充值状态     | status     | string(2)     | M    | 充值状态 01: "待处理"; 02: "充值成功";  03: "充值拒绝" |
| 充值发起时间 | createTime | Date          | M    | 充值发起时间                                           |
| 充值入账时间 | updateTime | Date          | M    | 充值入账时间                                           |


## 5.9 提现

### 5.9.1 提现接口

**1 功能描述**

|          |                                                  |
| -------- | ------------------------------------------------ |
| 交易代码 | TP1008                                           |
| 功能名称 | 提现交易申请                                     |
| 功能描述 | 用于发起境外提现，需提现账户名与商户注册名称相同 |
| 调用方式 | 实时接口                                         |
| 调用流程 | --                                               |
| 应用场景 | 用于发起境外提现，需提现账户名与商户注册名称相同 |

<aside class="success">
默认提现账户名称即为商户入网时提供的注册名称 
</aside>

**2 请求地址**

**Url：** `https://{baseUrl}/api/tp1008`

**Method：** `POST`

> 请求示例:

```json
{
    "merOrderNo":"8793478374",
    "currency":"USD",
    "amount": 10000.00,
    "bankAccountNo": "6248348342123342",
    "bankName": "Citibank",
    "bankAddress": "Queens Road, New York",
    "swiftCode":"7643843",
    "proxyBankName":"",
    "proxyBankAddress": "",
    "proxySwiftCode":"",
    "remark":"xxx公司贸易提现款项",
    "callbackUrl":"https://xxxx.xxxxxx.xx/xx"
}
```

**3 请求字段**

| 名称             | Json标签         | 类型          | 属性 | 取值说明                   |
| ---------------- | ---------------- | ------------- | ---- | -------------------------- |
| 商户订单号       | merOrderNo       | string(32)    | M    | 商户传入本次交易唯一订单号 |
| 币种             | currency         | string(3)     | M    | 提现币种，3位标准货币代码  |
| 金额             | amount           | decimal(18,2) | M    | 提现金额                   |
| 银行账号/IBAN    | bankAccountNo    | string(64)    | M    | 提现银行账号或IBAN         |
| 银行名称         | bankName         | string(64)    | M    | 提现银行名称               |
| 银行地址         | bankAddress      | string(256)   | M    | 提现银行的地址             |
| swift code       | swiftCode        | string(32)    | M    | 提现银行的swift code       |
| 代理行名称       | proxyBankName    | string(64)    | O    | 代理行名称                 |
| 代理行地址       | proxyBankAddress | string(256)   | O    | 代理行地址                 |
| 代理行swift code | proxySwiftCode   | string(32)    | O    | 代理行swift code           |
| 汇款附言         | remark           | string(64)    | O    | 汇款附言                   |
| 回调url          | callbackUrl      | string(256)   | M    | 回调通知Url                |
                                                                   
> 返回示例:

```json
{
    "merOrderNo":"8793478374",
    "bizFlow":"2184394993483534",
    "status": "PROCESS",
    "code": "",
    "message": ""
}
```
**4 响应字段**


| 名称       | Json标签   | 类型       | 属性 | 取值说明                   |
| ---------- | ---------- | ---------- | ---- | -------------------------- |
| 商户订单号 | merOrderNo | string(32) | M    | 商户传入本次交易唯一订单号 |
| 业务流水号 | bizFlow    | string(32) | M    | OTT生成的唯一流水号        |
| 状态       | status     | string(8)  | M    | 交易结果状态               |
| 结果码     | code       | string(8)  | M    | 交易结果代码               |
| 结果描述   | message    | string(64) | M    | 交易结果描述               |



###  5.9.2 提现交易历史查询

**1 功能描述**

| 交易代码 | TP3007                 |
| -------- | ---------------------- |
| 功能名称 | 提现历史交易查询       |
| 功能描述 | 提现历史交易查询       |
| 调用方式 | 实时接口               |
| 调用流程 | --                     |
| 应用场景 | 查询以往的提现历史交易 |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3007`

**Method：** `POST`

**3 请求字段**


| 名称         | Json标签   | 类型       | 属性 | 取值说明                             |
| ------------ | ---------- | ---------- | ---- | ------------------------------------ |
| 查询起始时间 | startTime  | Long       | O    | Unix13位时间戳，查询开始时间，闭区间 |
| 查询结束时间 | endTime    | Long       | O    | Unxi13位时间戳，查询结束时间，闭区间 |
| 业务订单号   | bizFlow    | String(32) | O    | OTT生成的唯一流水号                  |
| 商户订单号   | merOrderNo | String(32) | O    | 商户订单号                           |

<aside class="success">
若startTime与endTime没填，则bizFlow和merOrderNo中必填其一。若bizFlow和merOrderNo都没填，则startTime与endTime为必填，且间隔不能超过24小时
</aside>

> 返回示例:

```json
[
{
    "merOrderNo":"8793478374",
    "currency":"USD",
    "amount": 10000.00,
    "bankAccountNo": "6248348342123342",
    "bankName": "Citibank",
    "bankAddress": "Queens Road, New York",
    "swiftCode":"7643843",
    "proxyBankName":"",
    "proxyBankAddress": "",
    "proxySwiftCode":"",
    "remark":"xxx公司贸易提现款项",
    "bizFlow":"3213347378487348734",
    "status":"SUCCESS",
    "code":"S00000",
    "message":"成功",
    "crateTime": 1595228842000
},
{
    "merOrderNo":"8793478375",
    "currency":"USD",
    "amount": 10000.00,
    "bankAccountNo": "6248348342123342",
    "bankName": "Citibank",
    "bankAddress": "Queens Road, New York",
    "swiftCode":"7643843",
    "proxyBankName":"",
    "proxyBankAddress": "",
    "proxySwiftCode":"",
    "remark":"xxx公司贸易提现款项",
    "bizFlow":"3213347378487348734",
    "status":"SUCCESS",
    "code":"S00000",
    "message":"成功",
    "createTime": 1595228842000
}
]
```

**4 响应字段**


**返回对象是`List<WithdrawBean>`**

**WithdrawBean 的字段**

| 名称             | Json标签         | 类型          | 属性 | 取值说明                   |
| ---------------- | ---------------- | ------------- | ---- | -------------------------- |
| 商户订单号       | merOrderNo       | string(32)    | M    | 商户传入本次交易唯一订单号 |
| 币种             | currency         | string(3)     | M    | 提现币种，3位标准货币代码  |
| 金额             | amount           | decimal(18,2) | M    | 提现金额                   |
| 提现账户名称     | bankAccountName  | string(64)    | M    | 提现账户名称               |
| 银行账号/IBAN    | bankAccountNo    | string(64)    | M    | 提现银行账号或IBAN         |
| 银行名称         | bankName         | string(64)    | M    | 提现银行名称               |
| 银行地址         | bankAddress      | string(256)   | M    | 提现银行的地址             |
| swift code       | swiftCode        | string(32)    | M    | 提现银行的swift code       |
| 代理行名称       | proxyBankName    | string(64)    | O    | 代理行名称                 |
| 代理行地址       | proxyBankAddress | string(256)   | O    | 代理行地址                 |
| 代理行swift code | proxySwiftCode   | string(32)    | O    | 代理行swift code           |
| 汇款附言         | remark           | string(64)    | O    | 汇款附言                   |
| 回调地址         | callbackUrl      | string(256)   | M    | 回调地址                   |
| 业务流水号       | bizFlow          | string(32)    | M    | OTT生成的唯一流水号        |
| 交易结果状态     | status           | string(8)     | M    | 交易结果状态               |
| 交易结果码       | code             | string(8)     | M    | 交易结果码                 |
| 结果描述         | message          | string(64)    | M    | 交易结果描述               |
| 提现发起时间     | createTime       | long          | M    | 提现发起时间               |




### 5.9.3 提现结果通知

**1 功能描述**

|          |                                                                                                                               |
| -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| 交易代码 | TP2005                                                                                                                        |
| 功能名称 | 提现结果通知                                                                                                                  |
| 功能描述 | 提现结果异步通知                                                                                                              |
| 调用方式 | 通知接口                                                                                                                      |
| 调用流程 | --                                                                                                                            |
| 应用场景 | [提现交易](#5-9-1)发起成功且交易处理完毕后，将根据[提现交易](#5-9-1)参数内的回调Url进行回调通知最终结果。 |

<aside class="success">
本通知将按照间隔时间渐长的方式持续通知24小时.<br>商户应当以http 200返回，若通知持续时间结束仍未正常返回，则不再通知。 
</aside>

**2 请求地址**

**Url：** [提现交易](#5-9-1)中的 **callbackUrl**

**Method：** `POST`

> 请求示例:

```json
{
    "merOrderNo":"8793478374",
    "currency":"USD",
    "amount": 10000.00,
    "bankAccountNo": "6248348342123342",
    "bankName": "Citibank",
    "bankAddress": "Queens Road, New York",
    "swiftCode":"7643843",
    "proxyBankName":"",
    "proxyBankAddress": "",
    "proxySwiftCode":"",
    "remark":"xxx公司贸易提现款项",
    "bizFlow":"3213347378487348734",
    "status":"SUCCESS",
    "code":"S00000",
    "message":"成功"
}
```

**3 请求字段**

| 名称             | Json标签         | 类型          | 属性 | 取值说明                   |
| ---------------- | ---------------- | ------------- | ---- | -------------------------- |
| 商户订单号       | merOrderNo       | string(32)    | M    | 商户传入本次交易唯一订单号 |
| 币种             | currency         | string(3)     | M    | 提现币种，3位标准货币代码  |
| 金额             | amount           | decimal(18,2) | M    | 提现金额                   |
| 提现账户名称     | bankAccountName  | string(64)    | M    | 提现账户名称               |
| 银行账号/IBAN    | bankAccountNo    | string(64)    | M    | 提现银行账号或IBAN         |
| 银行名称         | bankName         | string(64)    | M    | 提现银行名称               |
| 银行地址         | bankAddress      | string(256)   | M    | 提现银行的地址             |
| swift code       | swiftCode        | string(32)    | M    | 提现银行的swift code       |
| 代理行名称       | proxyBankName    | string(64)    | O    | 代理行名称                 |
| 代理行地址       | proxyBankAddress | string(256)   | O    | 代理行地址                 |
| 代理行swift code | proxySwiftCode   | string(32)    | O    | 代理行swift code           |
| 汇款附言         | remark           | string(64)    | O    | 汇款附言                   |
| 业务流水号       | bizFlow          | string(32)    | M    | OTT生成的唯一流水号        |
| 交易结果状态     | status           | string(8)     | M    | 交易结果状态               |
| 交易结果码       | code             | string(8)     | M    | 交易结果码                 |
| 结果描述         | message          | string(64)    | M    | 交易结果描述               |



## 5.10 手续费

###  5.10.1 手续费交易历史查询

**1 功能描述**

| 交易代码 | TP3010                   |
| -------- | ------------------------ |
| 功能名称 | 手续费历史交易查询       |
| 功能描述 | 手续费历史交易查询       |
| 调用方式 | 实时接口                 |
| 调用流程 | --                       |
| 应用场景 | 查询以往的手续费历史交易 |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3010`

**Method：** `POST`

**3 请求字段**


| 名称         | Json标签  | 类型       | 属性 | 取值说明                                            |
| ------------ | --------- | ---------- | ---- | --------------------------------------------------- |
| 查询起始时间 | beginDate | Long       | O    | Unix13位时间戳，查询开始时间，闭区间                |
| 查询结束时间 | endDate   | Long       | O    | Unix13位时间戳，查询开始时间，闭区间                |
| 业务订单号   | batchNo   | String(32) | O    | OTT生成的唯一流水号                                 |
| 业务类型     | busiType  | String(6)  | O    | [业务类型](#6-1-5-biztype)                |
| 手续费状态   | status    | String(3)  | O    | 手续费状态 10: "未收取", 11: "已收取", 12: "已退回" |
| 第几页       | pageNum   | Integer    | O    | 查询第几页                                          |
| 每页多少条   | pageSize  | Integer    | O    | 每页多少条，每页最多支持100条                       |

                                                                
> 返回示例:

```json
{
	"pageNum": 1,
	"pageSize": 10,
	"total": 2343,
	"list": [ {
		"batchNo": "41200514566616790045",
		"merSingleBatchNo": "10011",
		"bizType": "C00002",
		"tradeCurrency": "PHP",
		"tradeAmt": 60000.0000,
		"feeCurrency": "USD",
		"feeTradeAmt": 2.0000,
		"status": "11",
		"tradeTime": "2020-05-14 19:57:33",
		"remark": "实时手续费流水"
	}]
}
```

**4 响应字段**


| 名称           | Json标签 | 类型               | 属性 | 取值说明 |
| -------------- | -------- | ------------------ | ---- | -------- |
| 当前页码       | pageNum  | Int                | M    | --       |
| 页显示数       | pageSize | Int                | M    | --       |
| 总数           | total    | Int                | M    | --       |
| 手续费信息集合 | list     | `List<FeeFlowRes>` | M    | --       |

**FeeFlowRes 的字段**

| 名称                   | Json标签         | 类型          | 属性 | 取值说明                                            |
| ---------------------- | ---------------- | ------------- | ---- | --------------------------------------------------- |
| 订单号                 | batchNo          | string(32)    | M    | 订单号                                              |
| 商户订单号             | merSingleBatchNo | string(32)    | O    | 商户传入本次交易唯一订单号                          |
| 业务类型               | bizType          | String(6)     | M    | [业务类型](#6-1-5-biztype)                |
| 手续费币种             | feeCurrency      | String(3)     | O    | 手续费币种，3位标准货币代码                         |
| 手续费币种对应交易金额 | feeTradeAmt      | decimal(18,2) | M    | 手续费币种对应交易金额                              |
| 手续费状态             | status           | string(2)     | M    | 手续费状态 10: "未收取", 11: "已收取", 12: "已退回" |
| 交易币种               | tradeCurrency    | string(3)     | M    | 交易币种，3位标准货币代码                           |
| 交易金额               | tradeAmt         | decimal(18,2) | M    | 交易金额                                            |
| 交易时间               | tradeTime        | Date          | M    | 交易时间                                            |
| 备注                   | remark           | string(1024)  | M    | 备注     


## 5.11 账务

### 5.11.1 账户余额查询

**1 功能描述**

| 交易代码 | TP3004           |
| -------- | ---------------- |
| 功能名称 | 账户余额查询     |
| 功能描述 | 当前账户余额查询 |
| 调用方式 | 实时接口         |
| 调用流程 | --               |
| 应用场景 | 当前账户余额查询 |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3004`

**Method：** `POST`

**3 请求字段**


| 名称 | Json标签 | 类型      | 属性 | 取值说明                         |
| ---- | -------- | --------- | ---- | -------------------------------- |
| 币种 | currency | String(3) | O    | 币种，若不传则为查询所有币种账户 |

                                                                   
> 返回示例:

```json
[
    {
        "currency": "USD",
        "balance": "2000.00",
        "status":"on"
    },
    {
        "currency": "CNY",
        "balance": "8231.22",
        "status":"off"
    }
]

```
**4 响应字段**


 接口返回对象为: **`List<CurrencyBalance>`**

**CurrencyBalance 字段：**

| 名称     | Json标签 | 类型      | 属性 | 取值说明                        |
| -------- | -------- | --------- | ---- | ------------------------------- |
| 币种     | currency | String(3) | M    | 币种                            |
| 余额     | balance  | String(3) | M    | 账户余额                        |
| 账户状态 | status   | String(3) | M    | 账户状态: on 为启用， off为禁用 |



### 5.11.2 账务流水交易查询

**1 功能描述**

| 交易代码 | TP3009                     |
| -------- | -------------------------- |
| 功能名称 | 账务流水历史交易查询       |
| 功能描述 | 账务流水历史交易查询       |
| 调用方式 | 实时接口                   |
| 调用流程 | --                         |
| 应用场景 | 查询以往的账务流水历史交易 |

**2 请求地址**


**Url：** `https://{baseUrl}/api/tp3009`

**Method：** `POST`

**3 请求字段**


| 名称         | Json标签  | 类型       | 属性 | 取值说明                                |
| ------------ | --------- | ---------- | ---- | --------------------------------------- |
| 查询起始时间 | beginDate | Long       | O    | Unix13位时间戳，查询开始时间，闭区间    |
| 查询结束时间 | endDate   | Long       | O    | Unix13位时间戳，查询开始时间，闭区间    |
| 业务订单号   | batchNo   | String(32) | O    | OTT生成的唯一流水号                     |
| 币种         | currency  | String(3)  | O    | 币种                                    |
| 收支类型     | flowType  | String(3)  | O    | 收支类型 1: "入金", 2: "出金"           |
| 流水类型     | busiType  | String(3)  | O    | [6.1.6流水类型](#6-1-6-busitype) |
| 第几页       | pageNum   | Integer    | O    | 查询第几页                              |
| 每页多少条   | pageSize  | Integer    | O    | 每页多少条，每页最多支持100条           |

> 返回示例:

```json
{
	"pageNum": 1,
	"pageSize": 10,
	"total": 9668,
	"list": [{
		"currency": "USD",
		"busiType": "C11",
		"busiDate": "2020-05-28 19:32:14",
		"inAmount": null,
		"outAmount": 7.0000,
		"vailAmount": 5572.3100,
		"batchNo": "41200528653124170019"
	}, {
		"currency": "USD",
		"busiType": "C07",
		"busiDate": "2020-05-27 17:52:56",
		"inAmount": null,
		"outAmount": 2218.0000,
		"vailAmount": 5628.3100,
		"batchNo": "41200527728820950004"
	}]
}
```

**4 响应字段**


| 名称             | Json标签 | 类型               | 属性 | 取值说明 |
| ---------------- | -------- | ------------------ | ---- | -------- |
| 当前页码         | pageNum  | Int                | M    | --       |
| 页显示数         | pageSize | Int                | M    | --       |
| 总数             | total    | Int                | M    | --       |
| 账务流水信息集合 | list     | `List<CurFlowRes>` | M    | --       |

**CurFlowRes 的字段**

| 名称         | Json标签   | 类型          | 属性 | 取值说明                                |
| ------------ | ---------- | ------------- | ---- | --------------------------------------- |
| 账务流水订单 | batchNo    | string(32)    | M    | 账务流水订单                            |
| 币种         | currency   | string(3)     | M    | 账务流水币种，3位标准货币代码           |
| 流水类型     | busiType   | String(3)     | M    | [6.1.6流水类型](#6-1-6-busitype) |
| 入金         | inAmount   | decimal(18,2) | M    | 入金金额                                |
| 出金         | outAmount  | decimal(18,2) | M    | 出金金额                                |
| 可用金额     | vailAmount | decimal(18,2) | M    | 可用金额                                |
| 交易时间     | busiDate   | Date          | M    | 交易时间                                |




## 5.12 配置

### 5.12.1 回调地址设置

**1 功能描述**

|          |                                              |
| -------- | -------------------------------------------- |
| 交易代码 | TP1014                                       |
| 功能名称 | 对于通知接口，设置回调地址                            |
| 功能描述 | 对于通知接口，设置回调地址                   |
| 调用方式 | 实时接口                                     |
| 调用流程 | --                                           |
| 应用场景 | 对于无交易传参的callback接口，单独设置回调地址 |

**2 请求地址**

**Url：** `https://{baseUrl}/api/tp1014`

**Method：** `POST`

> 请求示例:

```json
{
        "tradeCode":"TP2007",
        "callbackUrl":"https://xxxxx.xxxx.com/callback"
}
```                                                                 

**3 请求字段**

| 名称                     | Json标签              | 类型        | 属性 | 取值说明                                                                     |
| ------------------------ | --------------------- | ----------- | ---- | ---------------------------------------------------------------------------- |
| 回调地址              | callbackUrl               | string(64)          | M    | 回调地址                                                                    |
| 接口类型              | tradeCode               | string(6)          | M    | 回调的接口类型                                       |

> 返回示例:

```json
{
        "code":"SUCC"
}
```

**4 响应字段**


| 名称       | Json标签 | 类型        | 属性 | 取值说明                                                          |
| ---------- | -------- | ----------- | ---- | ----------------------------------------------------------------- |
| 结果码     | code     | string(6)   | M    | SUCC代表成功 |



#  6 附录

## 6.1 字段说明
### 6.1.1 paymentType 交易类型

| 字段值 | 说明       | 备注 |
| ------ | ---------- | ---- |
| B2B    | 企业对企业 | --   |
| B2C    | 企业对个人 | --   |
| C2B    | 个人对企业 | --   |
| C2C    | 个人对个人 | --   |

### 6.1.2 tradeCodeType 交易编码 

| 字段值         | 说明                             | 备注                                  |
| -------------- | -------------------------------- | ------------------------------------- |
| TRADE          | 线下一般货物贸易                 | 一般贸易                              |
| STAY           | 酒店费用                         | 酒店住宿                              |
| AIRLINE_TICKET | 旅行                             | 航空机票                              |
| STUDY_ABROAD   | 教育相关的学生开支               | 境外留学                              |
| SOFTWARE       | 咨询费、技术服务、学术费、专家费 | 管理咨询，软件开发                    |
| LOGISTICS      | 货物物流费                       | 物流费                                |
| INFO_CHARGES   | 信息服务费                       | 软件类                                |
| ADVER_SERVICE  | 广告或公关费用                   | 广告服务,公共关系服务，国际会展，会议 |
| EXPORTED_GOODS | 货款支付                         | 跨境电商                              |
| SALARY         | 工资或佣金支付                   | 劳务类                                |
| ONLINE_GAME    | 网络游戏装备                     | 游戏                                  |
| E_COMMERCE     | 电商                             | 电商                                  |

### 6.1.3 payMethod 支付方式

| 字段值           | 说明               | 备注     |
| ---------------- | ------------------ | -------- |
| cash_on_delivery | 支付方式为货到付款 | 货到付款 |
| advance          | 支付方式为预付款   | 预付款   |



### 6.1.4 purpose 付款目的

| 字段值 | 汇款目的（en）                                                                                              | 汇款目的（zh）                           |
| ------ | ----------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| 1      | Transfer to own account                                                                                     | 付款至自己账户                           |
| 2      | Family Maintenance                                                                                          | 赡家款                                   |
| 3      | Education-related student expenses                                                                          | 教育相关的学生开支                       |
| 4      | Medical Treatment                                                                                           | 医疗费                                   |
| 5      | Hotel Accomodation                                                                                          | 酒店费用                                 |
| 6      | Travel                                                                                                      | 旅行                                     |
| 7      | Utility Bills                                                                                               | 支付水电煤等基础设施账单                 |
| 8      | Repayment of Loans                                                                                          | 归还借款                                 |
| 9      | Tax Payment                                                                                                 | 支付税款                                 |
| 10     | Purchase of Residential Property                                                                            | 购买住宅                                 |
| 11     | Payment of Property Rental                                                                                  | 支付房屋租金                             |
| 12     | Insurance Premium                                                                                           | 保险预付                                 |
| 13     | Product indemnity insurance                                                                                 | 产品保险                                 |
| 14     | Insurance Claims Payment                                                                                    | 支付保费                                 |
| 15     | Mutual Fund Investment                                                                                      | 共同基金投资                             |
| 16     | Investment in Shares                                                                                        | 股权投资                                 |
| 17     | Donations                                                                                                   | 捐赠                                     |
| 18     | Information Service Charges                                                                                 | 信息服务费                               |
| 19     | Advertising & Public relations-related expenses                                                             | 广告或公关费用                           |
| 20     | Royalty fees, trademark fees, <br>patent fees, and copyright fees                                           | 忠诚服务费、商标费、专利费以及著作权费用 |
| 21     | Fees for brokers, front end fee, <br>commitment fee, guarantee fee and custodian fee                        | 交易费、担保费、保理费                   |
| 22     | Fees for advisors, technical assistance, <br>and academic knowledge, including remuneration for specialists | 咨询费、技术服务、学术费、专家费         |
| 23     | Representative office expenses                                                                              | 代表处开支                               |
| 24     | Construction costs/expenses                                                                                 | 建筑建设费用                             |
| 25     | Transportation fees for goods                                                                               | 商品转移费                               |
| 26     | For payment of exported goods                                                                               | 出口货物货款支付                         |
| 27     | Delivery fees for goods                                                                                     | 商品物流费                               |
| 28     | General Goods Trades - Offine trade                                                                         | 常规线下货物贸易                         |
| 29     | Other services charges                                                                              | 其他服务贸易支出                   |
| 30     | Salary / Commission Payment                                                                         | 工资或佣金支付                         |
| 31     | Fixed Maintenance Expenses                                                                        | 定期维护费用                      |
| 99     | Other fees (Please specify)                                                                       | 其他费用（请详述）                     |

### 6.1.5 bizType 业务类型

| 字段值 | 说明            |
| ------ | --------------- |
| 000008 | 电商收款手续费  |
| 000012 | VA月度管理费    |
| 000013 | 贸易收款手续费  |
| 000015 | 平台月度维护费  |
| C00001 | 跨境人民币入境" |
| C00002 | 全球下发        |
| C00003 | 平台入金手续费  |
| C0000  | 平台提现手续费  |

### 6.1.6 busiType 流水类型

| 字段值 | 说明          |
| ------ |-------------|
| C00    | 账务流水        |
| C01    | 换汇          |
| C02    | 换汇退回        |
| C05    | 人民币付款       |
| C06    | 人民币付款退回     |
| C07    | 外币付款        |
| C08    | 外币付款退回      |
| C09    | 提现          |
| C10    | 提现退回        |
| C11    | 手续费         |
| C12    | 手续费退回       |
| C13    | 收款          |
| C20    | 账户间转账       |
| C21    | 账户间转账手续费    |
| C22    | 入账费         |
| C23    | 平台管理费       |

### 6.1.7 tradePurpose 汇款用途代码

| 字段值              | 说明           |
|--------------------| -------------- |
| GOODSTRADE         | Goods Trade    |
| PLANETICKET        | Plane Ticket      |
| HOTELACCOMMODATION | Hotel Accommodation    |
| STUDYABROAD        | Study abroad (long)   |
| STUDYABROAD2       | Study abroad (short) |
| TRAVEL             | Travel (private)    |
| TRAVEL2            | Travel (public)  |
| SOFTWARE           | Software Service      |
| COMMUNICATION      | Coummunication    |
| TRANSPORT          | Logistics (import sea transportation)     |
| TRANSPORT2         | Logistics (export sea transportation)   |
| TRANSPORT3         | Logistics (export air transportation)      |

### 6.1.8 sourceFunds 资金来源

| 字段值 | 说明           |
|-----| -------------- |
| 0   | UBO (最终受益人) 资本投资UBO    |
| 1   | 经营多年的业务收益 / 贷款收入      |
| 2   | 公司向银行贷款    |
| 3   | UBO 继承遗产 / 家庭信托基金   |
| 4   | 家庭礼物或非股东礼物 |
| 5   | 保险收益 / 到期结算    |
| 6   | 法律案件的赔偿金  |
| 7   | 买卖股票投资收益 / 回报      |
| 8   | 奖金（政府或收据式彩票）    |
| 9   | 赌博或 奖金（非收据式彩票）     |
| 10  | 出售公司或公司股票的收益   |
| 11  | 商业或住宅物业的销售      |
| 12   | 出售公司投资收拥有的收益      |

### 6.1.9 paymentPurpose 付款目的

| 字段值 | 说明           |
|-----| -------------- |
| 0   | 建筑和装修（商业或住宅都适用）    |
| 1   | 支付中国或国外供应商      |
| 2   | 珠宝和手表出售或购买的支付    |
| 3   | 定期工资和佣金支付   |
| 4   | 法律、会计、秘书, 顾问, 专家费 |
| 5   | 技术维护/系统开发服务的支付    |
| 6   | 个人或家庭日常开支  |
| 7   | 行政和办公室日常运营开支      |
| 8   | 房地产投资    |
| 9   | 有形资产托管     |
| 10  | 汇款至同名账户   |
| 11  | 版权、商标, 牌照, 许可证的支付      |
| 12  | 差旅住宿费用（公司和个人均适用） |
| 13  | 水电煤气, 公共事业缴费 |
| 14  | 医疗和住院费用 |
| 15  | 教育费关包括大学学费, 寄宿费, 研讨会 |
| 16  | 写字楼、商业及住宅租赁相关 |
| 17  | 商户结算 |
| 18  | 服务平台月费, 定期维护费用 |
| 19  | 物流, 仓储, 运输费 |
| 20  | 商业（个人）税款相关支付-修改 |
| 21  | 保险索赔、保费、退保和赔偿 |
| 22  | 信贷, 归还借款信贷 |
| 23  | 其他金融投资产品 |
| 24  | 付款家庭成员/直系亲属 |
| 25  | 金钱捐赠和礼物 |
| 26  | 所有其他类型的短期 (一年以下)投资 |
| 27  | 无形资产托管 |
| 28  | 汇款给非关联第三方公司和非亲属 |

### 6.1.10 customerIdentity 客户身份

| 字段值   | 说明                                    |
|--------|---------------------------------------|
| 0      | 法人代表                                  |
| 1      | 公司董事                                  |
| 2      | 持股25%以上的股东                          |
| 3      | 以上都不是                                |

## 6.2 解决方案

<a href="https://tiger-space.sgp1.digitaloceanspaces.com/%E6%8D%A2%E4%BB%98%E7%B1%BB%E5%AE%A2%E6%88%B7%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88.pdf" target="_blank" download>换付类客户解决方案</a>

<a href="https://tiger-space.sgp1.digitaloceanspaces.com/%E6%94%B6%E6%AC%BE%E5%B9%B3%E5%8F%B0%E7%B1%BB%E5%AE%A2%E6%88%B7%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88.pdf" target="_blank" download>收款平台类客户解决方案</a>