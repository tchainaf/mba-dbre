docker pull ubuntu

docker images

# Em build, cria-se uma imagem
docker build -t devops .
docker build -t devops:0.1.0 .
docker build -t devops:0.2.0 .

# Ao executar, cria-se um container
docker run ubuntu
docker run devops:0.2.0
docker run -it ubuntu /bin/bash
docker run -it -v .:/shared ubuntu /bin/bash
docker run -it -v .:/shared devops /bin/bash

# Listar containers 
docker ps -a
docker ps -qa

# Listar logs do container
docker logs [ID]

# Destruir container
docker rm [ID]
docker rm -f [ID]
docker rm -f $(docker ps -qa)

# Executar bash em container ativo
docker exec -it [ID] /bin/bash

# Publicar no DockerHub
docker build -t tchainaf/iac .
docker login -u tchainaf
docker push tchainaf/iac