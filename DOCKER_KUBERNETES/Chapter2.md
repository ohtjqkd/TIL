# Management container by Docker

## Lifecycle
![](https://k21academy.com/wp-content/uploads/2020/10/Capture-5.png)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9987C3475E1D4BE835)


## Command

### create and start
```
# container create
docker create [image]
# container start
docker start []

# container create & start
docker run [image]
```

* docker run option
    - `-i`: interactive mode
    - `-t`: tty할당
    - `--rm`: 컨네이너 실행 종료 후 자동 삭제
    - `-d`: background mode (detached)
    - `--name [container-name]`: 컨네이너 이름 지정하여 실행
    - `-p n:n`: port binding
    - `-v /host-path:/container-path`: volume binding
    - `[image]`: docker 이미지
    - `[command]`: 컨테이너 내에서 실행할 명령어

* foreground에서 실행 중에 실행을 중지시키지 않고 호스트로 돌아오기: ctrl + p, q

## show container info

```
# 실행중인 컨테이너 상태 확인
docker ps

# 전체 컨테이너 상태 확인
docker ps -a

# 컨테이너 상세 정보 확인
docker inspect [container]
```

## pause and stop container
```
# container pause
docker pause [container]

# container unpause
docker unpause [container]

# container stop
docker stop [container]

# all container stop
docker stop $(docker ps -a -q)

# container force quit
docker kill [container]
```

## remove container
```
# remove container(running x)
docker rm [container]

# remove container after force quit
docker rm -f [container]

# remove container after container down
docker run --rm ...

# remove container stopped container
docker container prune
```

## Entrypoint and Command

- Entrypoint: 도커 컨테이너가 실행할 때 고정적으로 실행되는 스크립트 혹은 명령어, 생략할 수 있으며 생략될 경우 커맨드에 지정된 명령어로 수행

- Command: 도커 컨테이너가 실행할 때 수행할 명령어 혹은 엔트리포인트에 지정된 명령어에 대한 인자 값

entrypoint를 sh로 지정하면 command를 실행할 때 sh 환경에서 실행하게 됨

## Environment variable
1. run command
    ```
    docker run -e [variable_name] = [variable_value]
    ```

2. env file
    ```
    # something.env
    docker run --env-file [env_file_path]
    ```

## Run Command
```
docker exec [container] [command]
# bash로 접속
docker exec -it [container] bash
```

## Network
- Docker Network
    ![docker network](https://docs.docker.com/engine/tutorials/bridge3.png)
    docker0이 host와 container의 bridge network로 설정됨

    ```
    docker run -p [HOST_IP:PORT]:[CONTAINER_PORT] [conatainer]

    # 예시
    # nginx 컨테이너의 80번 포트를 호스트 모든 IP의 80번 포트와 연결하여 실행
    docker run -d -p 80:80 nginx
    # nginx 컨테이너의 80번 포트를 호스트 127.0.0.1 IP의 80번 포트와 연결하여 실행
    docker run -d -p 127.0.0.1:80:80 nginx
    # nginx 컨테이너의 80번 포트를 호스트의 사용 가능한 포트와 연결하여 실행
    docker run -d -p 80 nginx
    ```

- Expose vs Publish
    ```
    # expose 옵션은 문서화 용도
    docker run -d --expose 80 nginx
    # publish 옵션은 실제 포트를 바인딩
    docker run -d -p 80 nginx
    ```

- custom network
    ```
    docker network create --driver=bridge fastcampus

    docker run -d --network=fastcampus --net-alias=hello nginx
    ```
    net-alias는 네트워크 상에서 domain name으로 쓰임

Network 부분은 기존에 사용할 때 어려움이 많았던 부분, 다시 한 번 찾아보고 사용법을 익혀야겠다

## Volume
__Docker layer__
- Container layer: Read Write
    container가 생성됐을 때 생기는 layer, 컨테이너 종료시에 삭제된다.
- Image layer: Read Only
    image가 빌드 될 때 생성되며 docker run을 통해 컨테이너가 생겨도 image는 변경되지 않음
    image는 여러 개의 layer로 나누어져 있으며 이미지가 빌드가 된 이후 변경사항이 있다면 수정된 레이어만 다시 빌드하여 저장한다.

__Host Volume__  
```
# 호스트의 /opt/html 디렉토리를 Nginx의 웹 루트 디렉토리로 마운트
docker run -d --name nginx -v /opt/html:/usr/share/nginx/html nginx
```

__Volume Container__  
특정 컨테이너의 볼륨 마운트를 공유할 수 있음
```
docker run -d --name [volume name] -it -v /opt/html:/usr/share/nginx/html ubuntu:focal

#my-volume 컨터네이의 볼륨을 공유
docker run -d --name nginx --volumes-from [volume name] nginx
```

__Docker Volume__  
도커가 제공하는 볼륨 관리 기능을 활용하여 데이터를 보존
기본적으로 /var/lib/docker/volume/$(volume-name)/_data에 데이터가 저장됨
```
# web-volume 도커 볼륨 생성
docker volume create --name db

# 도커의 web-volume 볼륨을 nginx의 웹 루트 디렉토리로 마운트
docker run -d --name fastcampus-mysql \
    -e MYSQL_DATABASE=fastcampus \
    -e MYSQL_ROOT_PASSWORD=fastcampus \
    -v db:/var/lib/mysql -p 3306:3306 mysql:5.7
```

__읽기전용 볼륨 연결__
볼륨 연결 설정에 :ro 옵션을 통해 읽기 전용 마운트 옵션을 설정 가능
```
# 도커의 web-volume 볼륨을 nginx의 웹 루트 디렉토리로 읽기 전용 마운트
docker run -d --name nginx -v web-volume:/usr/share/nginx/html:ro nginx
```