## Docker
- [mysql docker official reference](https://dev.mysql.com/doc/mysql-installation-excerpt/8.0/en/docker-mysql-more-topics.html)

#### 도커 컨테이너 실행
```
docker compose up -d
```

#### 도커 컨테이너 내부 엑세스
```
docker compose exec mysql bash
```

## mysql version
- 강의의 예제는 8.0.2이지만 ARM기반 CPU로 된 맥에서 mysql docker를 실행하기 위해서는 8.0.28버전 이상이 필요.
- 현 시점(20230201)에서 최신 버전인 8.0.32를 사용


## Connection
#### in container
```
mysql -u루트게정 -p루트비밀번호
```
- example : `mysql -uroot -ppassword`

#### in host
```
docker compose ps
```
- PORTS 부분을 확인하면 `33060/tcp, 0.0.0.0:33060->3306/tcp`으로 되어 있는 것을 알 수 있다.
- host에서 도커의 mysql에 접근하려면 ip는 `0.0.0.0`, port는 `33060`을 입력한다.

## dbeaver
- 호스트 컴퓨터에 설치한다.
- [download](https://dbeaver.io/download/) mysql workbench의 경우 arm cpu를 지원하는 버전이 없기 때문에 다른 툴을 사용하도록 하자.
- host에서 도커의 mysql에 접근하려면 `docker compose ps` 결과에서 post부분 정보에 해당하는 ip는 `0.0.0.0`, port는 `33060`을 입력한다.

### 쿼리를 입력해서 잘 작동하는지 확인 해 보자.
```
show databases;
```

## 대용량 데이터 셈플
- https://dev.mysql.com/doc/index-other.html


## Reference
- [혼자 공부하는 SQL](https://www.youtube.com/playlist?list=PLVsNizTWUw7GCfy5RH27cQL5MeKYnl8Pm)
- [mysql DOCKER OFFICIAL IMAGE](https://hub.docker.com/_/mysql)