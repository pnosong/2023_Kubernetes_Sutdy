# 2023_Kubernetes_Study

#### 게시판 만들기

- 급하게 작성하느라 아직 미흡한 부분이 많습니다. 조만간 다시 수정해서 올리겠습니다.


- 아파치 서버를 띄우고 간단한 게시판 UI 등록
- 실행환경에 필요한 도커파일 작성

```Dockerfile
FROM ubuntu

LABEL maintainer="pnosong"

RUN apt-get update\
    && apt-get upgrade -y\
    && apt-get install vim git apache2 -y

ADD ./board.html /var/www/html/board.html

WORKDIR /var/www/html
EXPOSE 80

CMD [ "-D","FOREGROUND" ]
ENTRYPOINT [ "apachectl" ]
```

~~~
1. FROM 명령어를 통해 ubuntu 이미지를 이용한다. 태그는 사용하지 않았기 때문에 latest 버전을 사용했다.
2. LABEL 명령어를 이용한 도커피일 제작자 표시
3. RUN 명령어로 기본적인 업데이트 진행. 이미지 빌드 중에는 입력이 불가능 하기 때문에 -y 옵션을 미리 설정
4. ADD 명령어를 통해 생서된 컨테이너의 /var/www/html/ 경로에 board.html 파일 추가
5. WORKDIR 명령어로 기본적인 디렉토리를 /var/www/html/ 로 설정
6. EXPOSE 명령어로 컨테이너에서 80번 포트 이용
7. CMD 명령어로 컨테이너가 시작될 때 실행할 명령 설정. apache 서버를 이용하는 것이기 때문에 -D 옵션 설정
8. ENTRYPOINT 명령어로 마찬가지로 컨테이너가 시작될 때 실행할 명령어 설정
~~~


- 이미지 생성
~~~
docker build -t k8s_project_apache .
~~~

- 컨테이너 실행(호스트 머신의 9000포트 이용)
~~~
docker run -d --name k8s_study_container -p 9000:80 k8s_project_apache
~~~

- 웹 페이지 URL
~~~
http://localhost:9000/board.html
~~~

- 실행 화면
<img width="1000" alt="스크린샷 2023-02-14 오전 2 39 27" src="https://user-images.githubusercontent.com/92113241/218532645-a96b342e-234d-4445-8ac9-a77d22c76e48.png" style="width: 600px; height:auto;">
