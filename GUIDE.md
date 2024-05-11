# GUIDE

## Step by step

```shell
docker compose up -d
cd migrate && \
    go get && \
    go run main.go tables.go init && \
    go run main.go tables.go 25012024_posts.go migrate

cd crawler && \
    go run main.go

cd consumer && \
    go run main.go tables.go

```

```shell
docker network create --attachable crawler
docker compose -f docker-compose-crawler.yaml build
docker compose -f docker-compose-stream.yaml up -d

# Fix bugs not start kafka and elasticsearch
sudo chmod -R 777 elasticsearch
sudo chmod -R 777 kafka
docker compose -f docker-compose-stream.yaml up -d

docker compose -f docker-compose-crawler.yaml up -d
docker compose -f docker-compose-api.yaml up -d
```