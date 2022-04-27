---
title: OTT PAY HK International Payment API Document

language_tabs: # must be one of https://git.io/vQNgJ
  - CODE
  
toc_footers:
  - Copyright © 2022-OTTPay HK

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the OTTPay HK API
---

# OTTPay HK International Remittance Document

# 1 Overview
## 1.1 Purpose of writing

The purpose is to agree on the business interface between the merchant and the Ottpayhk payment system. Including communication protocol, transaction interface specification, file format, encryption and summary specification. refer to
Lead merchant developers to develop in accordance with this specification, and to interface with the Ottpayhk payment system.

## 1.2 Definitions and acronyms

UML timing diagram

![UML Timing Diagram](https://docs.hksd.ottpayhk.com/umlEn.png "UML Timing Diagram")


## 1.3 Platform test/launch preparations

**Test joint debugging stage**

Before the completion of the platform development and the system joint debugging test, you need to prepare the following items:
1. The platform generates the **RSA** key pair of the test environment, and sends the public key to Ottpayhk;
2. Apply to open the test environment platform number;

**On-line stage**

3. The platform generates an RSA key pair for the production environment and provides the public key to Ottpayhk;
4. Provide platform server IP address to Ottpayhk
5. Apply for the production environment platform number


## 1.4 Update log

**1.0.30 Additional refund notification interface 2021-08-06**

1. Added the refund notification interface for RMB and international remittances (tp2010)

**1.0.29 Added trade collection related interface 2021-06-23**

1. Added trade order application tp1012/receiving flow and trade order association tp1013/callback address setting tp1014
2. Notification of the arrival of trade receipts tp2007/Notification of the result of the trade order application tp2008/Notification of the result of the collection flow and the association result of the trade order tp2009
3. Newly added trade order application information query interface tp3013/newly added collection flow and trade order association query interface tp3014/trade receipt VA entry query interface tp3015
4. For RMB payment tp1001, increase the required mobile phone number

**1.0.28 Modification 5.1.7 Merchant access network 2021-06-18**

1. Modify the merchant entry field

**1.0.27 Modify tp1001 interface request field 2021-06-01**

1. Add the field of restore materials for payReduceList (only for games, e-commerce, and general trade)

**1.0.26 Added 5.1.10 VA account opening application tp1011 and 5.3.16 VA account query tp3012 2021-05-31**

1. Added 5.1.10 VA account opening application tp1011.
2. Added 5.3.16 VA account query tp3012.

**1.0.25 add 5.1.9 inter-merchant transfer interface tp1010 2021-04-21**

1. Added the 5.1.9 inter-merchant transfer interface tp1010, which supports merchants that are also registered for OTT to complete internal transfers.

**1.0.24 Modify tp1004 interface request field 2021-03-17**

1. In tp1004 international remittance, the debitAmount debit amount is added, which can support two types of locked debit amount or payment amount.

**1.0.23 Modify tp3005 interface return field 2021-03-15**

1. Update the purpose of remittance

**1.0.22 Modify tp3005 interface return field 2021-03-09**

1. Add selectOption enumeration value return

**1.0.21 Modify tp1001 interface request field 2021-01-12**

1. New required field payeeName in PayOrderRequest
2. cNAPSCode changed to the only required item

**1.0.20 Modify tp3006 interface return field 2020-11-12**

1. The return code and message of tp3006 are modified to resCode and resMessage

**1.0.19 Add a one-day price inquiry interface 2020-10-12**

1. Added 5.3.15 one-day price inquiry

**1.0.18 Added merchant query recharge flow list, accounting flow list and handling fee flow list 2020-08-06**

1. Added 5.3.12 recharge transaction history query
2. Added 5.3.13 Account Flow Transaction Query
3. Added 5.3.14 Transaction Fee Transaction History Query

**1.0.17 Add merchant network access interface & modify RMB interface 2020-07-31**

1. Added 5.1.7 Merchant Network Access/5.1.8 Merchant Network Access Information Improvement/5.2.4 Merchant Network Access Results Notification
2. 5.1.1 FeeFlag is added to the RMB payment request parameter, feeCurrency/feeAmount/actualPayAmount is added to the return parameter
3. 5.3.1 RMB payment query, add feeCurrency/feeAmount/actualPayAmount to the return parameter

**1.0.16 Notification of new tp2006 international remittance payment voucher 2020-06-04**


**1.0.15 tp3005 adds bank list field 2020-04-22**


**1.0.14 International Remittance Modification 2020-03-20**

1. International remittance increase remittance postscript
2. Update purpose
3. Update purpose

**1.0.13 International remittance adds associated fx order field 2020-03-17**


**1.0.12 Modify RMB payment interface fields 2020-03-01**


**1.0.11 FX and international remittance modification 2020-02-28**

1. The FX interface adds support for T0 T1 lock exchange
2. Modifications to the relevant interface fields of international remittance: add the purpose of remittance

**1.0.10 Modification of application fields for RMB issuance 2020-02-13**

1. New fields in the RMB issuance application interface
2. The first payee submits business license and legal person photo

**1.0.9 New field respCode for callbacks issued in RMB 2020-01-22**


**1.0.8 Add international remittance related interfaces 2020-01-17**


**1.0.7 Add the interface number query interface 2020-01-16**


**1.0.6 RMB payment added acceptance status 2019-12-30**


**1.0.5 Modify batch payment request 2019-12-26**


**1.0.4 Add FX related interfaces 2019-12-18**


**1.0.3 Modify the batch upload interface parameters 2019-12-17**


**1.0.2 Modify the batch upload interface 2019-12-16**


**1.0.1 adds 5.3.1 and 6.1 2019-05-13**


**1.0.0 New 2019-04-29**



# 2. Communication protocol
## 2.1 Agreement Agreement

1. The communication between the platform and Ottpayhk is based on the **HTTPS1.2** protocol, and the message organization format adopts the **json** specification.
2. The messages of both parties are sent in cipher text, and the cipher text, session key cipher text and signature of the message must be transmitted to the other party at the same time.
3. The platform and Ottpayhk are each other's client and server. According to the requirements of the application, the platform can take the initiative to initiate transaction requests as the client, Ottpayhk
   To answer. Ottpayhk can also initiate a transaction request on its own initiative, and the platform will respond. The platform needs to set the request address to receive Ottpayhk in advance when opening an account.
4. The client submits the request using the POST form **(Content-Type:application/json)** submission, and the content adopts **UTF-8** encoding.
5. The request and response consist of five domains: **merchantNo**=platform code, **jsonEnc**=message ciphertext, **keyEnc**=session key ciphertext, **sign**=message Signature


# 3 Transaction Interface Specification

## 3.1 Request message

Transaction messages follow the JSON specification. Example:

```json
{
    "head":{
        "version":"1.0.1", //---Message version number
        "tradeType":"00", //--00 request message
        "tradeTime":"1551341750", //---request time, 10-digit unix timestamp
        "tradeCode":"TP1001", //–Request transaction code
        "language":"cn", //–Language
    },
    "body":{
        //...
    }
}
```
1. The request message consists of two parts: the request message header and the request message body. The request message header information is in the message header (head. node, request message body information
   In the body of the message (body. node.
2. The message header is the same for every transaction. For the filling standard of request message header information, please refer to the "Common Message Header Description" section.
3. The message body is different according to the interface definition of each transaction. For the definition of request message body, please refer to the chapter "Business Transaction Interface". According to the connection of each transaction
   The port defines the assembly and analysis request message body.
4. When the client requests the message to be sent, POST submits four parameters: **merchantNo**=platform code; **jsonEnc**=message ciphertext; **keyEnc**=session key encryption
   Text; **sign**=message signature, where **merchantNo** is the clear text of the merchant number assigned by Ottpayhk to the cooperative platform, and the content of the **jsonEnc** parameter is the entire message plus
   The **hexadecimal string** after encryption, the **keyEnc** parameter is the cipher text of the message encryption session key, and the content of the **sign** parameter is the signature of this message. <br>

After the server receives the request and obtains the parameters according to HTTPS, it is processed according to the following steps:<br>
Step 1: Use the decrypted session key<br>
Step 2: Decrypt the ciphertext message to get the message civilization message;<br>
Step 3: Verify the signature. After the signature is passed, the content of the message is parsed. <br>

For message encryption, signature and verification methods, please refer to the chapter "Encryption and Signature Specifications"

**Note: For fields defined in the business transaction interface, regardless of whether the value is empty or not, the json tag of the field needs to be uploaded. **

## 3.2 Response message

Transaction messages follow the JSON specification.

> Example:

```json
{
    "head":{
        "version":"1.0.0", //---Message version number
        "tradeType":"01", //--01 response message
        "tradeTime":"1551341750", //---response time, 10-bit unix timestamp
        "tradeCode":"TP1001", //---corresponding to the requested transaction code
        "respCode":"S00000", //---request return code
        "respDesc":"Request successful", //--return code of request
    },
    "body":{
        //...
    }
}
```
1. The transaction response message consists of two parts: the response message header and the response message body. The response message header information is in the message header (head) node, and the response message body
   The information is in the body node.
2. The message header is the same for every transaction. Please refer to the "Common Message Header Description" section for the filling standard of the response message header information.
3. The message body is different according to the interface definition of each transaction. Please refer to the chapter "Transaction Message Interface" for the definition of response message body. Need to follow the interface of each transaction
   Define the assembly and analysis of the response message body.
4. The response message when the transaction is successful, the respCode of the message header is S00000, and the respDesc ​​is "transaction successful". At this time, the body node of the message is based on
   The actual business needs to be empty or not.
5. For the response message when the transaction is wrong, the error code and error information are filled in the respCode (return code) and respDesc ​​(return information description) fields in the header of the message
   Medium; the body node of the message is empty.
1. When the server responds to the message return, it returns the merchant number, message ciphertext, session key and signature as a standard json string **{"merchantNo":"",jsonEnc":"","keyEnc": "","sign":""}**, and then write the byte stream of the string to the return object of http. When the client receives the response from the server, the byte stream returned by the HTTP server is in accordance with the characters in the corresponding format String to get the message and summary parameters, and the parameters get
   After fetching, the digest is verified first, and the content of the message is parsed after the verification is passed.

Please refer to the "[Encryption and Signature Specification](#_4-Encryption and Signature Specification)" chapter for the message digest generation and verification method.

# 4 Encryption and signature specifications

## 4.1 Principle

1. All transaction messages need to be encrypted, signed and verified.
2. After receiving the message, both the requester and the responder need to perform signature verification, that is, regenerate the signature according to the agreed algorithm, and then compare it with the received signature.
   The content of the message can be analyzed after the comparison is passed. Otherwise, the content of the message or file may be tampered, partially lost, or forged.
3. Message encryption algorithm: DES/CBC/PKCS5Padding
4. Session key generation: KeyGenerator generation
5. Session key encryption algorithm: RSA/ECB/PKCS1Padding
6. Signature algorithm: SHA1withRSA

## 4.2 RSA key pair acquisition

> shell

```bash
openssl genrsa –out rsa_private_key_2048.pem 2048
#Generate rsa private key, encoded with X509, specify the number of bits of the generated key: 2048

openssl pkcs8 –topk8 –in rsa_private_key_2048.pem –out pkcs8_rsa_private_key_2048.pem –nocrypt
#Convert the rsa private key generated in the previous step into PKCS#8 encoding

openssl rsa –in rsa_private_key_2048.pem –out rsa_public_key_2048.pem –pubout
#Export rsa public key, encoded in X509, merchants need to follow the above steps to generate the merchant's public key pem and send it to Ottpayhk,
#Or the merchant can directly ask Ottpayhk for the key pair generation script to generate the public and private keys required by the merchant.
#Ottpayhk also needs to send the corresponding public key pem generated by Ottpayhk to the merchant.
```

For the merchant, it is necessary to generate the merchant's own RSA key pair (including the public key and the private key), in which the private key is kept by the partner, and the public key is provided to Ottpayhk.

For Ottpayhk, it is necessary to generate a corresponding public-private key pair for each merchant. Among them, the private key Ottpayhk keeps itself, and the public key needs to be provided to the merchant.



## 4.3 Message Encryption and Signature

![Encryption and Signature](https://docs.hksd.ottpayhk.com/signEn.png "Encryption and Signature")

1. The request or response **Json** message civilization text (**UTF-8 encoding**. Use the sender’s private key to sign (**SHA1withRSA**. ), and convert the signature result to **HEX characters String ** to get the sign domain.
2. Use the **KeyGenerator** generator to generate **DES** encrypted session key **SK**;
3. Use **SK** to encrypt **Json** plaintext (**DES/CBC/PKCS5Padding**., and convert the encrypted result into **HEX string**, get **jsonEnc**
   area.
4. Use the receiver's public key to encrypt the session key SK (**RSA/ECB/PKCS1Padding**., and convert the result into a **HEX string** to get **keyEnc**
   area.

## 4.4 Message decryption and signature verification


![Decryption and Sign Verification](https://docs.hksd.ottpayhk.com/checkSignEn.png "Decryption and Sign Verification")


1. Convert the **keyEnc** field to a binary byte array, and use the private key set by the receiver to pair the session key to obtain the plain text **SK**;
2. Convert **jsonEnc** and into a binary byte array, use the session key **SK** obtained in the previous step to decrypt, and get the plaintext json;
3. Use the plaintext decrypted in the previous step, the sender's public key, and the sign field data to verify the validity of the signature.


# 5 Business Interface

This chapter describes the business interface related to merchants accessing Ottpayhk. <br>
M means mandatory field, O means optional field

## 5.1 Trading Interface
### 5.1.1 RMB payment

**1 Function description**


|Transaction Code   | TP1001    |
|----|----|  
|Function name      | RMB payment |
|Function description | Initiate a RMB payment request and send the payee information to Ottpayhk |
|Calling method | Real-time interface |
|Calling process | First submit the restored materials to Ottpayhk via sftp, and then call this interface to send payment information |
|Application scenarios | Need to pay RMB to domestic cardholders |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp1001`

**Method:** `POST`

**3 Request field**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Order number | merOrderNo | String(32) | M | The unique order number of this transaction |
| Restored material path | fileUrlPath | String(128) | O | Restored material path uploaded to sftp file server |
| Transaction Type | paymentType | String | M | [Parameters are detailed in the field description](#_6-1-1-paymenttype-transaction type) |
| Callback address | callbackUrl | String | M | Address used for result notification |
| Payee List | payOrderList | `List<PayOrderRequest>` | M | Payment Information |
| Fee Flag | feeFlag | String(1) | O | When the fee is charged in real time, the user can choose whether to deduct internally or externally. <br/>1: External buckle, 0: Internal buckle |
| Restore material list| payReduceList| `List<payReduceList>` | O | Fill in when the payment information transaction code is game, e-commerce, general trade [parameters see field description](#_6-1-2-tradecodetype-transaction code )|

**PayOrderRequest information**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Single order number | merSingleNo | String | O | Order number corresponding to a single payment record |
| Beneficiary Account Number | payeeAccountNo | String | M | Beneficiary Bank Account Number |
| Payee Name | payeeName | String | M | Payee Bank Account Name |
| ID number / unified social credit code | identity | String | M | If the payee account type is 0, fill in the ID number, if it is 1, fill in the unified social credit code |
| Amount | amount | Decimal | M | Payment amount, in cents, for example: If you pay 200.00 yuan, you should fill in 20000 and the minimum is 1 |
| Cooperative Number | cNAPSCode | String | M | Recipient Bank Cooperative Number |
| Mobile Number | mobile | String | M | Mobile Number |
| Transaction Code | tradeCodeType | String | M | [Parameters are detailed in the field description](#_6-1-2-tradecodetype-transaction code) |
| Payment method | payMethod | String | O | [Parameters are detailed in the field description] (#_6-1-3-paymethod-payment method), <br>tradeCodeType is TRADE and paymentType is B2B, it cannot be empty, <br>default : Cash_on_delivery |
| Declaration Currency | declarationCurrency | String | O | The payMethod value is cash_on_delivery and cannot be empty, the default is CNY |
| Advance Proportion | advanceProportion | Float | O | payMethod value is advance, 0 <advanceProportion <1, up to two decimal places |
| Settlement period | settlementDate | String | O | payMethod value is advance Settlement period cannot be empty unit day |
| Name of payer | senderName | String | M | Name of real payer |
| Payer’s company registration number | senderIncorporationNo | String | M | Payer’s company registration number |
Payment registration place | registrationRegion | String | M | Payment area swift country area |
| Payer's bank name | senderBankName | String | M | Payer's bank name |
| Funding source | sourceFounds | String | M | Optional |
| Payer's bank account | senderBankAccountNo | String | M | Payer's bank account optional |

**payReduceList information**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Order number | orderNo | String | M | Order number corresponding to a single payment record (not more than 32 digits) |
| Order Currency | orderCurrency | String | M | Receiving Currency |
| Order amount | orderAmount | Decimal | M | Payment amount, in minutes, for example: If you pay 200.00 yuan, you should fill in 20000 and the minimum is 1 |
| Order Date | orderDate | String | M | Payment date, the format is "yyyy-MM-dd" |
| Payee Name | sellerName | Decimal | M | Payee Name |
| Payee ID Number | sellerId | String | M | Payee ID Number (The length does not exceed 18 digits) |
| Buyer Name | buyerName | String | O | Fill in when e-commerce transaction type |
| Product Name | goodsName | String | M | Product Name |
| Commodity category | goodsCategoryncy | String | M | Commodity category |
| Number of products | goodNumber | String | O | Number of products |
| Purpose of remittance | purpose | String | O | Purpose of payment |
| Buyer Bank Name | buyerBankName | String | O | Buyer Bank Name |
| Buyer Bank Card Number | buyerBankCard | String | O | Buyer Bank Card Number |
| Transaction Method | sendType | String | O | Delivery Method |
| Courier Amount | sendAmount | Decimal | O | Courier Amount, the unit is minutes, for example: If you pay 200.00 yuan, you should fill in 20000 and the minimum is 1 |
| Tax amount | taxAmount | Decimal | O | Tax amount, in cents, for example: If you pay 200.00 yuan, you should fill in 20000 and the minimum is 1 |
| Other Amount | otherAmount | Decimal | O | Other Amount, the unit is cents, for example: If you pay 200.00 yuan, you should fill in 20000 and the minimum is 1 |
| Notifier Type | applyType | String | O | Notifier Type |



> Return example:

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

**4 Response field**

If the respCode in the response header is S00000, the acceptance is successful. Please wait for the asynchronous notification (see [5.2.1 Payment callback] (#_5-2-1-System notifies the merchant of the payment result)) of the payment result. Message style: when
When respCode is S00000:

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Order number | merOrderNo | String(32) | M | Return as is |
| Business serial number | bizFlowNo | String(32) | M | The unique business serial number generated by Ottpayhk, which corresponds to the order number one-to-one |
| Status | status | String(1) | M | "0": "Accept", "1": "Success", "2": "Failure", "3": "Processing" |
| Fee currency | feeCurrency | String(3) | O | fee currency charged |
| Fee currency | feeAmount | Decimal | O | Fee amount charged |
| Actual payment amount | actualPayAmount | Decimal | O | Actual payment amount |

### 5.1.2 List price query interface

**1 Function description**


| Transaction Code | TP1002 |
|----|----|
| Function name | List price query |
| Function description | Query the FX quote price of a certain currency |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | Before FX trading, you need to inquire first |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp1002`

**Method:** `POST`

> Request example:

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

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Merchant order number | merOrderNo | String(32) | M | Merchant-defined unique order number |
| Sell Currency | sellCurrency | String(3) | O | Sell Currency |
| Buy currency | buyCurrency | String(3) | M | Buy currency |
| Lock Direction | lockDirection | String(4) | M | Lock the currency to sell or buy; Pass SELL to lock the amount of the sold currency, and pass BUY to lock the amount of the purchased currency |
| Locked amount | amount | String(20) | M | Specified FX amount |
| Lock type | lockType | String(2) | O | Optional field: currently supports optional T0, T1 |





> Return example:

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

**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Sell Currency | sellCurrency | String(3) | M | Sell Currency |
| Buy currency | buyCurrency | String(3) | M | Buy currency |
| Exchange rate | rate | String(18) | M | Exchange rate quote |
| Sell Amount | sellAmount | String(18) | M | Sell Amount |
| Buy Amount | buyAmount | String(20) | M | Buy Amount |
| Quote ID | quoteId | Long | M | Quote ID |
| Quotation validity period | expireTime | Long | M | unix timestamp, the effective time of this inquiry. If the effective time has passed, the inquiry will be void |
| Merchant order number | merOrderNo | String(32) | M | Merchant's incoming order number |
| Lock type | lockType | String(2) | O | Lock type T0, T1 |

### 5.1.3 FX Trading

| Transaction Code | TP1003 |
|----|----|
| Function name | FX trading |
| Function description | According to the quoted price after inquiry, initiate FX transaction |
| Calling method | Real-time interface |
| Calling process | After initiating the quote query interface, according to the obtained quoteId, initiate the corresponding FX transaction |
| Application scenarios | - |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp1003`

**Method:** `POST`

> Request example:

```json
{
    "quoteId": 7843892398239,
    "callbackUrl":"https://xxxx.xxxx.xxxx/xxxx/xxxx"
}

```


**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
| ------- | ----------- | ----------- | ---- | ----------- |
| Quote ID | quoteId | Long | M | Quote ID |
| Callback url | callbackUrl | String(256) | M | Callback notification Url |





> Return example:

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

**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Sell Currency | sellCurrency | String(3) | M | Sell Currency |
| Buy currency | buyCurrency | String(3) | M | Buy currency |
| Exchange rate | rate | String(18) | M | Exchange rate quote |
| Sell Amount | sellAmount | String(18) | M | Sell Amount |
| Buy Amount | buyAmount | String(20) | M | Buy Amount |
| Quote ID | quoteId | Long | M | Quote ID |
| Result code | code | String | M | Fx transaction result code |
| Result description | message | String | M | Transaction result description |
| Transaction serial number | bizFlow | String(32) | M | The unique serial number corresponding to Fx transaction |
| Lock type | lockType | String(2) | O | Lock type T0, T1 |

### 5.1.4 International remittance interface

**1 Function description**


| Transaction Code | TP1004 |
|----|----|
| Function name | International remittance interface |
| Function description | Initiate international remittance and initiate remittance to overseas beneficiaries. |
| Calling method | Real-time interface |
| Call Process | Call [5.3.9 Query International Payment Fields](#_5-3-9-Query International Payment Fields) After obtaining the required fields of the payee, initiate a remittance to the payee according to the corresponding fields. |
| Application scenarios | Initiate international remittance, initiate remittance to overseas beneficiaries |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp1004`

**Method:** `POST`

> Request example:

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

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Merchant order number | merOrderNo | string | M | Merchant custom order number, must be unique |
| Receiving country | countryCode | string | M | iso 3166-1 standard 2-character code |
| Receiving currency | arriveCurrency | string | M | Receiving currency, 3-digit standard currency code |
| Debit currency | debitCurrency | string | M | Debit currency, 3-digit standard currency code |
| Payment method | payType | string | M | Optional values: local or swift |
| Receiving account type | accountType | string | M | Only 1 (bank account) is currently supported |
| Debit Amount | debitAmount | string | C | Debit Amount, that is, the amount corresponding to the debit currency |
| Receipt amount | arriveAmount | string | C | Receipt amount (choose 1 between the deducted amount and the received amount, and fill in 1 at the same time, if you fill in at the same time, the received amount shall prevail) |
| Purpose of Remittance | purpose | string | M | See [6.1.4 Purpose of Remittance List](#_6-1-4-purpose-payment purpose) |
| Payer field | payer | object | M | Fill in according to the data returned by the corresponding country tp3005 |
| Payee field | payee | Object | M | Fill in according to the data returned by tp3005 of the corresponding country |
| Associate fx serial number | fxBizFlow | String | O | Associate fx serial number, if you fill in this field, this interface will not check the balance,<br>but the deducted amount cannot be greater than the amount of the corresponding fx order |
| Remittance postscript | tradeComments | String | O | Remittance postscript |
| Remarks for the purpose of the remittance | purposeRemark | String | O | When the purpose is 99, the purpose of the remittance shall prevail |





**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Debit Currency | debitCurrency | String | M | Debit Currency |
| Receiving currency | arriveCurrency | String | M | Receiving currency |
| Exchange rate | rate | String | M | Exchange rate |
| Debit Amount | debitAmount | String | M | Debit Amount |
| Received Amount | arriveAmount | String | M | Received Amount |
| Quote ID | quoteId | long | M | Quote ID |
| Quotation validity | expireTime | long | M | unix timestamp, the effective time of this inquiry. |
| Merchant order number | merOrderNo | String | M | Merchant order number |
| Associated fx serial number | fxBizFlow | String | O | Associated fx serial number |

### 5.1.5 International remittance transaction confirmation

**1 Function description**


| Transaction Code | TP1005 |
|----|----|
| Function name | International remittance transaction confirmation |
| Function description | Confirm the international remittance transaction and submit it formally. |
| Calling method | Real-time interface |
| Calling Process | Call [5.1.4 International Remittance Interface] (#_5-1-4-International Remittance Interface) to submit the transaction, then call this interface to confirm the transaction. |
| Application Scenarios | Initiate an international remittance, after initiating a remittance to an overseas beneficiary, confirm the international remittance transaction and submit it formally. |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp1005`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Quote ID | quoteId | Long | M | Quote ID |
| Callback url | callbackUrl | String | M | Callback notification Url |


**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Quote ID | quoteId | long | M | Quote ID |
| Receiving country | countryCode | string | M | iso 3166-1 standard 2-character code |
| Receiving currency | arriveCurrency | string | M | Receiving currency, 3-digit standard currency code |
| Debit currency | debitCurrency | string | M | Debit currency, 3-digit standard currency code |
| Payment method | payType | string | M | Optional values: local or swift |
| Receiving account type | accountType | string | M | Only 1 (bank account) is currently supported |
| Payment amount | arriveAmount | string | M | Payment amount |
| Debit Amount | debitAmount | String | M | Debit Amount |
| Exchange rate | rate | String | M | Exchange rate |
| Status | status | String | M | Order status |
| Result Code | code | String | M | Transaction Result Code |
| Result description | message | String | M | Transaction result description |
| Transaction serial number | bizFlow | String | M | The unique serial number corresponding to international remittance transactions |
| Merchant order number | merOrderNo | String | M | Merchant order number |
| Associated fx serial number | fxBizFlow | String | O | Associated fx serial number |

### 5.1.6 Withdrawal interface

**1 Function description**


| Transaction Code | TP1008 |
|----|----|
| Function name | Application for withdrawal transaction |
| Function description | Used to initiate overseas withdrawals, the account name of the withdrawal needs to be the same as the registered name of the merchant |
| Calling method | Real-time interface |
| Calling process | - |
| Application Scenarios | Used to initiate overseas withdrawals, the withdrawal account name needs to be the same as the merchant's registered name |
<aside class="success">
The default withdrawal account name is the registered name provided by the merchant when entering the network
</aside>

**2 Request address**


**Url:** `https://{baseUrl}/api/tp1008`

**Method:** `POST`

> Request example:

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
    "remark": "xxx company trade cash withdrawal",
    "callbackUrl":"https://xxxx.xxxxxx.xx/xx"
}
```

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Merchant order number | merOrderNo | string(32) | M | Merchant passes in the unique order number of this transaction |
| Currency | currency | string(3) | M | Withdrawal currency, 3-digit standard currency code |
| Amount | amount | decimal(18,2) | M | Withdrawal amount |
| Bank account number/IBAN | bankAccountNo | string(64) | M | Withdraw bank account number or IBAN |
| Bank Name | bankName | string(64) | M | Withdrawal Bank Name |
| Bank Address | bankAddress | string(256) | M | Withdrawal Bank Address |
| swift code | swiftCode | string(32) | M | swift code of the withdrawal bank |
| Proxy Bank Name | proxyBankName | string(64) | O | Proxy Bank Name |
| Proxy Bank Address | proxyBankAddress | string(256) | O | Proxy Bank Address |
| Proxy swift code | proxySwiftCode | string(32) | O | Proxy swift code |
| Remittance postscript | remark | string(64) | O | Remittance postscript |
| Callback url | callbackUrl | string(256) | M | Callback notification Url |




> Return example:

```json
{
    "merOrderNo":"8793478374",
    "bizFlow":"2184394993483534",
    "status": "PROCESS",
    "code": "",
    "message": ""
}
```
**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Merchant order number | merOrderNo | string(32) | M | Merchant passes in the unique order number of this transaction |
| Business serial number | bizFlow | string(32) | M | Unique serial number generated by OTT |
| Status | status | string(8) | M | Transaction result status |
| Result code | code | string(8) | M | Transaction result code |
| Result description | message | string(64) | M | Transaction result description |

### 5.1.7 Merchant access

**1 Function description**


| Transaction Code | TP1006 |
|----|----|
| Function name | Merchant application for network access |
| Function description | Collect merchant information and complete merchant access |
| Calling method | Real-time interface |
| Calling process | - |
| Application Scenarios | The purpose of this guide is to collect merchant profile information for OTTPAY HK. After the qualification review of the OTTPAY HK party, the qualification approval of the merchant will be approved, and follow-up services can be provided to the merchant. |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp1006`

**Method:** `POST`

> Request example:

```json
{
        "authorizationPaths": [
            "uploadFile/IMG_9289.PNG"
        ],
        "averageTransactionAmount": "3841000",
        "businessBackground": "Trading Background",
        "callbackUrl": "https://tttt.callback.xxx.com/api/callback",
        "companyWebsite": "https://www.company.baidu.com",
        "contactPhoneNumber": "+861453453453",
        "country": "HK",
        "directorPaths": [
            "uploadFile/IMG_9289.PNG"
        ],
        "employeeNumber": "1000",
        "goodstandPaths": [
            "uploadFile/IMG_9289.PNG"
        ],
        "incorporationPaths": [
            "uploadFile/IMG_9289.PNG"
        ],
        "mailingAddress": "Mailing Address",
        "maxTransactionAmount": "882200",
        "merNameEn": "Test API Mer Kyc Company1",
        "merchantApplicationPath": [
            "uploadFile/IMG_9289.PNG"
        ],
        "mermorandumPaths": [
            "uploadFile/IMG_9289.PNG"
        ],
        "officePaths": [
            "uploadFile/IMG_9289.PNG"
        ],
        "ownershipPaths": [
            "uploadFile/IMG_9289.PNG"
        ],
        "ownershipType": "A",
        "paymentPurpose": [
            "Medical fees",
            "Hotel fee"
        ],
        "permonthTransactionAmount": "55000",
        "permonthTransactionNumber": 8345234,
        "personAddressPaths": [
            "uploadFile/IMG_9289.PNG"
        ],
        "personIdentiPaths": [
            "uploadFile/IMG_9289.PNG"
        ],
        "projectPersonMail": "453523@163.com",
        "projectPersonName": "Zhang San",
        "projectPersonPosition": "CEO",
        "registerCapital": "10 million yuan",
        "registrationAddress": "Registration Address",
        "saleOne": "1000000",
        "saleThree": "100",
        "saleTwo": "10000",
        "serviceProvided": [
            "import and export",
            "Local Courier Service"
        ],
        "shareholderPaths": [
            "uploadFile/IMG_9289.PNG"
        ],
        "shopWebsite": "https://www.baidu.com",
        "sourceFunds": [
            "Labor Income",
            "Investment income"
        ],
        "suppliers": [
            {
                "supplierCountry": "HK",
                "supplierName": "xxx service company"
            },
            {
                "supplierCountry": "AU",
                "supplierName": "EGTH Limited"
            }
        ],
        "tradeClients": [
            {
                "tradeClientCountry": "HK",
                "tradeClientName": "TUIREO Limited"
            }
        ],
        "projectPersonPhone": "+861238345345"
    }
```

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Country | country | string(2) | M | iso 2-digit country code |
| Company English name | merNameEn | string(255) | M | Company English name |
| Company name in Chinese | merName | string(255) | O | Company name in Chinese |
| Ownership Type | ownershipType | string(1) | O | O
| Business Nature | businessBackground | string(255) | O | Business Nature |
| Sales URL | shopWebsite | string(255) | O | Sales URL |
| Company official website | companyWebsite | string(255) | O | company official website |
| Company Registered Address | registrationAddress | string(255) | M | Company Registered Address |
| Company mailing address | mailingAddress | string(255) | O | Company mailing address |
| Number of employees | employeeNumber | string(255) | O | Number of employees |
| Registered Capital | registerCapital | string(255) | O | Registered Capital |
| Business phone | contactPhoneNumber | string(255) | O | Business phone |
| Name of authorized administrator | projectPersonName | string(255) | O | Name of authorized administrator |
| Authorized Administrator Position | projectPersonPosition | string(255) | O | Authorized Administrator Position |
| Authorized administrator phone | projectPersonPhone | string(255) | O | Authorized administrator phone |
| Authorized Administrator Email | projectPersonMail | string(255) | M | Authorized Administrator Email |
| Products and services provided | serviceProvided | string(255) | O | Products and services provided |
| The nature of the money collected by the customer | sourceFunds | list(10) | O | Describe the nature of the money collected by your customer (source of money) |
| Nature of the money sent to the customer | paymentPurpose | list(10) | O | Describe the nature of the money you send to the customer (where the money goes) |
| The country of the branch | residesCountry | list(10) | O | The country of the branch |
| Main suppliers and their countries and regions | suppliers | list(5) | O | Main suppliers and their countries and regions |
| Main supplier name | supplierName | string(35) | O | Main supplier name (under suppliers) |
| Main supplier country | supplierCountry | string(2) | O | Main supplier country (under suppliers) |
| Main customer names and country | tradeClients | list(5) | O | Main customer names and country |
| Main client name | tradeClientName | string(35) | O | Main client name (under trades) |
| The country where the main customer name is located | tradeClientCountry | string(2) | O | The country where the main customer name is located (under trades) |
| Sales 1 year ago | saleOne | decimal(18,2) | O | Sales 1 year ago (unit: USD) |
| Sales 2 years ago | saleTwo | decimal(18,2) | O | Sales 2 years ago (unit: USD) |
| Sales 3 years ago | saleThree | decimal(18,2) | O | Sales 3 years ago (unit: USD) |
| Estimated number of transactions (per month) | permonthTransactionNumber | int | O | Estimated number of transactions (per month) |
| Estimated total transaction volume (monthly) | permonthTransactionAmount | decimal(18,2) | O | Estimated total transaction volume (monthly) (unit USD) |
| Estimated average transaction volume | averageTransactionAmount | decimal(18,2) | O | Estimated average transaction volume (unit USD) |
| Estimated single largest transaction amount | maxTransactionAmount | decimal(18,2) | O | Estimated single largest transaction amount (unit USD) |
| Merchant Service Cooperation Application Form | merchantApplicationPath | list(5) | O | Merchant Service Cooperation Application Form |
| Certificate of company registration | incorporationPaths | list(5) | M | Certificate of company registration |
| Articles of Association | mermorandumPaths | list(5) | O | Articles of Association |
| Proof of Good Survival | goodstandPaths | list(5) | O | Proof of Good Survival |
| Directors Roster | directorPaths | list(5) | O | Directors Roster |
| Register of shareholders | shareholderPaths | list(5) | O | Register of shareholders |
| Important Person ID Document | personIdentiPaths | list(5) | O | Important Person ID Document |
| Important Person Address Proof Document | personAddressPaths | list(5) | O | Important Person Address Proof Document |
| Board Resolution/Authorization Letter | authorizationPaths | list(5) | O | Board Resolution/Authorization Letter |
| Company ownership structure diagram | ownershipPaths | list(5) | O | Company ownership structure diagram |
| Office site photos | officePaths | list(5) | O | Office site photos |
| Callback URL | callbackUrl | string(255) | M | Callback URL, this URL will be called back after OTTPAY HK background review |




> Return example:

```json
{
        "bizFlow":"210622162803810002",
        "status": "ACCEPT",
        "code":"S00001",
        "message":"ACCEPT"
}
```

**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Business serial number | bizFlow | string(32) | M | Unique order number for network access |
| Status | status | string(6) | M | Application status code ACCEPT: Accepted successfully, waiting for callback |
| Result code | code | string(6) | M | Response result code, S00001 means that it has been successfully received,<br/>callback after OTTPAY HK review |
| Result description | message | string(255) | M | Response description |


### 5.1.9 Transfer between merchants

**1 Function description**


| Transaction Code | TP1010 |
|----|----|
| Function name | Transfer between merchants |
| Function description | Both are merchants registered with OTT, and transfer funds to the other OTT account |
| Calling method | Real-time interface |
| Calling process | - |
| Application Scenarios | Both merchants registered at OTT, transfer funds to the other OTT account |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp1010`

**Method:** `POST`

> Request example:

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

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Merchant order number | merOrderNo | string(32) | M | Merchant customized unique order number |
| Recipient account number | toAcctNo | string(32) | M | Recipient account number |
| Recipient's account name | toAcctName | string(255) | M | Recipient's account name |
| Transfer currency | currency | string(3) | M | Transfer currency |
| Transfer amount | amount | Decimal(18,2) | M | Transfer amount |
| Purpose of remittance | purpose | string(3) | M | Purpose of remittance, see appendix 6.1.4 Purpose of payment |
| Postscript | remark | string(255) | O | Postscript |




> Return example:

```json
{
        "bizFlow": "70210415775519090003",
        "status": "SUCC",
        "feeCurrency": "USD",
        "feeAmount": "2.50"
}
```

**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Business serial number | bizFlow | string(32) | M | Unique business order number on the OTT side |
| Result status | status | string(6) | M | Result status SUCC: Success FAIL: Failure |
| Fee currency | feeCurrency | string(3) | O | fee currency, if the fee mode is real-time collection, this field will be returned |
| Handling fee amount | feeAmount | string(22) | O | Handling fee amount, if the fee mode is real-time collection, this field will be returned |


### 5.1.10 VA account opening application

**1 Function description**


| Transaction Code | TP1011 |
|----|----|
| Function name | VA account opening application |
| Function description | Merchants initiate a VA account opening application, and after waiting for OTT review, the merchant can query specific VA account information through the VA query interface |
| Calling method | Asynchronous interface |
| Calling process | - |
| Application scenarios | Merchant initiates VA account opening application |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp1011`

**Method:** `POST`

> Request example:

```json
{
        "merOrderNo":"150",
        "bankType":"00"
}
```


**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Merchant order number | merOrderNo | string(32) | M | Merchant customized unique order number |
| Account Bank | bankType | string(2) | M | Account Bank Selection |





> Return example:

```json
{
        "bizFlow": "70210415775519090003",
        "status": "ACCEPT"
}
```

**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Business serial number | bizFlow | string(32) | M | Unique business order number on the OTT side |
| Result status | status | string(6) | M | Result status ACCEPT: received successfully FAIL: failed |


### 5.1.11 Collection flow and trade order association

**1 Function description**


| Transaction Code | TP1013 |
|----|----|
| Function name | Collection flow and trade order association |
| Function description | Collection flow and trade order association |
| Calling method | Real-time interface |
| Calling process | - |
| Application Scenarios | After the merchant's trade collection order is approved, associate the collection flow with the trade order |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp1013`

**Method:** `POST`

> Request example:

```json
{
        "contactNo":"62291060316483300005",
        "flowNo":"63291062211570000002",
        "callbackUrl":"https://xxxxx.xxxx.com/callback/inAcctNoticeUrl"
}
```


**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Trade order code | contactNo | string(32) | M | Trade order code, tp2008 returns |
| Collection flow code | flowNo | string(32) | M | Collection flow code, tp3015 returns |
| Payment notification address | callbackUrl | string(255) | M | Notification address after successful payment of trade receipts |




> Return example:

```json
{
        "bizFlow":"652362763878"
}
```

**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Business serial number | bizFlow | string(32) | M | Unique business order number on the OTT side |


### 5.1.12 Callback address setting

**1 Function description**


| Transaction Code | TP1014 |
|----|----|
| Function name | For the notification interface, set the callback address |
| Function description | For the notification interface, set the callback address |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenario | For the callback interface without transaction parameters, set the callback address separately |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp1014`

**Method:** `POST`

> Request example:

```json
{
        "tradeCode":"TP2007",
        "callbackUrl":"https://xxxxx.xxxx.com/callback"
}
```


**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Callback address | callbackUrl | string(64) | M | Callback address |
| Interface type | tradeCode | string(6) | M | Callback interface type |




> Return example:

```json
{
        "code":"SUCC"
}
```

**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Result code | code | string(6) | M | SUCC stands for success |

### 5.1.13 Trade order application

**1 Function description**

| Transaction Code | TP1012 |
| -------- | ----------------------- |
| Function name | Merchant creates trade order contract |
| Function description | Collect order information |
| Calling method | Real-time interface |
| Calling process | Merchant sends an application, ottpay returns the contract order number |
| Application scenario | Merchant collects order information and compliance materials, and the provider creates a new trade order and provides the contract number

**2 Request address**

**Url:** `https://{baseUrl}/api/tp1012`

**Method:** `POST`

> Request example:

```json
 {
    "callbackUrl":"http://www.baidu.com",
    "merOrderNo":"23134141421414",
    "currency":"CNY",
    "amount":"7010.20",
    "tradeType": "00",
    "buyerName": "TX",
    "buyerArea":"China",
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
    "logCompany":"International Trade Logistics Company",
    "annexUrl":["/src/iiii/a.png","/src/iiii/b.pdf","/src/iiii/c.png"]
}
```

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Callback interface address | callbackUrl | string(60) | M | Used to notify order status |
| Merchant unique order number | merOrderNo | string(32) | M | Merchant unique order number |
| Order currency | currency | string(3) | M | Order currency |
| Total order amount | amount | Decimal(18,2) | M | Total order amount |
| Trade Type | tradeType | string(2) | M | Trade Type Default: 00-Goods Trade |
| Buyer Name | buyerName | string(64) | M | Buyer Name |
| Purchaser's area | buyerArea | string(64) | M | Purchaser's area |
| Item information | goodsList | `List<goodsList>` | M | Item information The number of items does not exceed 10 |
| Transaction Date | transcationDate | string(10) | M | Transaction Date Format: yyyy-MM-dd |
| Transaction Voucher | transcationCert | `Array` | M | An array of multiple voucher file addresses (the file size does not exceed 20M) |
| Logistics Status | logStatus | string(1) | M | 0-Unshipped 1-Delivered If it is shipped logNo, logCompany, annexUrl, three fields are required |
| Logistics order number | logNo | string(64) | O | Logistics order number |
| Logistics company name | logCompany | string(128) | O | Logistics company name |
| Attachment | annexUrl | `Array` | O | Array of multiple attachment file addresses (the file size does not exceed 20M) | 

**goodsList**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Transaction Item Name | orderName| string(64) | M | Transaction Item Name |
| Number of transaction items | orderNum | string(10) | M | Number of transaction items |


**4 Response field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Trade order number | contractNo| string(32) | M | Trade order number (unique) |


**Response example:**

```json
{
     "contractNo": "2012042197287616"
}
```

## 5.2 Callback interface
### 5.2.1 The system informs the merchant of the payment result

**1 Function description**

| Transaction Code | TP2001 |
|----|----|
| Function name | Payment callback |
| Function description | Ottpayhk notifies merchants of payment results |
| Calling method | Real-time interface |
| Calling process | The merchant first calls [5.1.1 RMB payment](#_5-1-1-RMB payment) to initiate a RMB payment request to Ottpayhk, and Ottpayhk will perform the transaction. <br>After processing, notify the merchant. If the merchant does not call back in time within the specified time, the merchant should initiate an active inquiry |
| Application scenarios | Merchants need to know the final result of RMB payment |
<aside class="success">
This notification will continue to notify for 24 hours in a way that the interval is getting longer.<br>Merchants should return by http 200. If the notification duration expires and the notification does not return normally, no further notification will be made. <br>Merchants should use the [5.3.1 RMB payment service inquiry] (#_5-3-1-RMB payment service inquiry) inquiry interface to inquire about the transaction results.
</aside>
**2 Request address**


**Url:** **callbackUrl** in [5.1.1](#_5-1-1-RMB payment)

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Order number | merOrderNo | String(32) | M | Return as is |
| Business serial number | bizFlowNo | String(32) | M | The unique business serial number generated by Ottpayhk, which corresponds to the order number one-to-one |
| Success count | successCount | Int | M | Return success count |
| Number of failed entries | faultCount | Int | M | Return number of failed entries |
Read more | Payment details | payeeList | `List<payee>` | M | Payment details list is not paged |

**payee field:**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Single detail external merchant number | merSingleNo | String | M | The merchant's incoming voucher number for managing the merchant system |
| System order number | applyNo | String | | Order number generated by M Ottpayhk |
| Amount | Amount | Number(18,2) | M | Payment Amount |
| Status | Status | Int | M | "0":"Accepted","1", "Success","2","Failed","3","Processing" |
| Description | respDesc ​​| String | M | Transaction specific description |
| Status code | respCode | String | M | Transaction specific status code |



### 5.2.2 FX trading result notification

**1 Function description**


| Transaction Code | TP2002 |
|----|----|
| Function name | FX trading result notification |
| Function description | Asynchronous notification of Fx transaction results |
| Calling method | Notification interface |
| Calling process | - |
| Application scenarios | [5.1.3 Fx transaction] (#_5-1-3-fx transaction) after the successful initiation and transaction processing is completed, it will be based on [5.1.3 Fx transaction](#_5-1-3-fx transaction) The callback Url in the parameter performs a callback to notify the final result. |

<aside class="success">
This notification will continue to notify for 24 hours in a way that the interval is getting longer.<br>Merchants should return by http 200. If the notification duration expires and the notification does not return normally, no further notification will be made. <br>Merchants should use the [5.3.3 Currency Exchange History Transaction Inquiry] (#_5-3-3-Foreign Exchange History Transaction Inquiry) query interface to query the transaction results by themselves.
</aside>
**2 Request address**


**Url:** **callbackUrl** in [5.1.3 Fx transaction](#_5-1-3-fx transaction)

**Method:** `POST`

> Request example:

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

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Sell Currency | sellCurrency | String(3) | M | Sell Currency |
| Buy currency | buyCurrency | String(3) | M | Buy currency |
| Exchange rate | rate | String(18) | M | Exchange rate quote |
| Sell Amount | sellAmount | String(20) | M | Sell Amount |
| Buy Amount | buyAmount | String(20) | M | Buy Amount |
| Quote ID | quoteId | Long | M Quote ID |
| Result code | code | String | M | Fx transaction result code |
| Result description | message | String | M | Transaction result description |
| Business serial number | bizFlow | String(32) | M | Business serial number |



### 5.2.3 Notification of International Remittance Transaction Results

**1 Function description**

| Transaction Code | TP2003 |
|----|----|
| Function name | Notification of international remittance transaction results |
| Function description | Asynchronous notification of international remittance transaction results |
| Calling method | Notification interface |
| Calling process | - |
| Application scenarios | [5.1.5 International remittance transaction](#_5-1-5-International remittance transaction confirmation) After the initiation is successful and the transaction is processed, it will be based on [5.1.5 International remittance transaction](#_5-1-5 -International remittance transaction confirmation) The callback Url in the parameter is called back to notify the final result. |

<aside class="success">
This notification will continue to notify for 24 hours in a way that the interval is getting longer.<br>Merchants should return by http 200. If the notification duration expires and the notification does not return normally, no further notification will be made. <br>Merchants should use the [5.3.3 Currency Exchange History Transaction Inquiry] (#_5-3-3-Foreign Exchange History Transaction Inquiry) query interface to query the transaction results by themselves.
</aside>
**2 Request address**


**Url:** [5.1.5 International Remittance Transaction Confirmation] (#_5-1-5-International Remittance Transaction Confirmation) **callbackUrl**

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Quote ID | quoteId | long | M | Quote ID |
| Receiving country | countryCode | string | M | iso 3166-1 standard 2-character code |
| Receiving currency | arriveCurrency | string | M | Receiving currency, 3-digit standard currency code |
| Debit currency | debitCurrency | string | M | Debit currency, 3-digit standard currency code |
| Payment method | payType | string | M | Optional values: local or swift |
| Receiving account type | accountType | string | M | Only 1 (bank account) is currently supported |
| Payment amount | arriveAmount | string | M | Payment amount |
| Debit Amount | debitAmount | String | M | Debit Amount |
| Exchange rate | rate | String | M | Exchange rate |
| Payment status | status | string | M | Order status |
| Result Code | code | String | M | Transaction Result Code |
| Result description | message | String | M | Transaction result description |
| Transaction serial number | bizFlow | String | M | The unique serial number corresponding to international remittance transactions |
| Merchant order number | merOrderNo | String | M | Merchant order number |
| Associated fx serial number | fxBizFlow | String | O | Associated fx serial number |


### 5.2.4 Notification of Merchants' Network Access Results

**1 Function description**


| Transaction Code | TP2004 |
|----|----|
| Function name | Notification of merchant's network access results |
| Function Description | Asynchronous Notification of Merchant Access Results |
| Calling method | Notification interface |
| Calling process | - |
| Application Scenarios | [Merchant access information improvement](#_5-1-8-Merchant access information improvement) After successful initiation and transaction processing, it will be based on [Merchant access information improvement](#_5-1-8-Merchant access information Perfect) The callback Url in the parameter is used to call back and notify the final result. |

<aside class="success">
This notification will continue to notify for 24 hours in a way that the interval is getting longer.<br>Merchants should return by http 200. If the notification duration expires and the notification does not return normally, no further notification will be made.
</aside>
**2 Request address**


**Url:** **callbackUrl** in [Complete Merchant Access Information](#_5-1-8-Complete Merchant Access Information)

**Method:** `POST`

> Request example:

```json
{
        "bizFlow":"87200408378515100071",
        "code":"S00000",
        "message":"SUCCESS",
        "merchantNo":"005703100153",
        "merNameEn":"Demo Company Limited"
}
```

**3 Request field**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Business serial number | bizFlow | string(32) | M | Unique order number for network access |
| Result code | code | string(6) | M | Response result code, S00000 represents successful network access |
| Result description | message | string(255) | M | Response description |
| Merchant ID | merchantNo | string(32) | M | Merchant ID, which is the unique identification number of the merchant |
| Merchant English Name | merNameEn | string(255) | M | Merchant English Name |
| Authorization Code | authorizeCode | string(32) | M | Authorization Code |



### 5.2.5 Notification of withdrawal results

**1 Function description**


| Transaction Code | TP2005 |
|----|----|
| Function name | Withdrawal result notification |
| Function description | Asynchronous notification of withdrawal results |
| Calling method | Notification interface |
| Calling process | - |
| Application scenario | [Withdraw transaction](#_5-1-6-Withdraw interface) After the successful initiation and transaction processing is completed, it will proceed according to the callback Url in the parameters of [Withdraw transaction](#_5-1-6-Withdraw interface) The callback informs the final result. |
<aside class="success">
This notification will continue to notify for 24 hours in a way that the interval is getting longer.<br>Merchants should return by http 200. If the notification duration expires and the notification does not return normally, no further notification will be made.
</aside>
**2 Request address**


**Url:** **callbackUrl** in [Withdraw Transaction](#_5-1-6-Withdraw interface)

**Method:** `POST`

> Request example:

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
    "remark": "xxx company trade cash withdrawal",
    "bizFlow":"3213347378487348734",
    "status":"SUCCESS",
    "code":"S00000",
    "message":"Success"
}
```

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Merchant order number | merOrderNo | string(32) | M | Merchant passes in the unique order number of this transaction |
| Currency | currency | string(3) | M | Withdrawal currency, 3-digit standard currency code |
| Amount | amount | decimal(18,2) | M | Withdrawal amount |
| Withdrawal account name | bankAccountName | string(64) | M | Withdrawal account name |
| Bank account number/IBAN | bankAccountNo | string(64) | M | Withdraw bank account number or IBAN |
| Bank Name | bankName | string(64) | M | Withdrawal Bank Name |
| Bank Address | bankAddress | string(256) | M | Withdrawal Bank Address |
| swift code | swiftCode | string(32) | M | swift code of the withdrawal bank |
| Proxy Bank Name | proxyBankName | string(64) | O | Proxy Bank Name |
| Proxy Bank Address | proxyBankAddress | string(256) | O | Proxy Bank Address |
| Proxy swift code | proxySwiftCode | string(32) | O | Proxy swift code |
| Remittance postscript | remark | string(64) | O | Remittance postscript |
| Business serial number | bizFlow | string(32) | M | Unique serial number generated by OTT |
| Transaction result status | status | string(8) | M | Transaction result status |
| Transaction Result Code | code | string(8) | M | Transaction Result Code |
| Result description | message | string(64) | M | Transaction result description |



### 5.2.6 Notification of International Remittance Payment Voucher

**1 Function description**

| Transaction Code | TP2006 |
|----|----|
| Function name | Notification of international remittance payment voucher |
| Function description | International remittance payment voucher notice |
| Calling method | Notification interface |
| Calling process | - |
| Application scenario | After [5.1.5 International Remittance Transaction] (#_5-1-5-International Remittance Transaction Confirmation) is completed, and OTTPAYHK obtains the bank payment voucher, it will return the payment voucher in the form of Base64 through this interface Pass it to the merchant. |
<aside class="success">
This notification will continue to notify for 24 hours in a way that the interval is getting longer.<br>Merchants should return by http 200. If the notification duration expires and the notification does not return normally, no further notification will be made.
</aside>
**2 Request address**


**Url:** **callbackUrl** in [5.1.5 International Remittance Transaction] (#_5-1-5-International Remittance Transaction Confirmation)

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Transaction serial number | bizFlow | string | M | The unique serial number of international remittance, consistent with the bizFlow returned in tp1005 |
| File | fileBase | string | M | Byte stream after Base64 encoding |

### 5.2.7 Notification of Trade Receipt Arrival

**1 Function description**

| Transaction Code | TP2007 |
|----|----|
| Function name | Trade receipt arrival notification |
| Function Description | Trade Receipt Arrival Notification |
| Calling method | Notification interface |
| Calling process | - |
| Application Scenarios | After the merchant's VA sub-account is received, OTTPAYHK will send a notification to the merchant that the trade receipt funds have arrived |
<aside class="success">
This notification will continue to notify for 24 hours in a way that the interval is getting longer.<br>Merchants should return by http 200. If the notification duration expires and the notification does not return normally, no further notification will be made.
</aside>
**2 Request address**


**Url:** **callbackUrl** in [5.1.12 Callback Address Setting](#_5-1-12-Callback Address Setting)

**Method:** `POST`


> Request example:

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

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| The serial number of the account | flowNo | string(32) | M | The unique serial number of the trade receipt to the account |
| Received Amount | receiveAmount | decimal(18,2) | M | VA Received Amount |
| Payment currency | receiveCurrency | string(3) | M | VA Payment currency |
| Entry VA account number | vaAccount | string(16) | M | Entry VA account number |
| Payer name | senderName | string(64) | O | Payer name |
| Payer Account | senderAccount | string(32) | O | Payer Account |
| Payment time | receiveTime | string(10) | M | Payment time, 10-digit unix timestamp |


### 5.2.8 Notification of Trade Order Application Results

**1 Function description**

| Transaction Code | TP2008 |
|----|----|
| Function name | Return status notification of trade order result |
| Function description | Notify the merchant of the result of the order application after the operation review |
| Calling method | Notification interface |
| Calling process | - |
| Application Scenarios | [5.1.13 Trade Order Application] is successfully initiated, and the final result will be notified according to the callback Url. |

<aside class="success">
This notification will continue to notify for 24 hours in a way that the interval is getting longer.<br>Merchants should return by http 200. If the notification duration expires and the notification does not return normally, no further notification will be made. <br>Merchants should check the transaction results through the [5.3.18] query interface by themselves.
</aside>
**2 Request address**


**Url: **callbackUrl** in [5.1.13 Trade Order Application]

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Trade order number | contactNo | string(32)| M | Trade order number (unique) |
| Merchant order number | merOrderNo | string(32)| M | Merchant order number (unique) |
| Status | status | string(8) | M |'ACCEPT-Processing SUCC-success FAIL-failure' |
| Result description | message | string(64)| M | Transaction result description |

**Request example**
 ```json
{
    "contactNo": "20123910029181818",
    "merOrderNo": "1401203219391312",
    "status": "SUCC",
    "message": "Success"
}
```

### 5.2.9 Notification of the association result between the collection flow and the trade order

**1 Function description**

| Transaction Code | TP2009 |
|----|----|
| Function name | Notification of the association result of collection flow and trade order |
| Function description | Notice to the merchant after the collection flow is associated with the trade order |
| Calling method | Notification interface |
| Calling process | - |
| Application Scenarios | [5.1.11 Collection Flow and Trade Order Association] is initiated successfully and the transaction is processed, the callback Url in the [5.1.11 Collection Flow and Trade Order Association] parameter will be called back to notify the final result. |

<aside class="success">
This notification will continue to notify for 24 hours in a way that the interval is getting longer.<br>Merchants should return by http 200. If the notification duration expires and the notification does not return normally, no further notification will be made. <br>Merchants should use the [5.3.17 Collection Flow and Trade Order Association Inquiry Interface] to inquire about the transaction results by themselves.
</aside>
**2 Request address**


**Url:** **callbackUrl** in [5.1.11 Collection Flow and Trade Order Association]

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Trade order code | contactNo | string(32) | M | Trade order code |
| Collection flow code | flowNo | string(32) | M | Collection flow code |
| Account currency | currency | string | M | Account currency, 3-digit standard currency code |
| Payment amount | amount | decimal(18,2) | M | Payment amount |
| Fee Currency | feeCurty | String | M | Fee currency, 3-digit standard currency code |
| Handling fee amount | feeAmt | decimal(18,2) | M | OTT PAY charges handling fee |
| Entry time | approveTime | bigInt(13) | M | Entry timestamp (milliseconds) |
| Status | status | string(2) | M | '02-Pass 03-Reject' |
| Result description | message | string(64) | M | Transaction result description |

### 5.2.10 Refund notice

**1 Function description**

| Transaction Code | TP2010 |
|----|----|
| Function name | Refund notification |
| Function description | Return the amount to the merchant account after the failure of international remittance or RMB entry |
| Calling method | Notification interface |
| Calling process | - |
| Application scenario | After the failure of international remittance or RMB entry, the amount will be returned to the merchant account and a refund notification will be sent. The url for the merchant to accept the refund notification is set through the interface: [5.1.12 Callback address setting], and the tradeCode is set to tp2010. |

<aside class="success">
This notification will continue to notify for 24 hours in a way that the interval is getting longer.<br>Merchants should return by http 200. If the notification duration expires and the notification does not return normally, no further notification will be made.
</aside>
**2 Request address**


**Url:** **callbackUrl** in [5.1.12 Callback Address Setting](#_5-1-12-Callback Address Setting)

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Business Type | bizType | string(2) | M | 01-RMB 02-International Remittance |
| System order number | applyNo | string(32) | M | Ottpayhk order number of the original payment |
| Single order number | merSingleNo | string(32) | M | Original payment merchant order number |
| Original deduction currency | tradeurty | string | M | Original payment transaction merchant deduction currency, 3-digit standard currency code |
| Original deduction amount | tradeAmt | decimal(18,2) | M | Original payment transaction merchant deduction amount |
| Original payment time | tradeTime | bigInt(13) | M | Entry timestamp (milliseconds) |
| Refund currency | refundCurty | String | M | Refund currency, 3-digit standard currency code |
| Refund amount | refundAmt | decimal(18,2) | M | Refund amount |
| Remarks | remark | string(255) | M | Remarks |

## 5.3 Query interface

### 5.3.1 RMB payment business inquiry

**1 Function description**

| Transaction Code | TP3001 |
|----|----|
| Function name | RMB payment business inquiry |
| Function description | Merchants self-check the final result of RMB payment |
| Calling method | Real-time interface |
| Calling process | After the merchant sends a RMB payment request, query the corresponding order result |
| Application scenarios | Merchants need to know the final result of RMB payment |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3001`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Order number | merOrderNo | String(32) | O | Order number when the payment was initiated |
| Business serial number | bizFlowNo | String(32) | O | Ottpayhk generates a unique business serial number, which corresponds to the order number one-to-one.<br>Note: Only one order number and business serial number need to be filled in. Serial number shall prevail |


**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Order number | merOrderNo | String(32) | M | Order number when the payment request was initiated |
| Business serial number | bizFlowNo | String(32) | M | Business serial number returned by payment request |
| Result code | respCode | String(6) | M | Payment transaction result code |
| Result description | respDesc ​​| String(50) | M | Payment transaction result detailed description |
| Payee List | payeeList | `List<payee>` | M | Payee List |
| Fee currency | feeCurrency | String(3) | O | fee currency charged |
| Fee currency | feeAmount | Decimal | O | Fee amount charged |
| Actual payment amount | actualPayAmount | Decimal | O | Actual payment amount |

**payee field**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Single order number | merSingleNo | String(32) | M | Order number corresponding to a single payment record |
| Payee's Account Name | payeeName | String(64) | M | Payee's Bank Account Name |
| Beneficiary Account Number | payeeAccountNo | String(32) | M | Beneficiary Bank Account Number |
| Recipient account type | acctType | String(1) | M | 0: private account 1: public account |
| ID number/<br>Unified Social Credit Code | identity | String(32) | M | If the payee account type is **0**, fill in **ID number**, <br> is* *1** Then fill in **Unified Social Credit Code** |
| Amount | amount | String(18) | M | Payment amount, in minutes, for example: If you pay **200.00** yuan, you should fill in **20000** |
| Interline Number | cNAPSCode | String(64) | M | Interline Number |
| Mobile Number | mobile | String(13) | M | Mobile Number |
| Account Bank Name | bankName | String(32) | M | Beneficiary Bank Name |
| Province of the opening bank | bankProvince | String(32) | M | Province of the recipient bank |
| Account Bank City Name | bankCity | String(32) | M | City Name of Beneficiary Bank |
| Branch name | bankBranchName | String(32) | M | Beneficiary bank branch name |
| Transaction Code | tradeCodeType | String(6) | M | Corresponding transaction attribute type, please refer to [Parameters in the field description](#_6-1-2-tradecodetype-transaction code) |
| Single result code | respCode | String(6) | M | The result code corresponding to a single transaction |
| Single result description | respDesc ​​| String(50) | M | Single transaction corresponding result description |
| Payment method | payMethod | String | F | **tradeCodeType** is *TRADE*, and **paymentType** is *B2B*, it cannot be empty.<br>[Parameters are detailed in the field description](#_6-1- 3-paymethod-payment method) |
| Declaration currency | declarationCurrency | String | F | **payMethod** value is *cash_on_delivery* cannot be empty |
| Prepaid Proportion | advanceProportion | Float | F | **payMethod** value is advanc<br> 0 <advanceProportion <1 Up to two decimal places |
| Settlement account period | settlementDate | String | F | **payMethod** value is advance <br>Settlement account period cannot be empty Unit day |
| Name of payer | senderName | String | M | Name of real payer |
| Payer’s company registration number | senderIncorporationNo | String | M | Payer’s company registration number |
Payment registration place | registrationRegion | String | M | Payment area swift country region |
| Payer's bank name | senderBankName | String | M | Payer's bank name |
| Funding source | sourceFounds | String | F | Optional |
| Payer's Bank Account | senderBankAccountNo | String | F | Payer's Bank Account Optional |

### 5.3.2 Query support currency pairs

**1 Function description**

| Transaction Code | TP3002 |
|----|----|
| Function name | Query currency exchange support currency pairs |
| Function description | Query currency exchange support currency pairs, FX transactions can be carried out in the currently supported currencies |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | Need to query currently supported FX currencies |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3002`

**Method:** `POST`

**3 Request field**


none


**4 Response field**


The object returned by the interface is: **`List<CurrencyPair>`**

**CurrencyPair field:**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Sell Currency | sellCurrency | String(3) | M | Sell Currency |
| Buy currency | buyCurrency | String(3) | M | Buy currency |

### 5.3.3 Exchange history transaction query

**1 Function description**

| Transaction Code | TP3003 |
|----|----|
| Function name | Currency exchange history transaction query |
| Function description | Currency exchange history transaction query |
| Calling method | Real-time interface |
| Calling process | - |
| Application Scenarios | Query past historical exchange transactions |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3003`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Query start time | startTime | Long | O | Unix 13-bit timestamp, query start time, closed interval |
| Query end time | endTime | Long | O | Unxi 13-digit timestamp, query end time, closed interval |
| Quote ID | quoteId | Long | O | Quote ID |

*Note: If startTime and endTime are not filled, quoteId is required. If quoteId is not filled, startTime and endTime are required, and the interval cannot exceed 24 hours. *



> Return example:

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
**4 Response field**


The object returned by the interface is: **`List<ExchangeHistory>`**

**ExchangeHistory field:**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Sell Currency | sellCurrency | String(3) | M | Sell Currency |
| Buy currency | buyCurrency | String(3) | M | Buy currency |
| Exchange rate | rate | String(18) | M | Exchange rate quote |
| Sell Amount | sellAmount | String(20) | M | Sell Amount |
| Buy Amount | buyAmount | String(20) | M | Buy Amount |
| Quote ID | quoteId | Int | M | Quote ID |
| Result code | code | String | M | Fx transaction result code |
| Result description | message | String | M | Transaction result description |
| Business serial number | bizFlow | String(32) | M | Corresponding unique business serial number |


### 5.3.4 Account balance inquiry

**1 Function description**

| Transaction Code | TP3004 |
|----|----|
| Function name | Account balance inquiry |
| Function description | Current account balance query |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | Current account balance query |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3004`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Currency | currency | String(3) | O | Currency, if not passed, it will query all currency accounts |



> Return example:

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

**4 Response field**


The object returned by the interface is: **`List<CurrencyBalance>`**

**CurrencyBalance field:**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Currency | currency | String(3) | M | Currency |
| Balance | balance | String(3) | M | Account balance |
| Account status | status | String(3) | M | Account status: on is enabled, off is disabled |

### 5.3.5 Query the head office

**1 Function description**

| Transaction Code | TP6001 |
|----|----|
| Function Name | Head Office Query |
| Function description | Paging query head office information interface |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | Current account balance query |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp6001`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Number of pages | pageNo | Int | O | Number of pagination pages, default 1 |
| Page display number | pageSize | Int | O | Page display number, default 10 |


> Return example:

```json
{
    "pageNo": 1,
    "pageSize": 5,
    "totalRecord": 1,
    "results": [
        {
            "bankName": "China Development Bank",
            "bankId": 1,
            "bankNameEn": "xxx bank"
        }
    ]
}

```

**4 Response field**


| Name | Json tag | Type | Attribute | Value description |
 |----|----|----|----|----|
| Current page number | pageNo | Int | M | - |
| Current page display number | pageSize | Int | M | - |
| Total Records | totalRecord | Int | M | - |
| Headquarters information collection | results | `List<QueryBankResp>` | M | - |

**QueryBankResp field:**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Bank Name | bankName | String(64) | M | - |
| BankId | bankId | int | M | - |
| Bank name in English | bankNameEn | String(64) | M | - |


### 5.3.6 Query the provinces supported by branches under the head office

**1 Function description**

| Transaction Code | TP6002 |
|----|----|
| Function name | Query province information |
| Function description | Query the province where the branch is supported under the head office |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | - |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp6002`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Head Office Id | bankId | Int | M | Required Bank Code of Head Office |



> Return example:

```json
{
    "bankCode": "101",
    "provinceList": [
        {
            "provinceCode": "513",
            "provinceName": "Sichuan Province",
            "provinceNameEn": "si chuan province"
        }
    ]
}

```

**4 Response field**


| Name | Json tag | Type | Attribute | Value description |
 |----|----|----|----|----|
| Head Office Id | bankId | Int | M | Head Office Bank Code |
| Province Information Collection | provinceList | `List<ProvinceResp>` | M | - |

**ProvinceResp field:**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Province Code | provinceCode | String(64) | M | - |
| Province name | provinceName | String(32) | M | - |
| Province name in English | provinceNameEn | String(64) | M | - |

### 5.3.7 Query the supported cities of the branches under the head office

**1 Function description**

| Transaction Code | TP6003 |
|----|----|
| Function name | Query city information |
| Function description | Query the city where the branch is located under the head office |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | - |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp6003`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Head Office Id | bankId | Int | M | Required Bank Code of Head Office |
| Province Code | provinceCode | String(64) | M | Required Province Code |


> Return example:

```json
{
    "bankCode": "101",
    "provinceCode": "513",
    "cityList": [
        {
            "cityName": "Aba Tibetan and Qiang Autonomous Prefecture",
            "cityCode": "513225000000",
            "cityNameEn": "xxxx "
        }
    ]
}

```

**4 Response field**


| Name | Json tag | Type | Attribute | Value description |
 |----|----|----|----|----|
| Head Office Id | bankId | Int | M | - |
| Province Code | provinceCode | String(64) | M | - |
| City Information Collection | cityList | `List<CityResp>` | M | - |

**CityResp field:**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| City Code | cityCode | String(64) | M | - |
| City Name | cityName | String(32) | M | - |
| City name English | cityNameEn | String(32) | M | - |

### 5.3.8 Query all branches of a city under the head office

**1 Function description**

| Transaction Code | TP6004 |
|----|----|
| Function name | Query branch information |
| Function description | Query all branches of a city under the head office |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | - |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp6004`

**Method:** `POST`

> Request example:

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

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Pages | pageNo | int | O | Default 1 |
| Page display number | pageSize | int | O | Default 10 |
| Branch query request | query | `QueryBranchBankRequest` | M | Cannot be empty |

**Fields of QueryBranchBankRequest**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Head Office Id | bankId | Int | M | Cannot be empty |
| City Code | cityCode | String(64) | M | Cannot be empty |




> Return example:

```json
{
    "pageNo": 1,
    "pageSize": 5,
    "totalRecord": 1,
    "results": [
        {
            "bankLinkNo": "102100099996",
            "bankName": "Industrial and Commercial Bank of China Limited Jiuzhaigou Branch",
            "bankNameEn": "china gongshang bank",
            "bankProvinceCode": "513",
            "bankProvinceName": "Sichuan Province",
            "bankProvinceNameEn": "si chuan province",
            "bankCityCode": "513225000000",
            "bankCityName": "Aba Tibetan and Qiang Autonomous Prefecture",
            "bankCityNameEn": "a ba "
        }
    ]
}
```

**4 Response field**


| Name | Json tag | Type | Attribute | Value description |
 |----|----|----|----|----|
| Current page number | pageNo | Int | M | - |
| Number of pages displayed | pageSize | Int | M | - |
| Total | totalRecord | In | M | - |
| Collection of branch information | results | `List<QueryBranchBankResp>` | M | - |


**QueryBranchBankResp field:**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Link Number | bankLinkNo | String(64) | M | - |
| Bank Name | bankName | String(32) | M | - |
| Bank name in English | bankNameEn | String(32) | M | - |
| Province Code | bankProvinceCode | String(32) | M | - |
| Province name | bankProvinceName | String(32) | M | - |
| Province name in English | bankProvinceNameEn | String(32) | M | - |
| City Code | bankCityCode | String(32) | M | - |
| City Name | bankCityName | String(32) | M | - |
| City name in English | bankCityNameEn | String(32) | M | - |

### 5.3.9 Query International Payment Field

**1 Function description**

| Transaction Code | TP3005 |
|----|----|
| Function name | Query international payment field |
| Function description | Query fields required for payment to different countries |
| Calling method | Real-time interface |
| Calling process | - |
| Application Scenarios | Query the fields required for payment to different countries before international payment |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3005`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Receiving country | countryCode | string | M | iso 3166-1 standard 2-character code |
| Receiving currency | arriveCurrency | string | M | Receiving currency, 3-digit standard currency code |
| Debit currency | debitCurrency | string | M | Debit currency, 3-digit standard currency code |
| Payment method | payType | string | M | Optional values: local or swift |
| Receiving account type | accountType | string | M | Only 1 (bank account) is currently supported |



> Return example:

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
        "optional": []
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
                //When payerType==01, payerPersonName is required "payerPersonName"
            ],
            "00": [
                //When payerType==00, payerCompanyName is required "payerCompanyName"
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
                "value": "Work Permit"
            },
            {
                "code": "2",
                "value": "International Passport"
            },
            {
                "code": "3",
                "value": "ID card"
            },
            {
                "code": "4",
                "value": "Social Security"
            },
            {
                "code": "5",
                "value": "Residence Permit"
            },
            {
                "code": "6",
                "value": "Company Registration Number"
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

**4 Response field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
Payment party | payer | ParamField | M | Payment party required field requirements |
| Payee | payee | ParamField | M | Required fields for payee |
| Enumeration value field | selectOption | Object | O | The enumeration value of some fields of the payer and payer, the code is the value that should be passed, and the value is the corresponding description |
| Optional conditions | condition | Object | O | Pre-optional conditions |
| List of supported banks | bankList | `List<String>` | O | List of supported bank names |

**ParamField's field**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Required fields | required | `List<String>` | M | Required fields |
| Optional fields | optional | `List<String>` | M | Optional fields |

### 5.3.10 International remittance history transaction query

**1 Function description**

| Transaction Code | TP3006 |
|----|----|
| Function name | International remittance history transaction query |
| Function description | International remittance history transaction query |
| Calling method | Real-time interface |
| Calling process | - |
| Application Scenarios | Query past historical transactions of international remittances |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3006`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Query start time | startTime | Long | O | Unix 13-bit timestamp, query start time, closed interval |
| Query end time | endTime | Long | O | Unxi 13-digit timestamp, query end time, closed interval |
| Quote ID | quoteId | Long | O | Quote ID |
| Merchant order number | merOrderNo | String | O | Merchant order number |
<aside class="success">
If startTime and endTime are not filled in, one of quoteId and merOrderNo must be filled in. If both quoteId and merOrderNo are not filled, startTime and endTime are required, and the interval cannot exceed 24 hours
</aside>

**4 Response field**


**Return object is `List<RemittanceHistory>`**

**Fields of RemittanceHistory**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Quote ID | quoteId | long | M | Quote ID |
| Receiving country | countryCode | string | M | iso 3166-1 standard 2-character code |
| Receiving currency | arriveCurrency | string | M | Receiving currency, 3-digit standard currency code |
| Debit currency | debitCurrency | string | M | Debit currency, 3-digit standard currency code |
| Payment method | payType | string | M | Optional values: local or swift |
| Receiving account type | accountType | string | M | Only 1 (bank account) is currently supported |
| Payment amount | arriveAmount | string | M | Payment amount |
| Debit Amount | debitAmount | String | M | Debit Amount |
| Exchange rate | rate | String | M | Exchange rate |
| Status | status | string | M | status code |
| Result Code | resCode | String | M | Transaction Result Code |
| Result description | resMessage | String | M | Transaction result description |
| Transaction serial number | bizFlow | String | M | The unique serial number corresponding to international remittance transactions |
| Merchant order number | merOrderNo | String | M | Merchant order number |
| Payment and receipt fields | xxxxxx | String | M | The corresponding country fields are different, according to the data returned by tp3005 |
| Associated fx serial number | fxBizFlow | String | O | Associated fx serial number |



### 5.3.11 Withdrawal transaction history query

**1 Function description**

| Transaction Code | TP3007 |
|----|----|
| Function name | Withdrawal history transaction query |
| Function description | Withdrawal history transaction query |
| Calling method | Real-time interface |
| Calling process | - |
| Application Scenarios | Query past withdrawal history transactions |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3007`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Query start time | startTime | Long | O | Unix 13-bit timestamp, query start time, closed interval |
| Query end time | endTime | Long | O | Unxi 13-digit timestamp, query end time, closed interval |
| Business order number | bizFlow | String(32) | O | Unique serial number generated by OTT |
| Merchant order number | merOrderNo | String(32) | O | Merchant order number |

<aside class="success">
If startTime and endTime are not filled in, one of bizFlow and merOrderNo must be filled in. If both bizFlow and merOrderNo are not filled, startTime and endTime are required, and the interval cannot exceed 24 hours
</aside>


> Return example:

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
    "remark": "xxx company trade cash withdrawal",
    "bizFlow":"3213347378487348734",
    "status":"SUCCESS",
    "code":"S00000",
    "message":"Success",
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
    "remark": "xxx company trade cash withdrawal",
    "bizFlow":"3213347378487348734",
    "status":"SUCCESS",
    "code":"S00000",
    "message":"Success",
    "createTime": 1595228842000
}
]
```

**4 Response field**


**Returned object is `List<WithdrawBean>`**

**Field of WithdrawBean**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Merchant order number | merOrderNo | string(32) | M | Merchant passes in the unique order number of this transaction |
| Currency | currency | string(3) | M | Withdrawal currency, 3-digit standard currency code |
| Amount | amount | decimal(18,2) | M | Withdrawal amount |
| Withdrawal account name | bankAccountName | string(64) | M | Withdrawal account name |
| Bank account number/IBAN | bankAccountNo | string(64) | M | Withdraw bank account number or IBAN |
| Bank Name | bankName | string(64) | M | Withdrawal Bank Name |
| Bank Address | bankAddress | string(256) | M | Withdrawal Bank Address |
| swift code | swiftCode | string(32) | M | swift code of the withdrawal bank |
| Proxy Bank Name | proxyBankName | string(64) | O | Proxy Bank Name |
| Proxy Bank Address | proxyBankAddress | string(256) | O | Proxy Bank Address |
| Proxy swift code | proxySwiftCode | string(32) | O | Proxy swift code |
| Remittance postscript | remark | string(64) | O | Remittance postscript |
| Callback address | callbackUrl | string(256) | M | Callback address |
| Business serial number | bizFlow | string(32) | M | Unique serial number generated by OTT |
| Transaction result status | status | string(8) | M | Transaction result status |
| Transaction Result Code | code | string(8) | M | Transaction Result Code |
| Result description | message | string(64) | M | Transaction result description |
| Withdrawal initiation time | createTime | long | M | Withdrawal initiation time |

### 5.3.12 Recharge transaction history query

**1 Function description**

| Transaction Code | TP3008 |
|----|----|
| Function name | Recharge history transaction query |
| Function description | Recharge history transaction query |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | Query past recharge history transactions |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3008`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Query start time | beginDate | Long | O | Unix 13-bit timestamp, query start time, closed interval |
| Query end time | endDate | Long | O | Unix 13-bit timestamp, query start time, closed interval |
| Business order number | batchNo | String(32) | O | Unique serial number generated by OTT |
| Recharge Bank | bankCode | String(8) | O | Recharge Bank Code |
| Deposit currency | currency | String(3) | O | Deposit currency |
| Query minimum amount | minAmount | decimal(18,2) | O | Query minimum amount |
| Query maximum amount | maxAmount | decimal(18,2) | O | Query maximum amount |
| Recharge status | status | String(3) | O | Recharge status 01: "Pending"; 02: "Recharge successful"; 03: "Recharge refused" |
| Page Number | pageNum | Integer | O | Query Page Number |
| How many items per page | pageSize | Integer | O | How many items per page, each page supports up to 100 items |


> Return example:

```json
{
"pageNum": 1,
"pageSize": 10,
"total": 35,
"list": [{
"batchNo": "20180122SDC760719",
"curType": "USD",
"amount": "10000.00",
"bank": "Bank of China",
"status": "02",
"createTime": "2020-06-28 17:17:45",
"updateTime": "2020-06-29 16:56:54",
"account": "Company Name1"
},{
"batchNo": "11191226453692390002",
"curType": "CNY",
"amount": "240.06",
"bank": "Bank of China",
"status": "02",
"createTime": "2019-12-26 15:29:29",
"updateTime": "2019-12-26 15:29:39",
"account": null
}]
}
```

**4 Response field**


| Name | Json tag | Type | Attribute | Value description |
 |----|----|----|----|----|
| Current page number | pageNum | Int | M | - |
| Number of pages displayed | pageSize | Int | M | - |
| Total | total | Int | M | - |
| Recharge flow information collection | list | `List<RechargeRecord>` | M | - |

**Fields of RechargeRecord**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Recharge order | batchNo | string(32) | M | Recharge order |
| Currency | curType | string(3) | M | Deposit currency, 3-digit standard currency code |
| Amount | amount | decimal(18,2) | M | recharge amount |
| Recharge Bank | bank | string(64) | M | Recharge Bank |
| Recharge account | account | string(64) | M | Recharge account |
| Recharge status | status | string(2) | M | Recharge status 01: "Pending"; 02: "Recharge successful"; 03: "Recharge refused" |
| Recharge initiation time | createTime | Date | M | Recharge initiation time |
| Recharge entry time | updateTime | Date | M | Recharge entry time |

### 5.3.13 Account flow transaction query

**1 Function description**

| Transaction Code | TP3009 |
|----|----|
| Function name | Account flow history transaction query |
| Function description | Account flow history transaction query |
| Calling method | Real-time interface |
| Calling process | - |
| Application Scenarios | Inquiry of past historical transactions of accounting flow |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3009`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Query start time | beginDate | Long | O | Unix 13-bit timestamp, query start time, closed interval |
| Query end time | endDate | Long | O | Unix 13-bit timestamp, query start time, closed interval |
| Business order number | batchNo | String(32) | O | Unique serial number generated by OTT |
| Currency | currency | String(3) | O | Currency |
| Income and Expenditure Type | flowType | String(3) | O | Income and Expenditure Type 1: "Into Gold", 2: "Withdraw" |
| Flow Type | busiType | String(3) | O | [6.1.6 Flow Type](#616-busitype-Flow Type) |
| Page Number | pageNum | Integer | O | Query Page Number |
| How many items per page | pageSize | Integer | O | How many items per page, each page supports up to 100 items |


> Return example:

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

**4 Response field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Current page number | pageNum | Int | M | - |
| Number of pages displayed | pageSize | Int | M | - |
| Total | total | Int | M | - |
| Accounting flow information collection | list | `List<CurFlowRes>` | M | - |

**Fields of CurFlowRes**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Accounting Flow Order | batchNo | string(32) | M | Accounting Flow Order |
| Currency | currency | string(3) | M | Account transaction currency, 3-digit standard currency code |
| Flow Type | busiType | String(3) | M | [6.1.6 Flow Type](#616-busitype-Flow Type) |
| Deposit | inAmount | decimal(18,2) | M | Deposit amount |
| Withdrawal | outAmount | decimal(18,2) | M | Withdrawal amount |
| Available Amount | vailAmount | decimal(18,2) | M | Available Amount |
| Transaction time | busiDate | Date | M | Transaction time |


### 5.3.14 Transaction fee transaction history query

**1 Function description**

| Transaction Code | TP3010 |
|----|----|
| Function name | Transaction fee history transaction query |
| Function description | Transaction fee history transaction query |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | Query past transaction fee history transactions |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3010`

**Method:** `POST`

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Query start time | beginDate | Long | O | Unix 13-bit timestamp, query start time, closed interval |
| Query end time | endDate | Long | O | Unix 13-bit timestamp, query start time, closed interval |
| Business order number | batchNo | String(32) | O | Unique serial number generated by OTT |
| Business Type | busiType | String(6) | O | [Business Type](#_6-1-5-biztype-Business Type) |
| Handling fee status | status | String(3) | O | Handling fee status 10: "Not charged", 11: "Received", 12: "Returned" |
| Page Number | pageNum | Integer | O | Query Page Number |
| How many items per page | pageSize | Integer | O | How many items per page, each page supports up to 100 items |



> Return example:

```json
{
"pageNum": 1,
"pageSize": 10,
"total": 2343,
"list": [{
"batchNo": "41200514566616790045",
"merSingleBatchNo": "10011",
"bizType": "C00002",
"tradeCurrency": "PHP",
"tradeAmt": 60000.0000,
"feeCurrency": "USD",
"feeTradeAmt": 2.0000,
"status": "11",
"tradeTime": "2020-05-14 19:57:33",
"remark": "Real-time transaction fee turnover"
}]
}
```

**4 Response field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Current page number | pageNum | Int | M | - |
| Number of pages displayed | pageSize | Int | M | - |
| Total | total | Int | M | - |
| Collection of fee information | list | `List<FeeFlowRes>` | M | - |

**Fields of FeeFlowRes**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Order number | batchNo | string(32) | M | order number |
| Merchant order number | merSingleBatchNo | string(32) | O | Merchant passes in the unique order number of this transaction |
| Business Type | bizType | String(6) | M | [Business Type](#_6-1-5-biztype-Business Type) |
| Fee currency | feeCurrency | String(3) | O | fee currency, 3-digit standard currency code |
| Transaction amount corresponding to fee currency | feeTradeAmt | decimal(18,2) | M | Transaction amount corresponding to fee currency |
| Handling fee status | status | string(2) | M | Handling fee status 10: "Not charged", 11: "Received", 12: "Returned" |
| Transaction currency | tradeCurrency | string(3) | M | Transaction currency, 3-digit standard currency code |
| Transaction Amount | tradeAmt | decimal(18,2) | M | Transaction Amount |
| Trading Time | tradeTime | Date | M | Trading Time |
| Remarks | remark | string(1024) | M | Remarks |

### 5.3.15 One-day price inquiry interface

**1 Function description**


| Transaction Code | TP3011 |
|----|----|
| Function name | One-day price inquiry |
| Function description | One-day price inquiry |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenario | Used to obtain the reference price of the currency pair on the day, which is convenient for merchants to use for exchange rate conversion |

<aside class="success">
Quotation results are only for reference, not for actual transactions
</aside>

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3011`

**Method:** `POST`

> Request example:

```json
{
    "sellCurrency":"USD",
    "buyCurrency":"CNY"
}
```

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Sell Currency | sellCurrency | String(3) | M | Sell Currency |
| Buy currency | buyCurrency | String(3) | M | Buy currency |


> Return example:

```json
{
    "sellCurrency":"USD",
    "buyCurrency":"CNY",
    "rate":"7.0102"
}

```

**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Sell Currency | sellCurrency | String(3) | M | Sell Currency |
| Buy currency | buyCurrency | String(3) | M | Buy currency |
| Exchange rate | rate | String(18) | M | Exchange rate quote |

### 5.3.16 VA account opening query interface

**1 Function description**


| Transaction Code | TP3012 |
|----|----|
| Function name | VA account opening query interface |
| Function description | VA account opening query interface, after submitting a VA application, you can query account specific information through this interface |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | VA account opening query interface |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3012`

**Method:** `POST`

> Request example:

```json
{
    "bizFlow":"7123498239859278274"
}
```

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Query start time | startTime | Long(13) | O | Unix 13-bit timestamp, query start time, closed interval |
| Query end time | endTime | Long(13) | O | Unxi 13-digit timestamp, query end time, closed interval |
| OTT side business order number | bizFlow | String(32) | O | Order number returned when VA account is opened |
| Merchant order number | merOrderNo | String(32) | O | Merchant order number |
<aside class="success">
If startTime and endTime are not filled in, one of bizFlow and merOrderNo must be filled in. If both bizFlow and merOrderNo are not filled, startTime and endTime are required, and the interval cannot exceed 24 hours. According to the query of startTime and endTime, up to 100 entries are displayed.
</aside>


> Return example:

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

**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Merchant order number | merOrderNo | String(32) | M | Merchant order number |
| OTT side business order number | bizFlow | String(32) | M | Order number returned when VA account is opened |
| VA details | vaInfos | List | M | VA details |



**VaInfo fields**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| VA account name | accountName | string(255) | O | VA account name |
| VA account number | accountNo | string(64) | O | VA account number |
| SwiftCode | swiftCode | string(11) | O | Bank's SwiftCode |
| Bank Name | bankName | string(128) | O | Bank Name |
| Bank Address | bankAddress | string(255) | O | Bank Address |
| Country/Region | area | string(64) | O | Country/Region |
| Bank Code | bankCode | string(12) | O | Bank Code |
| Branch Number | branchCode | string(12) | O | Branch Number |
| Supported currencies | currency | string(255) | O | Supported currencies, multiple currencies are separated by |
| VA account status | status | string(8) | M | VA account status, ON: enable, OFF: disable/reject OPENING: account opening |
| Remark | remark | string(8) | O | When it is OFF, the specific reason for prohibition/rejection will be displayed |
| Application time | createTime | long | M | VA account opening application time |
| Modification time | updateTime | long | M | Modification time of VA account opening |


### 5.3.17 Collection flow and trade order association query interface

**1 Function description**


| Transaction Code | TP3014 |
|----|----|
| Function name | Collection flow and trade order related query interface |
| Function description | After submitting the collection flow and trade order association application, check whether the trade collection is credited through this interface |
| Calling method | Real-time interface |
| Calling process | - |
| Application Scenarios | After submitting the collection flow and trade order association application (TP1013), check whether the trade collection is credited through this interface |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3014`

**Method:** `POST`

> Request example:

```json
{
       "contactNo":"62291060316483300005",
       "flowNo":"63291062211570000002"
}
```

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Query start time | startTime | Long(13) | O | Unix 13-bit timestamp, query start time, closed interval |
| Query end time | endTime | Long(13) | O | Unxi 13-digit timestamp, query end time, closed interval |
| Trade order code | contactNo | string(32) | O | Trade order code, tp2008 returns |
| Collection flow code | flowNo | string(32) | O | Collection flow code, tp3015 returns |
| Business serial number | bizFlow | string(32) | O | The unique business order number on the OTT side, tp1013 returns |
<aside class="success"> 
If startTime and endTime, the interval cannot exceed 24 hours. According to the query of startTime and endTime, up to 100 entries are displayed.
</aside>


**4 Response field**



| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Information Collection | relateList | `List<ConfirmRelatetionReq>` | M | - |

**ConfirmRelatetionReq field: **

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Trade order code | contactNo | string(32) | M | Trade order code |
| Collection flow code | flowNo | string(32) | M | Collection flow code |
| Account currency | currency | string | M | Account currency, 3-digit standard currency code |
| Payment amount | amount | decimal(18,2) | M | Payment amount |
| Fee Currency | feeCurty | String | M | Fee currency, 3-digit standard currency code |
| Handling fee amount | feeAmt | decimal(18,2) | O | OTT PAY charges a handling fee |
| Entry time | approveTime | bigInt(13) | M | Entry timestamp (milliseconds) |
| Status | status | string(2) | M | '01-under review 02-pass 03-rejected' |
| Result description | message | string(64) | M | Transaction result description |

### 5.3.18 Trade Receipt VA Entry Inquiry Interface

**1 Function description**


| Transaction Code | TP3015 |
|----|----|
| Function name | Trade collection VA entry query interface |
| Function description | Trade receipt VA account query interface |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | You can query the specific receipt flow of the VA account |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3015`

**Method:** `POST`

> Request example:

```json
{
       "flowNo":"62291060316483300005"
}
```

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Query start time | startTime | Long(13) | O | Unix 13-bit timestamp, query start time, closed interval |
| Query end time | endTime | Long(13) | O | Unxi 13-digit timestamp, query end time, closed interval |
| VA billing order number | flowNo | string(32) | O | VA billing order number |
<aside class="success"> 
The interval between startTime and endTime cannot exceed 24 hours. According to the query of startTime and endTime, up to 100 entries are displayed. If startTime and endTime are not filled in, bizFlow is required.
</aside>


> Response example:

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

**4 Response field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Transaction serial number | flowNo | string(32) | M | The unique serial number of trade receipts |
| Received Amount | receiveAmount | decimal(18,2) | M | VA Received Amount |
| Payment currency | receiveCurrency | string(3) | M | VA Payment currency |
| Entry VA account number | vaAccount | string(16) | M | Entry VA account number |
| Payer name | senderName | string(64) | O | Payer name |
| Payer Account | senderAccount | string(32) | O | Payer Account |
| Payment time | receiveTime | string(10) | M | Payment time, 10-digit unix timestamp |



### 5.3.19 Trade order application information query

**1 Function description**


| Transaction Code | TP3013 |
|----|----|
| Function name | Trade contract result information query |
| Function description | Providers query the creation status of trade contracts |
| Calling method | Real-time interface |
| Calling process | - |
| Application scenarios | Merchants need to query the status of the order contract |

**2 Request address**


**Url:** `https://{baseUrl}/api/tp3013`

**Method:** `POST`

> Request example:

```json
{
       "startTime":"168419019000",
       "endTime":"168419019000",
       "contractNo":"62291060316483300005",
       "merOrderNo":"23455560316483300005"
}
```

**3 Request field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Query start time | startTime | Long(13) | O | Unix 13-bit timestamp, query start time, closed interval |
| Query end time | endTime | Long(13) | O | Unxi 13-digit timestamp, query end time, closed interval |
| Trade contract number | contractNo | string(32) | O | [5.1.13 Trade order application] Return to trade contract number |
| Order number | merOrderNo | string(32) | O | Order number provided by the merchant |
<aside class="success"> 
The interval between startTime and endTime cannot exceed 24 hours. According to the query of startTime and endTime, up to 100 entries are displayed. If startTime and endTime are not filled in, contractNo is required.
</aside>


> Response example:

```json
{
   "contractList":[
                   {
                       "contractNo":"2120319391838111181",
                       "status":"SUCC",
                       "message":"Success",
                       "merOrderNo":"23134141421414",
                       "orderNo":"2021062819217",
                       "currency":"CNY",
                       "amount":"7010.20",
                       "tradeType": "00",
                       "buyerName": "TX",
                       "buyerArea":"China",
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
                       "logCompany":"International Trade Logistics Company",
                       "annexUrl":["/src/iiii/a.png","/src/iiii/b.pdf","/src/iiii/c.png"]
                   }
                 ]
}
```

**4 Response field**


| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Trade Order | contractList | `List<contractList>` | M | Trade Order Collection |


**contractList**

| Name | Json tag | Type | Attribute | Value description |
|----|----|----|----|----|
| Merchant unique order number | merOrderNo | string(32) | M | Merchant unique order number |
| Order currency | currency | string(3) | M | Order currency |
| Total order amount | amount | Decimal(18,2) | M | Total order amount |
| Trade Type | tradeType | string(2) | M | Trade Type Default: 00-Goods Trade |
| Buyer Name | buyerName | string(64) | M | Buyer Name |
| Purchaser's area | buyerArea | string(64) | M | Purchaser's area |
| Item information | goodsList | `List<goodsList>` | M | Item information The number of items does not exceed 10 |
| Transaction Date | transcationDate | string(10) | M | Transaction Date Format: yyyy-MM-dd |
| Transaction Voucher | transcationCert | `Array` | M | An array of multiple voucher file addresses (the file size does not exceed 20M) |
| Logistics Status | logStatus | string(1) | M | 0-unshipped 1-shipped |
| Logistics order number | logNo | string(64) | O | Logistics order number |
| Logistics company name | logCompany | string(64) | O | Logistics company name |
| Logistics attachments | annexUrl | `Array` | O | Logistics attachments (file size not more than 20M)
| Trade order number | contractNo | string(32) | M | Trade order number (unique) | |
| Trade order status | status | string(8) | M | Trade order status ACCEPT-in process SUCC-success FAIL-failure|
| Query result description | message | string(128) | M | Query result description |


# 6 Appendix

## 6.1 Field description
### 6.1.1 paymentType transaction type

| Field Value | Description | Remarks |
|----|----|----|
| B2B | Business to Business | - |
| B2C | Business to Individual | - |
| C2B | Individual to Business | - |
| C2C | Individual to Individual | - |

### 6.1.2 tradeCodeType transaction code

| Field Value | Description | Remarks |
|----|----|----|
| TRADE | Offline general goods trade | General trade |
| STAY | Hotel Fees | Hotel Accommodation |
| AIRLINE_TICKET | Travel | Air Ticket |
| STUDY_ABROAD | Education-related student expenses | Study abroad |
| SOFTWARE | Consulting fees, technical services, academic fees, expert fees | Management consulting, software development |
| LOGISTICS | Cargo Logistics Fee | Logistics Fee |
| INFO_CHARGES | Information Service Fee | Software |
| ADVER_SERVICE | Advertising or public relations costs | Advertising services, public relations services, international exhibitions, conferences |
| EXPORTED_GOODS | Payment for goods | Cross-border e-commerce |
| SALARY | Wage or commission payment | Labor service |
| ONLINE_GAME | Online Game Equipment | Game |
| E_COMMERCE | E-commerce | E-commerce |

### 6.1.3 payMethod payment method

| Field Value | Description | Remarks |
|----|----|----|
| cash_on_delivery | Payment method is cash on delivery | cash on delivery |
| advance | Payment method is advance payment | advance payment |



### 6.1.4 purpose Payment purpose

| Field Value | Purpose of Remittance (en) | Purpose of Remittance (zh) |
|----|----|----|
| 1 | Transfer to own account |
| 2 | Family Maintenance | Family Support |
| 3 | Education-related student expenses | Education-related student expenses |
| 4 | Medical Treatment | Medical Expenses |
| 5 | Hotel Accomodation | Hotel Fees |
| 6 | Travel |
| 7 | Utility Bills | Pay infrastructure bills for water, electricity, coal, etc. |
| 8 | Repayment of Loans | Repayment of Loans |
| 9 | Tax Payment | Tax Payment |
| 10 | Purchase of Residential Property | Purchase of Residential Property |
| 11 | Payment of Property Rental | Payment of Property Rental |
| 12 | Insurance Premium | Insurance Prepaid |
| 13 | Product indemnity insurance | Product insurance |
| 14 | Insurance Claims Payment |
| 15 | Mutual Fund Investment | Mutual Fund Investment |
| 16 | Investment in Shares | Equity Investment |
| 17 | Donations | Donations |
| 18 | Information Service Charges | Information Service Charges |
| 19 | Advertising & Public relations-related expenses | Advertising or public relations expenses |
| 20 | Royalty fees, trademark fees, <br>patent fees, and copyright fees | Loyalty service fees, trademark fees, patent fees and copyright fees |
| 21 | Fees for brokers, front end fee, <br>commitment fee, guarantee fee and custodian fee | Transaction fee, guarantee fee, factoring fee |
| 22 | Fees for advisors, technical assistance, <br>and academic knowledge, including remuneration for specialists |
| 23 | Representative office expenses | Representative office expenses |
| 24 | Construction costs/expenses | Construction costs/expenses |
| 25 | Transportation fees for goods | Commodity transfer fees |
| 26 | For payment of exported goods |
| 27 | Delivery fees for goods | Commodity logistics fees |
| 28 | General Goods Trades-Offine trade | General Goods Trades-Offine trade |
| 29 | Other services charges | Other services trade charges |
| 30 | Salary / Commission Payment | Salary or Commission Payment |
| 31 | Fixed Maintenance Expenses | Regular Maintenance Expenses |
| 99 | Other fees (Please specify) | Other fees (Please specify) |

### 6.1.5 bizType Business Type

| Field Value | Description |
| ------ | --------------- |
| 000008 | E-commerce collection fee |
| 000012 | VA monthly management fee |
| 000013 | Trade collection fee |
| 000015 | Monthly platform maintenance fee |
| C00001 | Cross-border RMB Entry" |
| C00002 | Global distribution |
| C00003 | Platform deposit fee |
| C0000 | Platform withdrawal fee |

### 6.1.6 busiType pipeline type

| Field Value | Description |
| ------ | -------------- |
| C00 | Account flow |
| C01 | Currency Exchange |
| C02 | Exchange Return |
| C05 | RMB payment |
| C06 | RMB payment refund |
| C07 | Foreign currency payment |
| C08 | Foreign currency payment refund |
| C09 | Withdraw |
| C10 | Withdrawal Return |
| C11 | Handling fee |
| C12 | Handling fee refund |
| C13 | Collection |