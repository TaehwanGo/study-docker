# 도커

## 참고

- 드림코딩 엘리님 유튜브 : https://youtu.be/LXJhA3VWXFA

## 도커란?

- 어플리케이션을 패키징할 수 있는 툴
  - Application, System Tools, Dependencies를 하나로 묶어서
  - 다른 서버 or 다른 PC 등 그 어느곳에서도 쉽게 배포하고 안정적으로 구동할 수 있게 도와주는 툴
- e.g., Node.js
  - 웹앱이 발전하면서 => 소스파일(app.js) + npm + node.js + dependencies, configs(환경 변수 등) 등이 필요
  - 노드 버전이 내 PC와 서버의 버전이 맞지 않아서 동작이 되지 않을 수도 있음
- 컨테이너 : 소프트웨어 유닛
  - 어플리케이션 : app.js
  - 어플리케이션을 동작하기 위한 것들이 포함
    - node.js
    - npm
    - configuration
    - dependencies
    - assets : images
- 도커 컨테이너를 사용하면 어플리케이션 구동을 위한 런타임환경에 필요한 모든 것들을 구성, 어떤 PC에서든 동일하게 구동 가능

## VM과 도커의 차이

### VM

- 하드웨어 `Infrastructure` 위에 `Hypervisor software`(VM ware, VirtualBox)를 이용해서 각각의 가상의 머신을 만들 수 있음
  - Infrastructure -> Hypervisor -> Virtual Machine
    - Virtual Machine
      - App2, Libraries, Binaries, Guest OS
      - App1, Libraries, Binaries, Guest OS
      - App3, Libraries, Binaries, Guest OS
- VM은 운영체제를 포함하고 있기 때문에 굉장히 무거움
  - 느리고 리소스를 많이 필요로 함

### 컨테이너

- VM에서 경량화된 컨셉
  - Infrastructure -> Host OS -> Container Engine -> Container
    - Container
      - App1, Libraries, Binaries
      - App2, Libraries, Binaries
      - App3, Libraries, Binaries
- OS를 설치하지 않고 Container Engine이 설치된 Host OS를 공유
  - 운영체제와 커널에 대해서 공부를 깊이 해야되므로 자세한 부분은 스킵
- `컨테이너`가 동작하기 위해선 `컨테이너 엔진`이 필요하고
  - 컨테이너 엔진은 Host OS에 접근해서 필요한 것들을 처리
  - `컨테이너 엔진` 중 가장 많이 사용되는 것이 `도커`

## 도커의 3대 구성요소!(순서)

- 도커의 큰 그림
  - 컨테이너를 만들고
  - 배포하고
  - 구동한다

### Building Containers

- 컨테이너를 만들기 위해 필요한 3가지
  - 도커파일(Dockerfile)
  - 이미지(Image) <- 도커 파일
  - 컨테이너 <- 이미지

#### 도커파일(Dockerfile)

- 컨테이너를 어떻게 만들어야 되는지에 대한 설명서
- Copy files
  - 어플리케이션을 구동하기 위한 파일들에 대한 명시
- Install dependencies
  - 외부 dependencies에 대한 명시
- Set environment variables
  - 필요한 환경 변수에 대한 설정
- Run setup scripts
  - 어떻게 구동해야되는지에 대한 스크립트

#### 이미지(Image)

- 어플리케이션을 실행하는데 필요한 모든 세팅들

  - 코드(app.js)
  - 런타임 환경(node.js)
  - Assets
  - Dependencies
  - Configuration
  - Dockerfile

- 실행중인 어플리케이션을 스냅샷해서 이미지로 만들어두는 것이라고 생각하면 됨
- 이렇게 만들어진 이미지는 변경이 불가능한 상태가 됨

#### 컨테이너(Container)

- Sandbox 처럼
- 우리가 잘 캡쳐해둔 어플리케이션 이미지를 고립된 환경(개별적인 파일 시스템 안)에서 실행할 수 있는 것
- 컨테이너 안에서 어플리케이션이 동작한다
- 객체지향에 비유해서 설명
  - 이미지(Image) : 클래스
    - 동작하고 있는 어플리케이션을 스냅샷해서 템플릿 형태로 이미지를 만들어 둠
  - 컨테이너(Container) : 클래스의 인스턴스
    - 이미지를 이용해서 실제로 어플리케이션이 동작하는 컨테이너를 만들 수 있음
- 이미지는 불변의 상태
- 컨테이너는 개별적으로 수정이 가능한 상태
- 각각의 컨테이너에서 수정된 파일들이 있어도 이미지엔 영향을 주지 않음

## 도커 이미지 배포하는 과정(Shipping Containers)

- 컨테이너 배포(이미지를 공유)
- 깃허브 처럼
- `Image`(~= git)를 `Container Registry`(~= github)에 push
- 필요한 서버(또는 PC)에서 내가 원하는 이미지를 가지고 옴(~= git clone)
- 가져온 이미지를 그대로 실행하면 됨
- 이미지를 실행하기 위해선 도커같은 컨테이너 엔진이 설치가 되어야 함

#### 이미지를 공유할 수 있는 Container Registry

- Public, Private
  - Public : docker hub, RED HAT, Github packages
    - docker hub가 더 많이 사용되고 있음(github packages는 나온지 얼마 안됨)
  - Private
    - AWS, Google Cloud, Microsoft Azure

## 마지막 총 정리

- 도커를 사용하기 위해서 도커 설치
  - 내 PC에 도커를 설치
  - 내가 사용할 PC에 도커를 설치
- 어플리케이션 구동하는데 필요한 도커파일
- 도커파일을 이용해서 어플리케이션을 스냅샷할 수 있는 이미지를 만들음
- 이미지를 컨테이너 레지스트리(도커 허브)에 올린 다음
- 서버에서 컨테이너 레지스트리에 있는 이미지를 다운로드 받아서
- 컨테이너를 실행

## 실습 프로젝트 소개

## 도커 설치

## 노드 프로젝트 만들기

## Dockerfile 만들기

## 이미지 만들기

## 도커 컨테이너 실행

## 컨테이너 확인

## 이미지 배포

## 끝!
