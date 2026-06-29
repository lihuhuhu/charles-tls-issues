## what's next

测试 charles MIMT 是否有特征

## the issues Charlse repeatedly sending requests carrying fingerprint info

MITM tls 流程 :  
mobile phone tls info -> charles tls -> server tls

repeat tls 流程 (charles client )  
charles tls -> server tls

## charles tls VS repeat tls

**1. cipher suite**

MITM tls

| mobile phone 支持                             | charles choices and to server         | server choices                        |
| --------------------------------------------- | ------------------------------------- | ------------------------------------- |
| TLS_ECDHE_ECDSA_WITH_A                        | TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 | TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 |
| TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384       | none                                  | none                                  |
| TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 | none                                  | none                                  |
| TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256         | none                                  | none                                  |
| TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384         | none                                  | none                                  |
| TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256   | none                                  | none                                  |
| TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA            | none                                  | none                                  |
| TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA            | none                                  | none                                  |
| TLS_RSA_WITH_AES_128_GCM_SHA256               | none                                  | none                                  |
| TLS_RSA_WITH_AES_256_GCM_SHA384               | none                                  | none                                  |
| TLS_RSA_WITH_AES_128_CBC_SHA                  | none                                  | none                                  |
| TLS_RSA_WITH_AES_256_CBC_SHA                  | none                                  | none                                  |

repeat tls

| charles client tls 支持 | server chosen                         |
| ----------------------- | ------------------------------------- |
| none                    | TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 |

**2. extensions: supported groups**

| MITM tls       | charles client tls |
| -------------- | ------------------ |
| x25519 (29)    | x25519 (29)        |
| secp256r1 (23) | secp256r1 (23)     |
| secp384r1 (24) | secp384r1 (24)     |
| secp521r1 (25) | secp521r1 (25)     |
| x448 (30)      | x448 (30)          |
|                | ffdhe2048 (256)    |
|                | ffdhe3072 (257)    |
|                | ffdhe4096 (258)    |
|                | ffdhe6144 (259)    |
|                | ffdhe8192 (260)    |

**3. extensions: application layer protocol negotiation**

| MITM tls | charles client |
| -------- | -------------- |
| h2       | h2             |
| http/1.1 |                |

## summary

charles 对请求进行重放的时候利用的是自身的指纹并非原始请求指纹，其支持加密套件和应用层协议会与原始请求有区别，部分风控厂家似乎已经检测到 charles repeat 和 charles MITM 的特征了

从 tls 握手来看，charles 的 MIMT 似乎也存在特征

telegram: [交流](https://t.me/+4MxaaiydQsVjYTVl)
