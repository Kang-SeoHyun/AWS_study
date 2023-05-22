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

특징 📋 :
1. 가장 기본적인 형태의 (서버) 클라우드 컴퓨팅 (= 클라우드 컴퓨터 한 대) EC2 기반의 서버들이 많다.
2. Auto Scaling을 해줍니다.
3. 탄력적 IP 주소
	* 임의의 IP 가 할당되는데 (public ip 주소 - 실제로 외부에서 들어가면 들어가지는 주소)
	* IP 주소를 고정해서 쓰고 싶다하면 할당 받을 수 있음. - 돈내야함
	* 적용안하면 IP 주소가 계속 바뀐다. - 캡디때 터지면 계속 바꿨던 이유,,
4. 인스턴트
	* 서버를 안 쓸때 다시 쓸 것 같으면 중지, 안 쓸 것 같으면 종료
	* 정지 : 컴터를 썼던 기록들을 저장한 채로 중지
	* 종료 : 끄는데 포맷까지 하는거

비용 💰 : 서버 비용 + 몇 기가의 데이터가 흘렀는지 + 네트워크가 얼마나 사용 되었는지
* 온디맨드: 선결제 금액이나 장기 약정 없이 저렴하고 유연하게 Amazon EC2를 사용하기 원하는 사용자
	* 쓴 만큼 돈 내기
* 스팟 인스턴스: 시작 및 종료 시간이 자유로운 애플리케이션
	* 쓰고 결제하는 시스템은 비슷한데, 온디맨드가 필요하다하면 스팟은 뺏길 수 있음. (안전성X)
	* 대신에 80%정도 싸다. 근데 안정성은 인정되지 않는다.
	* 돌리다 꺼져도 되는거에 많이 씀.
	* 백엔드에서 배치에서 쓰고 보통 머신러닝에서 많이 씀.
* Saving Plans: 1년 또는 3년 기간의 일정 사용량 약정을 조건으로 EC2 및 Fargate 사용량에 대해 저렴한 요금을 제공하는 유연한 요금
	* 온디맨드랑 비슷하지만 미리 약정을 걸고 좀 더 싼 가격에 쓸 수 있는 이점이 있다.

### EC2 들어가서 인스턴스 생성해보기❗️
1. EC2 입장
2. 오른쪽 인스턴스 시작 눌러서 만들기
	* 프리티어가 공짜로 사용가능하다는 것
3. 키페어 생성하기 - RSA, .pem
4. EC2에서 실행 중인 인스턴스 들어가서 오른쪽에 연결버튼 누르고 따라하면 됨
	* 프라이빗 키 위치 잊지않기. (멘토님: document에 있었음: .pem)

## 🥜 AWS Elastic Beanstalk - E B 🥜

특징 📋 :
1. 얘는 실제로 현업에서 좀 많이 사용함.
2. EC2베이스에 기능들이 들어간 서비스라고 생각하면 됨.
	* Elastic Beanstalk = EC2 + 배포 버전 관리 (롤백) + Elastic Load Balancer + 모니터링 + 로그 트래킹 + 오토 스케일링
3. AWS 클라우드에서 애플리케이션을 신속하게 배포하고 관리할 수 있는 서비스 (애플리케이션 코드를 업로드하기만 하면 작동)
4. 다양한 언어 지원: .NET / PHP / Java / Ruby / Node.js / Python / Docker / Go
5. 코드 업로드하면 얘가 서버 만들자나 그걸 github action(elb)로 연동시키면 깃에 올리는 것 만으로도 AWS랑 연동시켜서 바로바로 할 수 있대.
	* 새로운 EC2를 키고 거기에 디벨롭한다음 성공하면 EC2 바꿈!

### Elastic Beanstalk 들어가서 어플리케이션 생성해보기❗️
1. Elastic Beanstalk 입장
2. 이름 정해주고
3. 플랫폼(사용언어) 설정 가능
4. 코드 업로드에서 .zip파일 올리면 자동으로 해줌
	* 서버 키는 코드 있으면 서버도 켜줌.
5. 프리셋은 오토스케일링 할지 말지 뭐 이런거 설정해서 할 수 있다.
	* 고가용성으로 하면 인스턴스를 여러개 쓸 수 있음.
6. 인스턴스 설정 할 수 있다.
7. 뒤에 엄청 많은 건 뭐 찾아가보면서 하면 됨.
8. 그림 : <img width="700" alt="Screen Shot 2023-05-20 at 5 19 09 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/e0066bfa-fd38-4f11-9674-9ab3bcf66bb8">
	* EB 생성할때 서버를 한대 값이랑 몇대 킬지 같은 환경 정해두면, 코드를 올리면 EB가 알아서 관리해줌
	* VPC 같은 보안 관련 된 건 EB밖이라 직접 다 해줘야 함.

## 🚪 AWS Fargate 🚪

특징 📋 :
1. 도커파일 자체를 올리는 거라 간편해서 많이 사용함.
2. Fargate를 사용하면 더 이상 컨테이너를 실행하기 위해 가상 머신의 클러스터를 프로비저닝, 구성 또는 조정할 필요가 없습니다. 따라서 서버 유형을 선택하거나, 클러스터를 조정할 시점을 결정하거나, 클러스터 패킹을
최적화할 필요가 없습니다.
3. 이전에는 컨테이너를 실행하기 위해서는 컨테이너를 실행할 Instance(EC2)를 실행시켜야하였지만, AWS Fargate는 이러한 수고를 덜어 줌

## 🙏🏻 AWS 서비스 비교 🙏🏻

❓왜 Fargate 대신에 EC2를 쓸까❓왜 Fargate 대신에 Elastic Beanstalk을 쓸까❓

<img width="100" alt="Screen Shot 2023-05-20 at 12 03 52 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/f9480c88-df42-45bb-8d60-948ee0de3f80">

```
 가격
2CPU / 8GB 로 가정 하였을 때
EC2: 0.104 USD
Fargate: 0.18624 + 0.04088 ~= 0.227 USD
 성능
같은 가격이면 EC2의 성능이 더 좋은 걸 쓸 수 있다. (칩셋)
```
-> 도커를 올리니까 서비스의 안정성은 확실 함. -> 돈 많으면 편하니까 쓰면 된다.

## 🏞 AWS ECR 🏞
> Amazon Elastic Container Registry - E C R

<img width="400" alt="Screen Shot 2023-05-20 at 6 23 51 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/a80527ca-d09d-490d-95ef-9d73056c5935">

특징 📋 :
1. 쉽게 말하면 도커(이미지)를 저장하는 장소
2. Amazon Elastic Container Registry(Amazon ECR)는 안전하고 확장가능하고 신뢰할 수 있는 AWS 관리형 컨테이너 이미지 레지스트리 서비스

* RDS (DB) = 데이터를 저장하는 장소
* S3 = 사진, 이미지 등 파일을 저장하는 장소
* ECR = 도커 이미지를 저장하는 장소


## 🌟 AWS ECS 🌟 중요! 🌟
> Amazon Elastic Container Service - E C S

특징 📋 :
1. ECS(Elastic Container Service)는 AWS에서 제공하는 컨테이너 오케스트레이션서비스로 여러 어플리케이션컨테이너를 쉽고 빠르게 실행하고, 컨테이너를 적절하게 분배 및 확장 & 축소 할 수 있도록 도와주는 서비스
2. 웬만해서는 큰 서비스면 ECS 쓴다고 보면 됨.
	* 그게 아니면 EKS(쿠버네티스)나 EB(Elastic Beanstalk)쓴다고 생각하면 됨.
3. AWS EC2 와 AWS Fargate 중 원하는 환경에서 실행 가능
4. Fargate가 도커파일 하나였으면 ECS는 도커파일 여러개로 묶은 서비스라고 보면 됨.
	* 난 EC2(서버한대)로 켜서 ECS로 돌릴거야~ (얜 컴터 하나 올렸다 내렸다 해야 돼ㅠ)
	* 난 파게이트 켜서 ECS로 돌릴거야~ (도커 하나 올려줘 내려줘로 관리 가능)
	* <img width="1018" alt="Screen Shot 2023-05-20 at 6 42 20 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/86718127-c546-4271-aeb1-1cf906fa0526">
	* ECS는 하나의 그룹이다.

### ✏️ 용어 정리 ✏️
* <img width="500" alt="Screen Shot 2023-05-20 at 12 02 51 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/1a3341a2-fe41-4dec-a6d5-1bbc37486a9b">
* Task: Task 안에는 한 개 이상의 컨테이너들이 포함되어 있으며 ECS에서 컨테이너를 실행하는 최소 단위는 Task이다. - 인스턴스화
* Task Definition: 컨테이너의 이미지, CPU/메모리 리소스 할당 설정, port 매핑, volume 설정
	* Task 여러개 키려면 필요하다.
* Service: Task들의 Life cycle 을 관리하며, 오토스케일링(여러개 켜주는 것)과 로드밸런싱을 관리
* Cluster: Task가 배포되는 Container Instance 들은 논리적인 그룹
* <img width="600" alt="Screen Shot 2023-05-20 at 12 03 08 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/0fcd55aa-7aaa-4c77-b683-074c74d90d43">
* (docker compose = task)가 여러개 떠 있다고 보면 됩니당.

## 🐍 AWS Lambda 🐍
> Amazon Lambda

특징 📋 :
1. 서버 없이도 코드를 실행시킬 수 있는 서버리스 컴퓨팅 서비스
2. Fargate와 비슷하다고 생각하면 됨
	* 얘는 코드 쟤는 도커 만 올리면 실행 됨.
3. 코드를 돌리기위한 리소스를 임의로 지정할 수 있으며, 사용 리소스 x 사용 시간에 따라 과금이 된다.
	* (ex. 메모리 용량 / 코어 갯수)
4. 최대 15분 / 최대 10GB / 최대 6개의 Core
	* 겁나 큰 단점
	* 매년 올라가긴 하지만,,
5. 사용 예시
	* 비동기 처리 (이미지 썸네일 생성)
	* 예측이 불가능 한 리소스 사용 (대용량 처리 / 머신러닝)
```
최대 1000개까지 킬 수 있는데 이미지를 받는 S3에서 람다를 키고 이미지를 분류한 뒤 DB에 저장.
-> 람다로 분산처리를 한다고 알면 됨.
-> 코드뭉치 실행기다 라고 알면 됨.
-> 서버리스 서비스
람다에 올라갈 수 있는 코드 용량이 정해져(250MB?)있는데 그 이상이 넘어가면 분류를 해야한다.
```
<img width="800" alt="스크린샷 2023-05-22 오후 11 17 06" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/bd8d6ad3-1ad4-4b22-bd79-9091dbcbbb70">

### ❓왜 항상 켜져있어야 하는 EC2 / Elastic Beanstalk 대신에 가성비 있는 Lambda을 선택하지 않을까❓
```
함수를 실행시키는 서비스다보니 계속 떠있는게 아니라 계속 죽는다. 계속 warm하게 유지 시키기엔 Latency가
높아서 서버로 사용하기에는 부적절하다.
```

### ❄️ Cold Start / Warm Start 🔥
* 기본적으로 EC2와 같은 인스턴스보다는 Latency가 높다.
* Cold start : 배포 패키지의 크기와 코드 실행 시간 및 코드의 초기화 시간에 따라 새 실행 환경으로 호출을 라우팅할 때 지연 시간이 발생하는 람다 호출 시작 (겨울에 자동차 시동 걸때에서 유래 됨)
* 5분정도 warm하게 유지 -> 램에 올라가 있는 상태 -> 이땐 반응이 좀 빠름.
* 계속 warm하게 유지하기 위해선 지속적으로 사용해야 하는 방법밖엔 없음
* 웜은 단축시킬 수 있는데 콜드는 단축이 불가능 함.
	* 어쨌든 그래도 15분 뒤에 끝나서 콜드가 뜨게 됨.

1. 아무것도 실행을 하지 않았을 때 :

	<img width="400" alt="Screen Shot 2023-05-20 at 12 22 30 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/4c0dafdf-313c-4e9f-a418-22b7edb54f73">

	어느 정도는 따듯하게 유지가 된다. (짧음)

2. 아무것도 올라가 있지 않았을 때 언어별로 얼마나 오래 걸리는 지 :

	<img width="400" alt="Screen Shot 2023-05-20 at 12 22 43 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/1c17c638-dc04-41f4-bbfc-4c1785e6939d">

	도커는 상당히 오래걸리는 걸 확인 가능, 자바도 느립니당 그래서 보통 람다를 쓸 때 파이썬이나 node.js를 씁니다.

✍🏻 사용 예시 : 일반적인 서버 latency는 보통 100ms 이하지만 람다는 거기 앞에 1이 붙는다 생각하면 됨. - 응답속도 느림
1. 만약에 하루에 request가 10000개 밖에 안온다. (많이 사용하지 않는 서비스, API, 기능)
2. 병렬처리 (머신러닝이나 youtube에 영상을 올리면 1080p, 720p로 인코딩 되는 분류 상황)
3. 비동기로 돌아가는 건 다 람다라고 보면 될 것 같음.

## 🐍 AWS Lambda - Serverless 🐍
Serverless Framework : <img width="100" alt="Screen Shot 2023-05-20 at 12 25 11 AM" src="https://github.com/Kang-SeoHyun/Kang-SeoHyun/assets/77817094/a082cebd-b020-4618-84b3-4599f8a004c1">

특징 📋 :
1. AWS, Azure, GCP 등의 서버리스 서비스를 쉽게 사용할 수 있도록 도와주는 오픈소스 프레임 워크
	* 람다를 쉽게 배포할 수 있도록 도와주는 프레임 워크
2. 사용 가능 서버:
	* Node 계열 – ExpressJS, NestJS 등..
	* Java 계열 – Spring(Spring Cloud Function),
	* Python 계열 – FastAPI, Flask 등..
3. 소규모 / 이용자가 많지 않은 서비스에서 가격 효율적으로 이용 가능

serverless로 해보기 ~!
```cli 2:43분 쯤 부터, 서버리스 환경 세팅 3:04분 쯤 부터
npm install -g serverless
serverless
sls deploy #코드 넣고 이거 치면 만들어줌. AWS에서 확인 가능.
```

# 👩🏻‍💻 과제 👩🏻‍💻
## 백엔드에서 AWS 활용 🍉
1. serverless(Lambda) 사용해서 API 서버를 구축해보기
	- API 서버를 aws fargate / ECR 이용해서 띄워보기
2. SNS 예시 파이프라인 구축해보기
	- S3 presigned url 이용해서 S3에 이미지 업로드 (20개)
	- 이미지가 업로드 되면 람다 트리거를 통해 image resizing 하는 로직 실행 후 S3에 크롭된 이미지 저장
