---
title: JWT(Json Web Token)中默认的声明含义
date: 2018-07-19 15:02:26
tags: [jwt,develop]
categories: [个人]
---

本文参考资料：

https://tools.ietf.org/html/rfc7519#section-4.1

<!-- more --> 

按照JWT协议的说法，默认的声明是可选的，目前是为了提供参考、增加payload效能，同时为各语言的实现提供参考。

## iss(Issuer)

jwt的颁发者，其值应为大小写敏感的字符串或Uri。

e.g.
```javascript
{
    "iss": "llbetter.com"
}
```

## aud(Audience)

jwt的适用对象，其值应为大小写敏感的字符串或Uri。一般可以为特定的App、服务或模块。

比如我们颁发了一个jwt给一个叫"JsonWebToken"的app使用，sub可以是这个app的包签名或者标识。

服务器端的安全策略在签发时和验证时，aud必须是一致的。

e.g.
```javascript
{
    "iss": "llbetter.com",
    "aud": "com.llbetter.JsonWebToken"
}
```

## sub(Subject)

jwt的所有者，可以是用户ID、唯一标识。

e.g.
```javascript
{
    "iss": "llbetter.com",
    "aud": "com.llbetter.JsonWebToken",
    "sub": "10000" // user id
}
```

## exp(Expiration Time) 

jwt的过期时间，必须是可以解析为时间/时间戳的数字类型。服务器端在验证当前时间大于过期时间时，应当验证不予通过。

e.g.
```javascript
{
    "iss": "llbetter.com",
    "aud": "com.llbetter.JsonWebToken",
    "sub": "10000", // user id
    "exp": 1516239022
}
```

## nbf(Not Before)

表示jwt在这个时间后启用。同exp一样，需为可以解析成时间的数字类型。

e.g.
```javascript
{
    "iss": "llbetter.com",
    "aud": "com.llbetter.JsonWebToken",
    "sub": "10000", // user id
    "exp": 151239022,
    "nbf": 151139022
}
```

## iat(Issued At)

jwt的签发时间。同exp一样，需为可以解析成时间的数字类型。

e.g.
```javascript
{
    "iss": "llbetter.com",
    "aud": "com.llbetter.JsonWebToken",
    "sub": "10000", // user id
    "exp": 151239022,
    "nbf": 151139022,
    "iat": 151039022
}
```

## jti(JWT ID)

签发jwt时给予当前token的唯一ID，通常用于一次性消费的token。

e.g.
```javascript
{
    "iss": "llbetter.com",
    "aud": "com.llbetter.JsonWebToken",
    "sub": "10000", // user id
    "exp": 151239022,
    "nbf": 151139022,
    "iat": 151039022,
    "jti": "550e8400-e29b-41d4-a716-446655440000"
}
```