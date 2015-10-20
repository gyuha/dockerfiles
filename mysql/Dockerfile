FROM ubuntu:14.04

# ENV로 환경 변수 DEBIAN_FRONTEND에 noninteractive를 반드시 설정한다.
# apt-get으로 MySQL 패키지를 설치하면 사용자가 직접 root 비밀번호를 입력하는 부분이 나온다.
# 하지만, Docker 이미지를 생성할 때는 입력을 할 수가 없으므로 noninteractive를 설정해서 넘어감.
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN echo "mysql-server mysql-server/root_password password" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password" | debconf-set-selections
RUN apt-get install -y mysql-server

WORKDIR /etc/mysql
# mysql 외부 접속 허용
RUN sed -i "s/127.0.0.1/0.0.0.0/g" my.cnf

ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# 접속 포트
EXPOSE 3306

ENTRYPOINT /entrypoint.sh
