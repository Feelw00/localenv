# localenv

## 설치

### Git Clone

```bash
git clone https://github.com/Feelw00/local-databases.git
```

### 볼륨 생성

```bash
sh prepare_volumes.sh
```

## 실행

### Compose 실행

```bash
docker compose up -d
```

### 일부 컨테이너 실행

```bash
docker compose up -d {container_name} # 또는 docker-compose 주석 처리
```

### 컨테이너 삭제

```bash
docker compose down
```

### 일부 컨테이너 삭제

```bash
docker compose down {container_name}
```

### Data Dump

```bash
mysqldump -u 사용자이름 -p 비밀번호 DB명 > dump-DB명-202301011159.sql
```

### Data Load

```bash
mysql -u 사용자이름 -p DB명 < dump-DB명-202301011159.sql
```

## LocalStack

로컬에서 AWS 서비스를 사용할 수 있게 해주는 서비스

### LocalStack 설치

```bash
brew install awscli awscli-local
```

### LocalStack 환경 설정

```bash
aws configure
AWS Access Key ID [****************asdf]: asdf
AWS Secret Access Key [****************1234]: asdf1234
Default region name [ap-northeast-2]: ap-northeast-2
Default output format [None]:
```

### LocalStack 실행

```bash
localstack start
```

### LocalStack 컨테이너 실행

```bash
docker compose up -d localstack
```

### SQS 대기열 생성

```bash
awslocal sqs create-queue --queue-name health-check
```

### SQS 메시지 전송

```bash
awslocal sqs send-message --queue-url http://sqs.ap-northeast-2.localhost.localstack.cloud:4566/000000000000/health-check --message-body "Hello World"
```

### SQS 메시지 수신

```bash
awslocal sqs receive-message --queue-url http://sqs.ap-northeast-2.localhost.localstack.cloud:4566/000000000000/health-check
```

### SQS 메시지 삭제

```bash
awslocal sqs delete-message --queue-url http://sqs.ap-northeast-2.localhost.localstack.cloud:4566/000000000000/health-check
```
