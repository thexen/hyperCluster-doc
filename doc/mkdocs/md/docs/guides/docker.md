# Kubernetes Configurations

***Kubernets 설정 안내서***

----

![대체 텍스트](../images/sync-001.png)

----
preference.yaml

    ...
    peers:
    peer1:
        addr: 192.168.10.111:8080
        volumes: 
            repo-name1: volume-name1
    ...




----

docker-compose.yaml  파일 설정

`/etc/hypercluster/artefacts/cert` 인증서 저장소   
`/etc/hypercluster/artefacts/onetimekey` onetime key 저장소 

    version: '3.4'

    services:
        hypercluster:
        privileged: true
        image: golang:1.14.4 
        ports:
        - 8080:8080
        working_dir: /app
    environment:
      - HYPERCLUSTER_PEER_HOSTNAME=peer1
      - HYPERCLUSTER_PEER_PREFERENCE_FILE=/etc/hypercluster/conf.d/preference.yaml
      - HYPERCLUSTER_PEER_LOG_PREFERENCE_FILE=/etc/hypercluster/conf.d/log.yaml
    volumes:
      - /home/centos/docker/hypercluster/peer:/app
      - /data:/data
      - /home/centos/docker/hypercluster/peer/conf.d:/etc/hypercluster/conf.d
      - /home/centos/docker/hypercluster/peer/artefacts:/etc/hypercluster/artefacts
      - /var/log/hypercluster:/var/log/hypercluster

    #command: ./hypercluster start -hostname peer1 -conf /etc/hypercluster/conf.d/preference.yaml -log /etc/hypercluster/conf.d/log.yaml
    command: ./hypercluster start
    