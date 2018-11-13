# 安装 LimeSurvey 3.15.3 181108

```bash
docker pull mysql:5.5.50
docker pull php:5.6.38-fpm-alpine
docker build -t limesurvey:3.15.3-181108 .

docker run \
    --name limesurvey-db \
    -d \
    --network limesurvey \
    -e MYSQL_ROOT_PASSWORD=limesurvey \
    -e MYSQL_DATABASE=limesurvey \
    mysql:5.5.50

docker run \
    --name limesurvey-web \
    -d \
    --network limesurvey \
    limesurvey:3.15.3-181108
```