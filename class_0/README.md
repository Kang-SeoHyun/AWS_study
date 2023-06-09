# ✏️사전 과제✏️

## ❓작업을 비동기로 처리해야하는 상황 3가지
> 유튜브를 예로 들면 좋아요, 알림/푸쉬 서비스, 영상 업로드, 영상 자막처리 등에 비동기 처리 방식이 사용된다.

* 웹 API 호출
	* 엄밀히 따지면 백엔드 레벨의 비동기 처리는 아님
* 대용량 데이터 처리
* 즉각적인 처리가 필요하지 않은 경우
* 100ms (강사님 주관적 경험) 이상 걸리는 작업 혹은 병렬 처리가 필요한 경우
	* 서버리스 람다 등 aws 인프라 사용 (차차)

## ❓매일 다른 시간 평소의 3배에 달하는 트래픽이 몰리는 SNS 서비스가 있습니다. 어떤 형식으로 아키텍쳐를 구성하면 서버를 더 안정적으로 운영할 수 있을까요?
> 서버는 빨리 열면 되는데 DB는 수평적으로 스케일링하는 분산화가 어려워서 서버보다 디비가 더 터지기 쉽다. 그래서 redis가 디게 중요함.

* 메인 서버의 Load Balancer / Auto Scaling
* 이용자 / 게시물 캐싱 처리를 위한 Redis
* 이미지 캐싱을 위한 CloudFront - Contents Delivery Network - CDN (이따)
	* 위 세개는 사실 무조건 백엔드 기본으로 가져가게 된다.
* 이미지 처리 (ex. 크롭, 업로드, 영상 인코딩 등)를 위한 서버리스 함수와 메세지 큐
* 알림 서비스를 위한 서버리스 함수와 메세지 큐

### **틈새** Redis 공부❗

1. Redis는 휘발성 데이터 저장할 때 쓰임.
	1.1 TTL(?)이라고 어느 시간 이상 지나면 data(key) 날려버림.
	1.2 TTL은 서비스에 따라서 다름. (뭐 변화 많은 sns는 짧고, 적은 직방은 길고)
2. Redis 캐싱 어떻게 진행되나?
		![image](https://user-images.githubusercontent.com/77817094/236193716-da21079a-b7c0-426f-a9f8-6f990ebc6f2c.png)
3. Redis를 두세개 더 켜서 DB부활을 줄일 수 있다면 키면 좋음.
4. DB는 터지는 경우 있는데 Redis는 유연성을 가지고 있어서 터질 가능성이 적다.
	4.1 글고 터져도 백엔드는 DB접근하면 되기 때문에 ㄱㅊ다. 복구하면 됨.
