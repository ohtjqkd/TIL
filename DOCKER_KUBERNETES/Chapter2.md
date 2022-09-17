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