---
layout: single
title: "Kafka Cluster ID doesn’t match Error"
categories: kafka
tag: [kafka]
#toc: true 
author_profile: false
sidebar:
    nav: "docs"
---


### Cluster ID doesn’t match stored clusterId in meta.properties

카프카 구동시 주피터 실행 시키고 , 브로커 실행 시킬때 마다 , 클러스터 id가 안맞는다는 에러를 뱉어냄

근본적인 해결방안은 아직 찾지 못했으나, 임시방편으로 

에러 로그를 잘 보면 2개에 id가 보이는데, 앞에 cluster id를 **<u>meta.properties</u>**파일에 업데이트 시켜 주고 구동 하면 완료 

(브로커 설정파일 (config/server.properties)안에 **<u>log.dirs</u>** = '경로' 에 가보면 meta.properties확인 가능 )



![meta](../../images/2022-08-19-kafka-cluster-error/meta.png)
