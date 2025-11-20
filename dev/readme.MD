# 구조
.
└─ app
    └─ Dockerfile       : fast api 관련 도커파일 (핵심서비스)
    └─ main.py          : 파이썬 구성된 fastapi 기반 코드 (개발한 내용)
    └─ requirements.txt : 서비스 구동을 위한 필요 패키지 목록
└─ nginx
    └─ nginx.conf       : nginx 에서 fastapi로 프록시 하는 구성 (설정파일)
└─ docker-compse.yml    : 컴포즈 파일 -> n개의 컨테이너 구성 -> 연결 -> 구동

# 구성 명령
## 생성 및 실행
docker-compose up -d --build
## 종료 및 제거
docker-compose down

# 시크릿 변수
- MYSQL_ROOT_PASSWORD   -> 1234
- MYSQL_USER            -> guest
- MYSQL_PASSWORD        -> 1234
- DOCKER_USERNAME       -> gwaun260
- DOCKER_PASSWORD       -> 
- EC2_HOST              -> 15.152.37.188
- EC2_USERNAME          -> ubuntu
- EC2_KEY               -> xxx.pem 파일 내용전부

# Docker 기반 CI/CD 흐름도
로컬 PC 개발 -> GIT 특정브런치 PUSH -> 이벤트 감지 -> Git Action 작동
-> xxx.yml에 상세하게 잡들 기술 -> 커스텀으로 구성
-> 소스코드를 체크아웃(git action에서 제공하는 리눅스에 소스코드 체크아웃)
-> 검증
-> 도커 허브 로그인 -> git action에서 제공하는 리눅스에 세션이 생성됨
(사용자명, 액세스토큰 제공(시크릿변수))
-> fastapi 앱, 커스텀된 nginx 이미지를 Dockerfile 생성하여(build) -> 푸시(본인 계정의 도커허브 레퍼지토리상에)