# Load Balancer 구현

1. 사용하는 이미지 
- Image: traefik:v1.7.16-alpine 
- 출처 : https://hub.docker.com/_/traefik

2. 제공하는 기능
- sticky session 
- ssl 인증서 연결

3. 시행착오
- 처음에 docker swarm, docker stack 이 제공하는 loadbalancer 를 사용했지만, stickysession 을 제공하지 않는다.
- stickysession 을 제공하는 traefik 이미지를 사용하여 loadbalancer 컨테이너를 배포했다.
- traefik 컨테이너가 http, https 포트를 가지고 있기 때문에 https 를 작동할때에는 traefik을 통해야 한다.
- volume 을 사용하여 ssl 인증서를 traefik 에 연결했다.
