# API 

***Version 0.6.1.0에서 추가된 모든 API 안내서.***

----

## Objectstorage Synchronization

**API를 설명합니다.**

사용자가 접속한 `peer`에서 Objectstorage Synchronization API를 사용 할 경우 `cluster`에 참여한 모든 `peer`들에게 업로드 중인 파일이
실시간으로 sync가 진행됩니다.


### Upload

업로드 방법은 Version 0.6.0.0에서 설명한 업로드 API와 동일하며 업로드 된 파일은 HASH Code로 중복 확인을 거친후 중복제거 된 파일들만
저장소에 저장이 됩니다.
그리고 metadata는 mongodb와 연동하여 관리 됩니다.

인증없이 다운로드를 가능하게 할려면 `disclosure`를 query에 추가하여 업로드를 하여야 합니다.

!!! tip "disclosure 사용 방법"
    PUT /{named-cluster}/{URI}?disclosure HTTP/1.1

만약 `disclosure`를 설정 하지 않으면 `Authorization` 인증을 하여야 합니다

```
PUT /{named-cluster}/{URI} HTTP/1.1
Authorization: Basic  {base64(user/password)}
Content-Length: {`size`}
```

!!! note ""
    PUT /replica-name1/1.txt?pretty&disclosure HTTP/1.1    
    Host: 127.0.0.1:8080    
    Connection: Close   
    Authorization: Basic YWRtaW46YWRtaW4=    
    Content-Length: 20    
    
    12345678901234567890    

### Get Fileinfo

저장되어 있는 content의 정보를 가져옮니다.  
정보의 내용에는 onetimekey를 포함한 다운로드 `url`을 포함하고 있으며 해당 API를 사용 하기 위해서는 cluster role 이 `restapi`로 설정 되어 있어야 합니다

!!! note ""
    GET /{named-cluster}/fileinfo?key={URI}&validity=5m HTTP/1.1  
    Authorization: Basic  {base64(user/password)}  

`{URI}`는 업로드에서 사용한 URI를 입력하면 되며  
`validity`는 onetimekey의 유효 시간을 설정 합니다. 



### Download
다운로에는 인증이 필요 없는 content와 인증이 필요한 content가 있습니다.

업로드 시 disclosure를 설정하여 업로드 할 경우 업로드한 content에 한해 인증 없이 다운로드가 가능합니다.

!!! note ""
    GET /{named-cluster}/{URI}?collection={user} HTTP/1.1  

`collection` content의 개시자를 입력하면 됩니니다

인증이 필요한 content는 두가지 방식이 있으며
하나는 Authorization 설정 이고 다른 하나는 onetimekey를 이용하는 방법이 있습니다

!!! note ""
    GET /{named-cluster}/{URI} HTTP/1.1  
    Authorization: Basic  {base64(user/password)}  


!!! note ""
    GET /{named-cluster}/{URI}?onetimekey= HTTP/1.1  


### Get Prefix

업로드 되어 metadata로 관리되고 있는 목록을 가져 옮니다.  
해당 API를 사용 하기 위해서는 cluster role 이 `restapi`로 설정 되어 있어야 합니다

!!! note ""
    GET /{named-cluster}/prefix?key= HTTP/1.1  

key는 업로드시 uri의 path를 입력 하면 됩니다   
예를 들어 아래와 같이 업로드를 하였다면   

!!! note ""
    GET /cluster-name/1/2/a.txt HTTP/1.1    

uri는 `/{named-cluster}/prefix?key=/1/2` 게 됩니다.

----------------------------------------------------------------------------------------------------------------