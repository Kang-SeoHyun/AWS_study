# 🫧 AWS 🫧
-> 백엔드는 주목!
```txt
컴퓨팅 파워 (서버)
- AWS EC2
- AWS Elastic Beanstalk
- AWS ECS
- AWS Fargate
- AWS Lambda(Serverless)
```

## 🧴AWS EC2🧴
> Amazon Elastic Cloud Compute - E C C - EC2

* 가장 기본적인 형태의 클라우드 컴퓨팅 (= 클라우드 컴퓨터 한 대)
* 온디맨드: 선결제 금액이나 장기 약정 없이 저렴하고 유연하게 Amazon EC2를 사용하기 원하는 사용자
	* 스팟 인스턴스: 시작 및 종료 시간이 자유로운 애플리케이션
	* Saving Plans: 1년 또는 3년 기간의 일정 사용량 약정을 조건으로 EC2 및 Fargate 사용량에 대해 저렴한 요금을 제공하는 유연한 요금

## AWS Elastic Beanstalk
> Amazon Elastic Beanstalk

* AWS 클라우드에서애플리케이션을신속하게 배포하고 관리할 수 있는 서비스 (애플리케이션코드를 업로드하기만하면 작동)
* Elastic Beanstalk = EC2 + 배포 버전 관리 (롤백) + Elastic Load Balancer + 모니터링 + 로그 트래킹 + 오토 스케일링
* 다양한 언어 지원: .NET / PHP / Java / Ruby / Node.js / Python / Docker / Go

## AWS Fargate

* Fargate를 사용하면 더 이상 컨테이너를 실행하기 위해 가상 머신의 클러스터를 프로비저닝, 구성 또는 조정할 필요가 없습니다. 따라서 서버 유형을 선택하거나, 클러스터를 조정할 시점을 결정하거나, 클러스터 패킹을
최적화할 필요가 없습니다.
* 이전에는 컨테이너를 실행하기 위해서는 컨테이너를 실행할 Instance(EC2)를 실행시켜야하였지만, AWS Fargate는 이러한 수고를 덜어 줌

## AWS 서비스 비교

❓왜 Fargate 대신에 EC2를 쓸까❓

❓왜 Fargate 대신에 Elastic Beanstalk을 쓸까❓

<img width="100" alt="Screen Shot 2023-05-20 at 12 03 52 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/f9480c88-df42-45bb-8d60-948ee0de3f80">
<img width="327" alt="Screen Shot 2023-05-20 at 12 04 00 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/fbb07f3d-5e01-492e-9c8f-7423ea217bc4">


## AWS ECR
> Amazon Elastic Container Registry - E C R
* Amazon Elastic Container Registry(Amazon ECR)는 안전하고 확장가능하고 신뢰할 수 있는 AWS 관리형 컨테이너 이미지 레지스트리 서비스
* RDS (DB) = 데이터를 저장하는 장소
* S3 = 사진, 이미지 등 파일을 저장하는 장소
* ECR = 도커 이미지를 저장하는 장소

## AWS ECS
> Amazon Elastic Container Service - E C S
* ECS(Elastic Container Service)는 AWS에서 제공하는 컨테이너 오케스트레이션서비스로 여러 어플리케이션컨테이너를 쉽고 빠르게 실행하고, 컨테이너를 적절하게 분배 및 확장 & 축소 할 수 있도록 도와주는 서비스
* AWS EC2 와 AWS Fargate 중 원하는 환경에서 실행 가능

### 용어 정리
Task Definition: 컨테이너의 이미지, CPU/메모리 리소스 할당 설정, port 매핑, volume 설정
Task: Task 안에는 한 개 이상의 컨테이너들이포함되어 있으며 ECS에서 컨테이너를 실행하는 최소 단위는 Task이다. (인스턴스화)
Service: Task 들의 Life cycle 을 관리하며, 오토스케일링과로드밸런싱을 관리
Cluster: Task 가 배포되는 Container Instance 들은 논리적인 그룹

<img width="600" alt="Screen Shot 2023-05-20 at 12 02 51 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/1a3341a2-fe41-4dec-a6d5-1bbc37486a9b">


<img width="600" alt="Screen Shot 2023-05-20 at 12 03 08 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/0fcd55aa-7aaa-4c77-b683-074c74d90d43">


## AWS Lambda
> Amazon Lambda
* 서버 없이도 코드를 실행시킬 수 있는 서버리스 컴퓨팅 서비스
* 코드를 돌리기위한 리소스를 임의로 지정할 수 있으며, 사용 리소스 x 사용 시간에 따라 과금이 된다. (ex. 메모리 용량 / 코어 갯수)
* 최대 15분 / 최대 10GB / 최대 6개의 Core
* 사용 예시
	\- 비동기 처리 (이미지 썸네일 생성)
	\- 예측이 불가능 한 리소스 사용 (대용량 처리 / 머신러닝)

### ❓왜 항상 켜져있어야 하는 EC2 / Elastic Beanstalk 대신에 가성비 있는 Lambda을 선택하지 않을까❓

### Cold Start / Warm Start
* 기본적으로 EC2와 같은 인스턴스보다는 Latency가 높다.
* 콜드 스타트: 배포 패키지의 크기와 코드 실행 시간 및 코드의 초기화 시간에 따라 새 실행 환경으로 호출을 라우팅할 때 지연 시간이 발생하는 람다 호출 시작 (겨울에 자동차 시동 걸때에서 유래 됨)
* 5분정도 warm하게 유지
* 계속 warm하게 유지하기 위해선 지속적으로 사용해야 하는 방법밖엔 없음


Cold Start / Warm Start

<img width="400" alt="Screen Shot 2023-05-20 at 12 22 30 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/4c0dafdf-313c-4e9f-a418-22b7edb54f73">

<img width="400" alt="Screen Shot 2023-05-20 at 12 22 43 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/1c17c638-dc04-41f4-bbfc-4c1785e6939d">

일반 적인 서버 latency: 100ms 이하

상황
1. 만약에 하루에 request가 10000개 밖에 안온다 (많이 사용하지 않는 서비스 / API / 기능이다)
2. 병렬처리 (youtube에 영상을 올리면 1080p, 720p로 인코딩 되는 상황)

## AWS Lambda - Serverless
Serverless Framework : <img width="100" alt="Screen Shot 2023-05-20 at 12 25 11 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/a082cebd-b020-4618-84b3-4599f8a004c1">

1. AWS, Azure, GCP 등의 서버리스 서비스를 쉽게 사용할 수 있도록 도와주는 오픈소스 프레임 워크

2. 사용 가능 서버:
* Node 계열 – ExpressJS, NestJS 등..
* Java 계열 – Spring(Spring Cloud Function),
* Python 계열 – FastAPI, Flask 등..

3. 소규모 / 이용자가 많지 않은 서비스에서 가격 효율적으로 이용 가능
