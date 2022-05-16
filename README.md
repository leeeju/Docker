# Docker 사용법
---

### - 환경구성 : Windows10, Docker Desktop

![도커](https://user-images.githubusercontent.com/84003327/160781878-d32e36cd-6ab0-4b0e-94d0-3ba0e3cbc5de.PNG)

- Docker(도커)란?

도커는 컨테이너 기반의 ```오픈소스``` 가상화 플랫폼이다 

```컨테이너라``` 생각하면 하나 하나의 물건(컨텐츠, OS, 운용환경) 등을 담을 수 있는 그릇이라고 생각하면 쉽게 생각 할 수 있다, 각각의 가상환경 속에서 내가 원하는 별도의 운영환경을 구성하고 프로젝트를 빌드 할 수 있는 하나의 독립공간을 만드는것이라 할 수 있다 더 쉽게 생가하면 버츄얼 박스(Oracle VM VirtualBox)를 사용해서 별도의 가상 환경을 만드는 것에 비해서 매우 가볍고 컴팩트 하게 만들어 생성, 삭제가 용이하다고 할 수 있다 

VirtualBox와 같은 가상머신은 호스트서버 OS위에 게스트 OS 전체를 가상화하여 사용하는 방식입니다. 이 방식은 여러가지 OS를 가상화(리눅스에서 윈도우를 돌린다던가) 할 수 있고 비교적 사용법이 간단하지만 ```무겁고 느려서``` 듀얼부팅으로 단독 셋팅을 하지 않는한 여타 운영환경에선 사용하기 불편하다

![도커2](https://user-images.githubusercontent.com/84003327/160781909-4da06926-d8e8-4f9c-b63d-1c0909d5319f.PNG)


서버관리에서 이야기하는 컨테이너도 이와 비슷한데 다양한 프로그램, 실행환경을 컨테이너로 추상화하고 동일한 인터페이스를 제공하여 프로그램의 배포 및 관리를 단순하게 해준다. 백엔드 프로그램, 데이터베이스 서버, 메시지 큐등 어떤 프로그램도 컨테이너로 추상화할 수 있고 조립PC, AWS, Azure, Google cloud등 어디에서든 실행할 수 있다

이렇게 탄생한 방법이 프로세스 격리 기술이다, 리눅스에서는 이 방식을 리눅스 컨테이너라고 하고 단순히 프로세스를 격리시키기 때문에 가볍고 빠르게 동작한다 CPU나 메모리는 딱 프로세스가 필요한 만큼만 추가로 사용하고 성능적으로도 없기 때문에 다양한 개발을 하거나 할 때 많이 사용하게 된다   


---
도커 사용법
---
- 설치를 먼저 했다고 가정함.

![프롬프트](https://user-images.githubusercontent.com/84003327/160783977-6f034a6d-f523-4d68-ad69-3497669045fe.PNG)


먼저 윈도우 프롬프트(CMD)를 실행해준다 

```bash
docker run -d -p 80:80 docker/getting-started
```
명령어를 사용해 연습용 틀을 만들어 준다, 

```docker```[실행툴 이름], ```run```[실행 명령어], ```-d``` [분리 모드(백그라운드에서)에서 컨테이너 실행] , ```-p``` 80:80 [호스트의 포트 80을 컨테이너의 포트 80에 매핑(변경가능)], ```docker/getting-started```[사용할 이미지 선택]


위 명령어를 입력해주면 다음과 같이 가상환경이 셋팅되는것을 볼 수 있다.

![todtjd](https://user-images.githubusercontent.com/84003327/160789503-64b28d69-3d17-4425-811b-f803d78b273e.PNG)


그럼 도커 시스템에 가상환경이 셋팅 된것을 볼 수 있다

![aaaa](https://user-images.githubusercontent.com/84003327/160789551-441aba38-69b6-48b5-aaeb-514c4865f757.PNG)

더 자세한 도커 생성 명령어는 다음과 같다.

|옵션|내용|
|----|---|
|-d  | detached mode 흔히 말하는 백그라운드 모드|
|-p  | 호스트와 컨테이너의 포트를 연결 (포워딩)|
|-v | 호스트와 컨테이너의 디렉토리를 연결 (마운트)|
|-e  |컨테이너 내에서 사용할 환경변수 설정|
|–name | 컨테이너 이름 설정|
|–rm  |프로세스 종료시 컨테이너 자동 제거|
|-it  | 	-i와 -t를 동시에 사용한 것으로 터미널 입력을 위한 옵션|
|–link  | 컨테이너 연결 [컨테이너명:별칭]|


### docker ps 명령어

```bash
docker ps
```

명령어를 사용하면 현재 사용중인 프로세스의 상태를 보여주게 된다 

![aaa](https://user-images.githubusercontent.com/84003327/168518735-962b778d-f8dc-46e9-b880-f2525e27b557.PNG)


---
## ubuntu 16.04 container 만들기 

아래 명령어를 사용해서 우분트 컨테이너를 만들어 보자.

```bash
docker run --rm -it ubuntu:18.04 /bin/bash
```

---

위 명령어를 사용하게 되면 ```--rm``` 명령어가 들어가 있기 때문에 1회용 우분트가 만들어 지는것을 볼 수 있을것이다 생성된 우분투를 도커를 종료(exit 명령어)함과 동시에 삭제 되는것을 볼 수 있다

우분트가 생성되었으면 사용자가 ID가 root@6ffef1ec40c0로 변경된것을 볼 수 있으며  ```ls``` 를 사용해서 생성된 파일을 점검하고 ```cat /etc/issue``` 를 사용해서 우분트의 버전을 확인해 보자 

![aasd](https://user-images.githubusercontent.com/84003327/160794052-cd65445b-df0f-4e8b-8168-694fd352307e.PNG)

---

## docker pytorch 환경 만들기

도커를 사용하는데 있어서 주된 용도로 사용되는 것이 머신러닝 및 딥러닝이며 pytorch, TensorFlow가 주로 사용된다,
그중에서 난이도가 비교적 쉬운 pytorch를 사용해서 도커 컨테이너를 만들어 보자.

```bash
docker run -it pytorch/pytorch
```

를 사용해서 pytorch의 이미지를 다운로드 해주자 

![토치](https://user-images.githubusercontent.com/84003327/168543315-f9dc6065-53c3-40d6-9a00-318a444cf999.PNG)


위 사진과 같이 도커에 pytorch의 이미지가 다운로드 되고 있으며 다운이 완료 되면 사용 할 수 있다
다운이 완료됬는지 확인 겸 컨테이너의 ```ID 생성```이 이루어 졌는지 확인을 위한 명령어를 입력해 보자 

```bash
docker images
```

![id](https://user-images.githubusercontent.com/84003327/168545107-cea28f83-2bd5-40b5-ba5d-687dbcebbdf4.PNG)

아이디를 확인했다면 ```exit``` 를 입력해서 컨테이너에서 빠져 나와 다시 컨테이너 접속 명령어위에서 확인한 컨테이너 이미지ID를 사용해서 연결이 되는지 확인해본다.

```bash
docker run -it ca04e7f7c8e5
```

![캡처](https://user-images.githubusercontent.com/84003327/168545920-6ee59a9c-6228-43d0-b1de-f55f0dd2eff2.PNG)







