---
title: 라즈베리파이3 초기 세팅 가이드 (2)
categories: IoT
comments: true
---

## SSH 연결
라즈베리파이는 어떤 목적으로 사용하든지 SSH로 원격으로 접속해서 사용하는게 가장 일반적이에요.
근데 모니터, 키보드, 마우스 없이 SSH로 연결하기 위한 초기세팅은 꽤나 복잡하네요. (불가능은 아니에요.)

* 기본적으로 라즈비안은 SSH 연결이 막혀있어요.
* SSH 연결 없이 라즈베리파이 IP 주소를 확인해야해요.
* 보통 라즈베리파이는 무선으로 활용하기에 원격으로 와이파이 연결을 해야해요.

제 경험상 가장 쉽고 빠른 방법은 기본적인 인터페이스(모니터, 키보드, 마우스)를 연결해서 세팅하는거에요.
초기 세팅할 때만 잠깐이면 되요. 여분이 없으면 주변 사람들한테 잠깐 빌립시다. 라즈베리파이는 HDMI와 USB 포트가 있어요.

![img](/assets/images/180618/img1.png){: width="80%"}{: .image-center}

디스플레이 연결후, 전원을 연결하면 위와 같은 화면을 볼 수 있는데요.

![img](/assets/images/180618/img2.png){: width="80%"}{: .image-center}

![img](/assets/images/180618/img3.png){: width="80%"}{: .image-center}

Preferences -> Raspberry Pi Configuration 에서 SSH 연결을 허용해 줍시다.

라즈베리파이는 기본적으로 User: pi / PW: raspberry 라는 공통 계정 정보를 갖고 있기 때문에, SSH 허용 후에는 비밀번호를 변경하여 보안에 신경을 써주는게 좋아요.

![img](/assets/images/180618/img4.png){: width="80%"}{: .image-center}

디스플레이가 연결되었다면, 와이파이 연결 및 IP주소를 확인하는 것은 참 쉽죠? 이제 ssh로 그냥 접속하면 되겠네요. scp로 필요한 파일들은 넘겨줍시다.

## 기타 이슈 사항

### 가상 키보드

혹시라도 키보드가 없으신 분들은 임시로 쓸 수 있는 가상 키보드를 쓸 수 있어요. 급할 때, 간단한 입력정도는 써볼 수 있겠네요.
```
$ sudo apt-get install matchbox-keyboard
$ sudo reboot
```
위와 같이 간단하게 설치할 수 있어요. 설치후, 리부팅까지 해줘야 해요.

![img](/assets/images/180618/img5.png){: width="80%"}{: .image-center}

![img](/assets/images/180618/img6.png){: width="80%"}{: .image-center}

위와 같이 Preference -> Main Menu Editor에서 Accessories 항목에 키보드가 생긴 것을 확인할 수 있네요.

![img](/assets/images/180618/img7.png){: width="80%"}{: .image-center}

간단하게 쓰기에는 나쁘지 않네요.

### RSA 공유키 충돌 문제

저는 라즈베리파이 물리적인 세팅이 되어있는 상태에서 마이크로 SD카드만 바꿔가면서 여러 개의 라즈베리파이를 세팅했어요.
이러다보니 라즈베리파이에서 특정 IP에 연결 후 공유키를 교환한 상태에서 SD카드를 바꿔버리니 특정 IP에 대한 시스템이 바뀌어버린 상황이에요.
Man in the Middle Attack에 대해서 경고를 하네요.

![img](/assets/images/180618/img8.png){: width="80%"}{: .image-center}

하지만 이거는 해킹 사고는 아니기에 그냥 공유키를 초기화 시켜줍니다.
```
$ ssh-keygen -R 192.168.0.19
```
