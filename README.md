# Sticky-session Load Balancer 구현

-------
#### 시행착오
- 처음에 docker swarm, docker stack 이 제공하는 loadbalancer 를 사용했지만, stickysession 을 제공하지 않는다.
- stickysession 을 제공하는 traefik 이미지를 사용하여 loadbalancer 컨테이너를 배포했다.
- traefik 컨테이너가 http, https 포트를 가지고 있기 때문에 https 를 작동할때에는 traefik을 통해야 한다.
- volume 을 사용하여 ssl 인증서를 traefik 에 연결했다.
------

#### 사용하는 이미지 
- Image: traefik:v1.7.16-alpine 
- 출처 : https://hub.docker.com/_/traefik

------

#### 제공하는 기능
- sticky session 
- ssl 인증서 연결
- dashboard 사용

------

#### 사용방법
- {domain}, {image}, {email} 안에 해당되는 내용을 추가한다
- 네트워크를 만든다 (이름은 yml 파일에 정의되어 있음)

      docker create network pub_net 
  
- traefik 컨테이너를 실행한다

      docker-compose up -d
  
- web 컨테이너를 실행하고 복제한다 (원하는 개수만큼)

      cd web
      docker-compose up -d
      docker-compose scale pub=5 
  
 ------ 

#### 환경
- docker version: 19.03.12
- docker-compose version: 1.27.1
- ssl 인증서 경로 : /etc/letsencrypt/
