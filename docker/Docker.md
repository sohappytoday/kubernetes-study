# Docker

## Index
- [Container](#Container)
- [도커 준비 환경](#도커-준비-환경)

---
## Container
컨테이너란 OS 위에 만들어지는 '격리'된 가상 환경

### Why Container?
1\. Compare with VM(Virtual Machine)

VM은 Hypervisor 위에 OS까지 가상화하여 격리한다.  
다만, Docker는 Host OS 커널을 공유하면서 사용자 공간만 격리하여 실행한다.  
따라서 가볍고 더 빠르게 애플리케이션을 실행할 수 있다.

2\. Use MSA(Micro Service Architecture) in company

정확히는 컨테이너가 MSA 운영을 쉽게 만들어줘서 MSA를 선택하는 회사가 많아졌지만,  
신입 개발자 입장에서는 반대로 회사가 많이 채택하니까 공부해서 나쁠 것 없다!라고 이해하면 될 것 같다.

### What is Docker?
도커는 컨테이너 기술을 이용해 어디서든(macOS, Windows, Ubuntu 등) 동일한 환경을 만들 수 있게 해준다.

---
## 도커 준비 환경
nginx 서버를 시작하기 위해 명령어를 치려 하나, 현재 진행중인 프로젝트가 있어 8090포트로 맞춰두었다.
```shell
docker run --rm --detach --publish 8090:80 --name web nginx:mainline
```

### 도커 이미지  
애플리케이션을 실행하는 데 필요한 모든 것과 메타데이터 등 컨테이너의 각종 설정의 집합체이다.
도커 이미지는 여러 개의 이미지 레이어를 쌓아 올려 만든다.

### Dockerfile  
Dockerfile은 컨테이너 이미지의 설계도이다.
```Dockerfile
# 베이스 이미지 선택
FROM nginx:mainline

# 내 index.html을 컨테이너 안으로 복사
COPY index.html /usr/share/nginx/html
```

이렇게 하면 `http://localhost:8090` 접속 시 내 index.html이 뜨게 되는 컨테이너를 실행할 이미지를 생성하게 된다.
```shell
# 이미지 빌드
docker build ./docker/custom-nginx -t nginx-custom:1.0.0
```

### 컨테이너 실행
`--rm` : 컨테이너 종료시 자동 삭제
`-d` : 백그라운드 실행
`-p` : Port 포워딩
`--name` : 컨테이너 이름 지정
```shell
# 이미지 실행
docker run --rm -d -p 8090:80 --name web nginx-custom:1.0.0
```

### registry 구축
private registry를 구축해주었다.
```shell
docker run -d -p 5000:5000 -v ./docker/registry:/var/lib/registry --name registry registry:2

docker tag nginx-custom:1.0.0 localhost:5000/nginx-custom:1.0.0
docker push localhost:5000/nginx-custom:1.0.0
```
이미지를 tag 후 registry에 `docker push`를 해주었다.

