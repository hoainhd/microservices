./gradlew :microservices:product-service:build
cd microservices/product-service
docker build -t product-service .
docker images | grep product-service
docker run --rm -p8080:8080 -e "SPRING_PROFILES_ACTIVE=docker" product-service
docker run -d -p8080:8080 -e "SPRING_PROFILES_ACTIVE=docker" --name my-prd-srv product-service
docker logs my-prd-srv -f
--tail 0
--since 5m
docker rm -f my-prd-srv

./gradlew clean build && docker-compose build && ./test-em-all.bash start stop
./gradlew build && docker-compose build && docker-compose up
docker images | grep demo01
docker-compose up -d
docker-compose ps
docker-compose logs -f
docker-compose logs -f product review
localhost:8080/product-composite/123
docker-compose down

docker system prune -f --volumes
docker-compose up -d --scale product=0
docker-compose up -d --scale product=1

docker ps --format {{.Names}}

http://localhost:8080/swagger-ui.html

docker-compose exec mongodb mongo product-db --quiet --eval "db.products.find()"
docker-compose exec mongodb mongo recommendation-db --quiet --eval "db.recommendations.find()"
docker-compose exec mysql mysql -uuser -p review-db -e "select * from reviews"

docker-compose exec mongodb mongo --quiet
db.products.find()
db.recommendations.find()
docker-compose exec mysql mysql -uuser -p review-db
select * from reviews;

export COMPOSE_FILE=docker-compose-partitions.yml
docker-compose build && docker-compose up -d

docker-compose down
unset COMPOSE_FILE

docker-compose exec kafka /opt/kafka/bin/kafka-topics.sh --zookeeper zookeeper --list
docker-compose exec kafka /opt/kafka/bin/kafka-topics.sh --describe --zookeeper zookeeper --topic products
docker-compose exec kafka /opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic products --from-beginning --timeout-ms 1000
docker-compose exec kafka /opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic products --from-beginning --timeout-ms 1000 --partition 1
