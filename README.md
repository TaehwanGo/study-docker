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

- https://github.com/dream-ellie/docker-example

## 도커 설치

- https://www.docker.com/get-started/
  - docker desktop에서 운영체제에 맞게 다운로드
- vs code의 docker extension 설치

## 노드 프로젝트 만들기

`npm init -y`

`npm i express`

`node index.js`

## Dockerfile 만들기

- 어떤 이미지를 만들 것인지
- 어떤 것들이 필요한지 명시하는 것

```dockerfile
FROM baseImage
```

- baseImage가 기본이지만 노드는 미리 만들어둔 이미지를 이용
  - alpine : 최소한의 기능이 있는 리눅스

```Dockerfile
WORKDIR /app
```

- linux의 cd와 같은 명령어
- 이미지 파알 안에서 어떤 디렉토리의 어플리케이션을 복사해올 것인지 명시

```dockerfile
COPY package.json package-lock.json ./
```

- 도커파일에서 카피하고 가져오는 것은 레이어 시스템으로 구성되어 있기 때문에 빈번히 변경되는 파일은 마지막에 작성하는 것이 좋음
- package.json 보다 index.js가 더 자주 변경되기 때문에 index.js를 나중에 복사 해옴

```dockerfile
# RUN npm install
RUN npm ci
```

- package.json에 있는 모든 라이브러리를 설치
- npm install : 프로젝트 버전과 설치 버전이 달라질 수 있음
- npm ci : package-lock.json에 명시되어있는 것을 그대로 설치

```dockerfile
ENTRYPOINT ["node", "index.js"]
```

- node실행하고 index.js도 실행하라는 뜻

- 레이어 개념
  - 도커파일에서 위에서 부터 명령어가 있는데
  - 이 명령어 중 변경되지 않은 부분은 이미지에서도 그대로 사용하고
  - 도커파일의 변경된 부분부터 다시 만들기 때문에
  - 빈번히 변경되는 레이어일 수록 뒤에 명령어를 배치하면 도커 이미지를 만드는 시간이 단축됨

## 이미지 만들기

`docker build -f Dockerfile -t fun-docker .`

- 제일 마지막의 점(.) : build context
  - 도커에게 도커가 필요한 파일이 어디에 있는지 알려주는 것
  - 명령어를 수행하는 현재 경로를 지정
  - `-f` 옵션 : 어떤 도커파일을 사용할 것인지 명시
    - 기본적으로 `Dockerfile`이란 이름을 사용하지만 다른 이름을 지정할 수도 있음
  - `-t` 옵션 : 도커이미지에 이름을 부여, 태그 같은 개념

`docker images`

- 로컬 머신에 만들어진 도커 이미지들을 확인할 수 있음

## 도커 컨테이너 실행

- 방금 만든 이미지를 실행

`docker run -d -p 8080:8080 fun-docker`

- `-d` 옵션 : detach - background에서 도커가 동작해야 됨
  - node.js 백엔드 어플리케이션이기 때문에 백그라운드에서 계속 동작해야 되는데 아니면 터미널이 계속 기다려야 되므로 detach옵션을 줘서 터미널은 도커 동작과 관계없이 할거 하라는 뜻
- `-p` 옵션 : 포트를 지정
  - 호스트 머신의 8080과 컨테이너 머신의 8080을 연결
  - 각각의 컨테이너는 개별적인 고립된 환경에서 동작하고 있음
    - 호스트 머신의 포트와 컨테이너 머신의 포트를 연결하는 작업 필요
- 명령어 실행 : 컨테이너의 id가 프린트 됨

## 도커 컨테이너 멈추기

`docker stop fun-docker`

- docker stop :tagName

## 컨테이너 확인

`docker ps`

- 현재 실행 중인 도커 컨테이너들의 리스트
- 컨테이너 id 확인 가능

`docker logs :id`

- 컨테이너 발생한 로그들을 확인 가능

도커데스크탑(Docker Desktop) 파일을 실행해서 편리하게도 이용 가능

- 컨테이너 내부에서도 터미널 사용 가능

## 이미지 배포

- 도커 허브에 가입하고 새로운 레포를 생성

- push commands

`docker push gth1123/docker-example:tagname`

- 이미지 이름이 repository이름과 매칭이 되어야 함

`docker tag fun-docker:latest gth1123/docker-example:latest`

- 기존에 만든 도커 이름 변경

`docker images`

- 도커 이미지들 확인
  - 내가 만든 두개의 이미지 - 원본, 이름 변경한 것 - 확인 가능

`docker login`

- 푸시하기 위해선 로그인을 해야 함

`docker push gth1123/docker-example:latest`

- 도커허브 레포와 이름을 맞춘 내 로컬 도커 이미지를 push

- 도커허브의 레포에 내가 방금 푸시한 도커이미지를 확인할 수 있음 !

## 끝!

- 도커 컴포즈, 데이터 베이스, 문법 등에 대해서도 추가로 공부해보자 !
