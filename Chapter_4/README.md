# Chapter04.데이터 링크 계층

- [데이터 링크 계층의 역할과 이더넷](#%EF%B8%8F-데이터-링크-계층의-역할과-이더넷)
- [MAC 주소의 구조](#%EF%B8%8F-MAC-주소의-구조)
- [스위치 구조](#%EF%B8%8F-스위치-구조)
- [데이터가 케이블에서 충돌하지 않는 구조](#%EF%B8%8F-데이터가-케이블에서-충돌하지-않는-구조)

<br>

## 💡 데이터 링크 계층의 역할과 이더넷
> 데이터 링크 계층은 네트워크 장비 간에 신호를 주고 받는 규칙을 정하는 계층으로, 랜에서 데이터를 정상적으로 주고 받기 위해 필요한 계층이다. 이 규칙들 중 일반적으로 상용되는 규칙을 이더넷(Ethernet)이라 부른다.


### 추가적인 내용 기술
- 허브에 연결된 여러 대의 PC가 동시에 데이터를 보내면 데이터들이 충돌될 수 있는데, 이더넷이 여러대의 PC가 동시에 데이터를 전송해도 충돌이 발생하지 않도록 제어한다.
- 이 때 이더넷은 CSMA/CD 방식으로 데이터를 송신하는 시점을 제어하는데, 여기서 CSMA란 데이터를 보내려는 목적지 PC에 데이터가 흐르고 있는지 파악하고 흐르지 않는다면 데이터를 전송하는 규칙이다. 또한 충돌이 발생하는지 확인하는 규칙을 CD라고 한다.
- 하지만, 현재는 CSMA/CD 방식이 비효율적이다는 이유로 사용하지 않고, 스위치라는 네트워크 장비를 이용한다.


<br>

## 💡 MAC 주소의 구조
> MAC 주소는 랜카드를 제조할 때 정해지기 때문에 물리 주소라고도 불리며, 전 세계에서 고유한 번호가 할당되어 있다. MAC 주소는 48비트 숫자로 구성되어 있는데 앞 쪽 24비트는 랜 카드를 만든 제조사 번호이고, 뒤 쪽 24비트는 제조사가 랜 카드에 붙인 일련 번호의 조합이다.


### 추가적인 내용 기술
- OSI 모델에서는 L6 계층에 해당하는 데이터 링크 계층, TCT/IP 모델에서는 네트워크 계층에서 이더넷 헤드와 트레일러를 붙이는데, 이 이더넷 헤드에는 목적지의 MAC주소(6바이트) + 목적지 MAC주소(6바이트) + 유형(2바이트)"로 구성되어 있다.![](https://images.velog.io/images/jewon119/post/be58bee8-bb3a-4dbe-a980-f7959291cb0e/image.png)
- 이 계층에서 캡슐화할 때, 붙는 꼬리 부분으로 트레일러 또는 FCS(Frame Check Sequence)라고도 하는데, 이는 데이터 전송 도중 오류가 발생하는지 확인하는 용도로 사용한다.
- 즉 송신측 PC에서는 데이터 링크 계층에서 이더넷 헤드와 트레일러를 캡슐화하여 물리 계층으로 보내고, 수신측 PC에서는 물리 계층에서 전달된 프레임의 헤드와 트레일러를 제거해 도착지 MAC주소가 자신의 MAC주소와 일치한지 확인 후 상위 계층으로 올려보낸다.

<br>

## 💡 스위치 구조
> 스위치는 데이터 링크 계층에서 동작하는 네트워크 장비이며, 레이어 2스위치 또는 스위칭 허브(허브와 비슷하게 생김)라 불린다. 스위치는 내부에 MAC 주소 테이블(MAC Address Table)이 존재하고, 여기서 스위치의 port번호와 해당 port에 연결되어 있는 PC의 MAC 주소가 매핑되는 DB이다. 이에 브릿지 테이블이라고도 불린다.


### 추가적인 내용 기술
- 송신측 MAC주소와 수신측 MAC주소가 포함된 프레임이란 데이터를 송신측 PC에서 전송하면, 스위치의 MAC 주소 테이블에 송신측 MAC 주소와 해당 포트를 매핑시킨다. 이를 과정을 MAC 주소 학습 기능이라 부른다.
- 또한 MAC 주소 테이블에 수신측 MAC주소와 port가 매핑되어있다면 다른 연결된 port로는 데이터가 전달되지 않는다.
- 다만, MAC 주소 테이블에 프레임의 저장된 수신측 MAC주소와 port번호가 매핑되있지 않다면 모든 연결된 port의 PC로 데이터가 전달된다. 이를 플러딩(flooding, 홍수)이라 부른다.

<br>

## 💡 데이터가 케이블에서 충돌하지 않는 구조
> 케이블의 구조적 측면에 있어 데이터의 송수신을 동시에 하는 "전이중 통신 방식"과 회선 하나로 송신과 수신을 번갈아가하면 "반이중 통신 방식"이 있다. 이에 전이중 통신 방식을 데이터를 동시에 전송해도 충돌이 발생하지 않지만, 반이중 통신 방식은 데이터를 동시에 전송하면 충돌이 발생한다.


### 추가적인 내용 기술
- PC 2대를 랜케이블(크로스 케이블)로 직접 연결하면 전이중 방식으로 통신하지만, 허브를 통해 연결하면 반이중 방식으로 통신하기 때문에 충돌할 수 있다.
- 이에 비해, 스위치는 전이중 방식으로 통신하기 때문에 동시에 데이터를 전송해도 충돌이 일어나지 않는다.
- 뿐만 아니라, 충돌이 발생할 때 영향을 미치는 범위를 충돌 도메인(collision domain)이라 하는데, 허브 방식은 한 곳에서 충돌이 발생해도 연결된 모든 PC에 영향을 미친다.
- 하지만, 스위치는 연결된 모든 PC에서 충돌에 대한 영향을 미치지 않고, 충돌 범위가 작기 때문에 통신 효율이 높다.
