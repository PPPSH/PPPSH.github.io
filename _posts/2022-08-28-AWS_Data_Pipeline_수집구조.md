---
layout: single
title: "AWS Data Pipeline_수집구조"
categories: AWS
tag: [AWS, Kinesis,Firehose, API Gateway,S3]
#toc: true 
author_profile: false
sidebar:
    nav: "docs"
---

### AWS 클라우드 환경 내 수집 프로세스 구축1

소스, 실시간 데이터생성 전달 (RESTFul API) -> 처리(Kinesis) -> 타켓 저장(S3) 

사용 서비스 : EC2, API Gateway , Kinesis Streams, Kinesis Firehose  , S3

![aws_arc](../../images/2022-08-28-AWS_Data_Pipeline_수집구조/aws_arc.png)

### 1.  API Gateway
   외부 소스에서 AWS에 접근하는 Point, RESTFul API를 받아주는곳 

   API Gateway는 트래픽 관리, CORS 지원, 권한 부여 및 액세스 제어, 제한, 모니터링 및 API 버전 관리 등 최대 수십만 개의 동시 API 호출을 수신 및 처리하는 데 관계된 모든 작업을 처리

### 2. Kinesis Streams
   Like Kafka 
   실시간으로 스트리밍 데이터를 수집, 버퍼링 및 처리
<br>

### 3. Kinesis Firehose
   카프카의 컨슈머 같은 느낌 ? 

   실시간 스트리밍 데이터를 s3, Redshift , Splunk등 다양한 타켓소스로 전송하기 위한 서비스

### 4. S3
   어디서나 원하는 양의 데이터를 저장하고 검색할 수 있도록 구축된 객체 스토리지

​	