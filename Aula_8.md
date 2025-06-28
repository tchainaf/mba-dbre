# Minio

Object Store

https://min.io/docs/minio/container/index.html

## Run

```sh
cd minio
docker compose up
```

## Minio Client

https://min.io/docs/minio/linux/reference/minio-mc.html?ref=docs

```sh
echo "🔗 Conectando ao MinIO com mc..."
docker exec -i minio-client mc alias set local http://minio:9000 admin miniopwd

echo "🪣 Criando bucket chamado 'meu-bucket'..."
docker exec -i minio-client mc mb local/meu-bucket

echo "📂 Enviando arquivo para o bucket..."
echo "Este é um teste de upload via MinIO Client (mc)" > arquivo.txt
docker cp README.md minio-client:/README.md
docker exec -i minio-client mc cp /README.md local/meu-bucket/

echo "📋 Listando arquivos no bucket..."
docker exec -i minio-client mc ls local/meu-bucket/
```

# DBT

## Run PostgreSQL

```sh
docker run -d \
    --name postgres \
    --rm \
    -e POSTGRES_USER=new_user \
    -e POSTGRES_PASSWORD=my_pwd \
    -p 5432:5432 \
    postgres
```

## Install dbt

```sh
cd dbt
make install
mkdir profiles
```

## Start project

```sh
export DBT_PROFILE_DIR=$(pwd)/profiles
dbt init study_dbt --profiles-dir=$DBT_PROFILE_DIR
export DBT_PROJECT_DIR=$(pwd)/study_dbt
dbt debug --profiles-dir=$DBT_PROFILE_DIR
```

## Run

```sh
dbt seed --profiles-dir=$DBT_PROFILE_DIR
dbt run --profiles-dir=$DBT_PROFILE_DIR
```

## Generating Docs

```sh
dbt docs generate --profiles-dir=$DBT_PROFILE_DIR
dbt docs serve --profiles-dir=$DBT_PROFILE_DIR
```