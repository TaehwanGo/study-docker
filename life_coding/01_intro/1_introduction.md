# 생활 코딩 Docker

## 1. 수업 소개

- 도커의 이용자가 되기 위한 최소한의 개념과 원리

## 2. 설치

- 리눅스 운영체제 위에서 돌아가는 앱들이다

  - 리눅스, 맥이라면 가상 머신에 운영체제를 깔아서 도커를 사용가능
    - 도커가 알아서 가상머신을 만들고 리눅스를 설치해줌
  - 사용하는 운영체제가 리눅스라면 성능저하가 없음
  - 만약 운영체제가 리눅스가 아니라면 성능저하를 약간 감수해야 함(그럼에도 불구하고 편의성이 매우 좋음)

- docker 공식 홈페이지에서 설치 가능

  - 리눅스 : 리눅스 설치 가이드
  - 윈도우나 맥 : 도커 데스크탑 for 운영체제

- 도커 데스크톱, 대쉬보드 실행으로 가능

- 도커는 주로 명령어로 실행을 함
  - docker images : 이미지 리스트 확인

## 3. 이미지 pull

- pull : docker hub에서 image 찾아서 컴퓨터에 다운받는 것
- run : 이미지를 실행하는 것(image -> container)

#### 이미지를 다운 받는 방법

- docker hub에서 여러 이미지들을 다운 가능

#### 실습 : 아차피 웹 서버 이미지 다운

- docker에서 httpd로 검색
- docker pull httpd

#### 도커 관련 명령어들

- https://docs.docker.com/reference/ 에서 Command-line reference

## 4. 컨테이너 run

docker run [OPTIONS] :imageName [COMMAND] [ARG...]

- 이미지 뒤쪽에 옵셔널한 명령어는 컨테이너 안에서 적용할 옵션들

`docker run httpd`

`docker ps`

- docker ps -a
  - stop 된 것들도 볼 수 있음

하나의 이미지는 여러개의 컨테이너를 만들 수 있음

`docker run --name ws2 httpd`

실행 중인 도커를 끄고 싶다면

- docker stop [OPTIONS] CONTAINER [CONTAINER...]

중지했던 컨테이너를 다시 실행하고 싶다면

- `docker start ws2`

도커의 로그들을 보고 싶다면

- `docker logs ws2`
  - `docker logs -f ws2` : watch mode

컨테이너를 삭제할 땐

- `docker stop ws2`
- `docker rm ws`
  - 현재 실행 중인 컨테이너는 지울 수 없음

이미지를 삭제할 때

- `docker rmi [OPTIONS] IMAGE [IMAGE...]

## 5. 네트워크

`docker run --name ws2 -p 8080:80 httpd`

- 이름 설정을 먼저 해줘야 함
- host의 8080과 container의 80포트를 연결 : 포트포워딩(port forwarding)

## 6. 명령어 실행

#### Docker desktop

- docker desktop에서 특정 컨테이너를 클릭하고 cli 클릭 -> 커맨드 창
- `pwd` : 현재 디렉토리 경로
- `ls -al` : 현지 디렉토리에 위치한 파일들

#### CLI로 명령어 창 열기

docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

- `docker exec ws2 pwd`

  - HOST에서 Container의 명령을 실행

- `docker exec -it ws2 /bin/sh`
  - Container의 터미널을 실행
  - i : Keep STDIN open even if not attached
  - t : Allocate a pseudo-TTY
  - 운영체제의 이해가 필요
    - 간단히 : 터미널과 컨테이너를 지속적으로 연결할 땐 -it를 쓴다고 알고 넘어가자
- exit : HOST로 돌아올 수 있음

- `docker exec -it ws2 /bin/bash`
  - sh보다 bash가 기능이 더 많고 경로까지 표시되서 좋음

#### 아파치의 index.html을 수정하고 싶은 경우

- 도커 허브 공식 httpd 문서 참고
  - https://hub.docker.com/_/httpd
  - /usr/local/apache2/htdocs/

## 7. 호스트와 파일 시스템의 연결

- 호스트에서 파일을 수정하면 컨테이너에 자동으로 반영되도록
  - 만약 컨테이너가 없어지더라도 호스트에는 남아있게

`docker run -p 8888:80 -v ~/projects/study-docker/life_coding/01_intro:/usr/local/apache2/htdocs/ httpd`
