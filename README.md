# Nginx 설정 파일 구조 및 적용 방법

## 파일 구조

다음과 같은 구조로 Nginx 설정 파일을 구성

```
프로젝트_디렉토리/
├── docker-compose.yml
├── nginx/
   ├── nginx.conf
   └── conf.d/
       ├── dev.conf
       └── prod.conf

```

## 각 nginx 설정 파일의 역할
- `nginx/nginx.conf`: 메인 설정 파일
- `nginx/conf.d/dev.conf`: 개발용 도메인 설정
- `nginx/conf.d/prod.conf`: 운영용 도메인 설정


## 적용 방법
1. 도메인에 대한 SSL 인증서가 있는지 확인

- dev.eeos.co.kr 인증서: `/etc/letsencrypt/live/dev.eeos.co.kr/`
- eeos.co.kr 인증서: `/etc/letsencrypt/live/eeos.co.kr/`

인증서가 없다면 다음 명령어로 발급

```bash
certbot certonly --webroot -w /path/to/webroot -d eeos.co.kr
```

2. Nginx 설정 파일 수정
- 각 설정 파일의 proxy_pass ${DEV_IP}, ${PROD_ID} 부분을 실제 서버 IP로 변경

3. Docker 컨테이너 실행

```bash
docker-compose down
docker-compose up -d
```

4.  다음 URL로 테스트

- https://domain/health-check
