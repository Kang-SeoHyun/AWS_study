# 🫧 AWS 🫧

```txt
인프라 관련 요소들
- AWS API Gateway
- AWS S3
- AWS ELB
- AWS CloudFront
- AWS Secret Manager
```
### 🥊 On-premise **vs** Cloud Computing 🥊
```
On-premise: 온프레미스란 기업의 서버를 클라우드 같은 원격 환경에서
운영하는 방식이 아닌, 자체적으로 보유한 전산실 서버에 직접 설치해
운영하는 방식
Cloud Computing: 클라우드 컴퓨팅은 인터넷을 통하여 데이터를 저장하거나
데이터베이스, 서버, 네트워킹, 소프트웨어와같은 도구, 애플리케이션등 다양한
서비스를 제공하는 방식
ex) AWS, GCP(google cloud blabla)
```

### ❓Cloud Computing을 쓰는 이유
1. 카프카 클러스터 규모
2. 편리한 서버의 확장
3. 등등

### ❓근데 왜 AWS를 쓸까
이미 우리나라는 AWS를 사용해서 구축한 경우가 많아서라고 생각함.
대신 구글 클라우드는 머신러닝에 차별화된 서비스가 많긴 함.

## 🏠 AWS VPC 🏠
-> Virtua Private Cloud

* 가상 네트워크 서비스로 퍼블릭 네트워크와 프라이빗 네트워크를 분리하고
모니터링할 수 있도록 해주는 서비스
* 네트워크 구성과 관련된 사실상 모든 기능을 담당하며, 자체 데이터
센터에서 운영하는 기존 네트워크와 매우 유사한 형태

 <img width="700" alt="Screen Shot 2023-05-05 at 1 56 22 AM" src="https://user-images.githubusercontent.com/77817094/236273250-f6900781-d818-4f24-894e-93e6081a482d.png">

```
쉽게 말해 vpc라는 건 집을 짓는다고 생각하면 됨.
엄마 방도 필요하고, 아빠 방도 필요하고, 내 방도 필요하고,, -> subnet
vpc안에는 많은 subnet이 존재할 수 있습니다.
인터넷과 vpc가 소통할 수 있는 창구는 인터넷 게이트웨이(현관문)이다.
라우터(라우터를 기능이라 표현했음)를 통해 이 집의 구조를 알 수 있다. -> routing table을 통해
프라이빗 서브넷은 인터넷 연결이 안되고, 퍼블릭서브넷은 인터넷 연결이 됩니다.
```

😓 사실 맨 처음 서버 인프라 세팅할 때 만지는 경우 이외에는 만질 일 없습니당.
> 근데 상당히 중요하니까 꼭 알아야 함.
> 큰 회사에서는 데브옵스가 많이 건듬.


## 🚪 AWS API Gateway 🚪
-> 맨 처음에 user의 request를 받게 되는 곳.
-> 외부 사용자가 내부 서비스로 접근하는 가장 첫 단계다.
- 어떤 규모에서든 개발자가 API를 손쉽게 생성, 게시, 유지 관리, 모니터링 및
보안 유지할 수 있도록 하는 완전관리형 서비스
- 서버의 “대문”과 같은 역할
- API Gateway가 할 수 있는 것들:
    - ex) 트래픽 관리 (제한), CORS 지원, 권한 부여 및 액세스 제어, 제한, 모니터링
    API 버전 관리, 인증관련 등…

## 🧴 AWS ELB 🧴
-> Elastic Load Balancing
* 다수의 컴퓨팅 리소스(EC2, Lambda, 등)를 부하 분산시켜주는 아주 중요한 서비스
* 총 3가지 종류의 Balancer가 있으며, Application Load Balancer가 일반적인 상황에서 가장 많이 쓰임.
* <img width="700" alt="Screen Shot 2023-05-05 at 1 52 55 AM" src="https://user-images.githubusercontent.com/77817094/236272482-4431a31d-3b53-4ccb-8d6f-3ce420f61d60.png">
* ALB: Application Load Balancer
* NLB: Network Load Balancer
* GWLB: Gateway Load Balancer

<img width="600" alt="Screen Shot 2023-05-05 at 2 05 19 AM" src="https://user-images.githubusercontent.com/77817094/236275574-d99f530b-e4f4-4a7c-8003-2960f463cfe7.png">

-> 아마 라운드로빈 알고리즘을 통해 부하분산 처리함.
```
ALB는 라운드 로빈 방식의 로드 밸런싱 알고리즘을 사용하여 트래픽을 분산합니다. 이 방식은 서버 간 부하를 고르게 분산시키는 간단하고 효율적인 방법입니다. ALB는 서버 그룹에 대해 트래픽 로드 밸런싱을 수행하며, 각 서버가 동일한 양의 트래픽을 처리할 수 있도록 보장합니다.라운드 로빈 알고리즘은 서버 그룹의 모든 서버에 대해 순서대로 요청을 분배합니다. 즉, 첫 번째 요청은 첫 번째 서버에게 보내지고, 두 번째 요청은 두 번째 서버에게 보내지고, 세 번째 요청은 세 번째 서버에게 보내지는 식입니다. 이러한 방식으로 요청이 순서대로 분배되므로, 각 서버는 고르게 부하가 분산되게 됩니다.ALB는 라운드 로빈 방식 외에도 가중치 기반 로드 밸런싱, 세션 지속성 및 최소 연결 수를 기반으로 하는 로드 밸런싱 알고리즘을 지원합니다. 이러한 다양한 로드 밸런싱 알고리즘을 사용하여 ALB는 서버 그룹의 트래픽을 효율적으로 분산시키며, 안정적인 웹 애플리케이션을 제공합니다.
```

## 🏞 AWS S3 🏞
-> Simple Storage Service (S3)

* 가장 오래된 AWS 서비스중 하나로 엄청난 내구성과 가용성을 자랑하며 이미지,동영상,
오디오 파일과 같은 정적파일들을 용이하게 관리하도록 돕는 스토리지 서비스
* 단순 파일의 저장 공간을 넘어서서 데이터를 저장하는 스토리지 플랫폼
    * 데이터 처리: S3에 저장되는 Trigger를 이용해 람다를 실행 시킬 수도 있음
    * 로그: AWS 안에서 이뤄지는 대부분의 로그는 S3에 저장 됨
    * 쿼리 지원: AWS Athena를 통하여 S3에 저장된 파일을 쿼리할 수도 있음
    * 호스팅: Single Page Application (React)를 호스트 할 수도 있음


### 💪🏽 **S3는 Trigger 이랑 Presigned URL을 지원함.**
Trigger
-> 어떤 트리거가 있을 때, 람다로 넘어가서 원하는 거 얻을 수 있음.
--> ex) 과한 용량의 파일을 자동 리사이징해서 돌려줌.
<img width="400" alt="Screen Shot 2023-05-05 at 2 19 27 AM" src="https://user-images.githubusercontent.com/77817094/236280073-48d3f84a-2277-45e4-a73d-6256797c7f32.png">

Presigned URL
-> 이미지 받는 새로운 방법
<img width="400" alt="Screen Shot 2023-05-05 at 2 22 33 AM" src="https://user-images.githubusercontent.com/77817094/236281173-5ca71beb-b737-4b41-a639-40d337ad8606.png">

## ☁️ AWS CloudFront ☁️

* 전 세계에 있는 AWS 엣지 로케이션을 통하여 CDN 서비스를 제공 함
* 현재 48개국 90개가 넘는 도시에서 410개가 넘는 접속 지점 (엣지 로케이션 400개 이상, 리전별 중간 티어 캐시 13개)로 구성된 글로벌 네트워크를 지원
* <img width="726" alt="Screen Shot 2023-05-05 at 2 31 18 AM" src="https://user-images.githubusercontent.com/77817094/236283057-53b3e08b-9022-43a1-af94-86952bb1b98e.png">
* 속도는 높이고, 가격은 내릴 수 있다. (서버 부하는 줄일 수 있음 - S3쓰니까)
    * S3가 훨씬 더 비싸다.
    * 이미지를 사용한다면 CloudFront를 거의 무조건 사용해야한다~
* cloudfront(global service)를 쓰려면 S3(global service)를 사용해야하고 버킷까지 만들어야합니다.
    * region에 대한 제약이 없다.
    * region 구분이 없다고 알아두면 됨.


### ❓ EC2 ( Elastic Compute Cloud) 란
EC2서비스는 AWS에서 비용, 성능, 용량면에서 탄력적인 클라우드 컴퓨터를 제공하는 서비스라고 할 수 있다.
```
아마존 웹 서비스(AWS)에서 제공하는 클라우드 컴퓨팅 서비스
클라우드 컴퓨팅은 인터넷(클라우드)을 통해 서버, 스토리지, 데이터베이스 등의 컴퓨팅 서비스를 제공 -> AWS에서 원격으로 제어할 수 있는 가상의 컴퓨터를 한 대 빌리는 것
후불제 PC방과 같이 사용한 만큼 비용을 지불하기 때문에 탄력적인 이라는 의미의 Elastic이라는 단어가 붙어있다.
Elastic은 비용적인 부분 뿐만이 아니라 필요에 따라 성능, 용량을 자유롭게 조절할 수 있다는 의미도 가지고 있다
```

## 🌝 AWS Secret Manager / Parameter Store 🌝
* 데이터베이스 보안 인증 정보 및 API 키와 같은 보안 정보를 안전하게
암호화하고 중앙 집중식으로 감사할 수 있도록 도와주는 서비스
* .env 파일을 서버 별로 따로 관리하기 보다는 한 곳에서 집중적으로 관리 - 환경변수 파일
* DB 정보와 같은 민감한 정보는 암호화가 지원이 되는 Secret Manager에
저장
* 간단한 정보 (ex. Endpoint)는 Parameter Store에 저장하여 사용
