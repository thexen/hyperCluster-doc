# URI Query

***URI Query 안내서***

----

!!! note ""
    pretty                


***Request 결과를 가독성이 좋은 상태로 가공하여 출력합니다.***

----

!!! note ""
    purge

***UPLOAD 또는 SYNC(PUSH) 할려는 파일이 대상 peer에 존재 한다면 저장이 완료 되는 시점에 최신파일 여부와 상관없이 swap을 합니다.***

----

!!! note ""
    cluster

***Request 결과에 Cluster정보를 포함하여 출력합니다.***

----

!!! note ""
    recursive

***FIND 명령에서 만 유효한 Query입니다. 검색하고자 하는 대상이 Directory인 경우 모든 하위 Direcectory의 정보를 출력합니다.***

----

!!! note ""
    disclosure

role: `objectstorage`  
***업로드 명령에서 discloure를 설정하여 업로들 하면 인증절차 없이 다운로드가 가능합니다.***

----

!!! note ""
    validity

role: `objectstorage`  
***content의 정보를 가져 올때 onetimekey도 함께 발급이 됩니다. 이때 발급된 onetimekey의 유효시간을 설정합니다.***  

        #휴효시간을 10분으로 설정
        validity=10m

----

!!! note ""
    collection

role: `objectstorage`  
***discloure 설정으로 업로드 된 content를 다운로드 할 때 사용되며, content의 개시자를 의미 합니다.***

----

!!! note ""
    key

role: `restapi`  
***metadata의 정보들 중에서 prefix와 key가 일치하는 목록을 가져올때 사용 됩니다.***