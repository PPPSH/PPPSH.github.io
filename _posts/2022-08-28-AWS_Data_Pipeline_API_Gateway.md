---
layout: single
title: "AWS Data Pipeline[API Gateway]"
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

![aws_arc](../../images/2022-08-28-AWS_Data_Pipeline_API_Gateway/aws_arc.png)

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

---

## 1. API Gateway 설정
![api_gateway_0828](../../images/2022-08-28-AWS_Data_Pipeline_API_Gateway/api_gateway_0828-1693068.png)

1. 외부 소스로 부터 Restful API를 통해 호출 될것

2. 리소스 -> 메서드 순으로 생성 

3. Gateway를 통해 전달 받은 메시지를 Kinesis로 전달 하는 구조이므로, 통합유형은 AWS서비스 

4. AWS 리전은 EC2 리전과 동일하게 생성 

5. 작업은 PutRecord (향후 좀더 공부 예정...)

6. 실행역할은 IAM에서 추가 후 복사해서 사용 

   IAM , 역할만들기 -> EC2 사용사례에서 API Gateway -> 기본CloudWatch 권한정책으로 및 역할이름 생성(apigate  to kinesis 등 ..) ->

   정책연결을 통해 역할 추가 (AmazoneKinesisFullAccess) -> **요약에 역할 ARN내용 복사 후 활용** 

7. 저장

8. 그림 #3에 통합 요청 -> #4 에 HTTP 헤더 파일 수정 , 매핑 템플릿 수정 및 템플릿 추가 , **StreamName 이후 설정에 필요** 

   ```json
   #set ( $enter = "
   ")
   #set($json = "$input.json('$')$enter")
   {
    "Data": "$util.base64Encode("$json")",
    "PartitionKey": "$input.params('X-Amzn-Trace-Id')",
    "StreamName": "test-stream"
   }
   ```

   

9. 작업에 API 배포  후 생성 된 URL 활용 

   







