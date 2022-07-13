# API 

***Version 0.6.0.0에서 추가된 모든 API 안내서.***

----

## Syntax

**API 사용 구문을 정의 합니다.**

### Request 
HTTP Request Syntax를 사용하며

```
METHOD URI?Query HTTP/1.1
```

Request의 URI는 `cluster`섹션에 등록한 `named-cluster`가 포함하여야 합니다.    
`named-cluster`는 대소문자를 구분하지만, `uri` 와 `source uri`는 대소문자 구분을 하지 않으며 `lower case` 처리 됩니다.

[※ 사용 가능한 URI Query](query.md)

```
METHOD /{named-cluster}/{URI}?{Query} HTTP/1.1
```

!!! note ""
    GET /replica-name1/1.txt HTTP/1.1

### Authorization
Request Header에는 `Authorization`이 포함되어 있어야 합니다. 
단 `cluster.users`에 `anonymous` 익명 사용자를 허용 할 경우 인증절차 없이 사용 가능합니다.

```
Authorization: Basic  {base64(user/password)}
```

!!! note ""
    GET /replica-name1/1.txt HTTP/1.1    
    Authorization: Basic YWRtaW46YWRtaW4=

[※ RFC 7235, section 4.2: Authorization](https://tools.ietf.org/html/rfc7235#section-4.2)

----------------------------------------------------------------------------------------------------------------