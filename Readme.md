# Dev Starter Pack - Hands-on Docker

Baixar o Docker Desktop para sua plataforma (Windows, Linux ou Mac) atraves do link abaixo:
[Docker Desktop](https://www.docker.com/products/docker-desktop)


## Exemplo 1 - Criando um container via linha de comando 
 Baixar imagem NGINX do registry Docker Hub
```console
docker pull nginx:latest
```

 Baixar imagem APACHE do registry Docker Hub
```console
docker pull httpd:latest
```

 Listar as imagens disponiveis localmente
```console
docker image ls
```
 
 Criar e executar um container a partir da imagem baixada (nginx)
```console
docker run -d -p 8080:80 nginx:latest
```
 
 Listar os containers em execucao
 ```console
 docker container ls 
 ```

 Parar um container
```console
docker container stop <container_id>
```


## Exemplo 2 - Build de uma imagem com codigo

Clonar repo de com aplicacao de exemplo (Azure Devops):
```console
git clone https://localiza.visualstudio.com/DefaultCollection/StarterPack/_git/intro.docker
```

Clonar repo de com aplicacao de exemplo (GitHub):
```console
git clone https://github.com/jonaopower/intro.docker.git
```

Criar o arquivo Dockerfile (sem extensao e com D maiusculo) e adicionar o seguinte conteudo:
```Dockerfile
FROM nginx:latest
WORKDIR /usr/share/nginx/html
COPY app/ .
```

Fazer build da imagem:
```console
cd intro.docker
docker build -t nome_da_imagem:tag .
```

Verificar as camadas da imagem recem criada:
```console
docker history nome_da_imagem:tag
```

 Criar e rodar um container a partir da imagem recem criada
```console
docker run -d -p 8080:80 nome_da_imagem:tag
```

 Confirmar que container foi criado, está rodando, e que foi publicado atraves da porta 8080:
```console
docker container ls
docker ps
```

Acessar a aplicacao recem publicada atraves do link abaixo:
[http://localhost:8080](http://localhost:8080)

Parar o container:
```console
docker container stop <container_id>
```

## Exemplo 3 - Build de uma imagem com codigo + volume persistente

Modificar o arquivo Dockerfile conforme exemplo abaixo:
```Dockerfile
FROM nginx:latest
```

Fazer build da imagem:
```console
docker build -t nome_da_imagem:tag .
```

Verificar as camadas da imagem recem criada:
```console
docker history nome_da_imagem:tag
```

 Criar e rodar um container a partir da imagem recem criada
```console
 docker run -v <caminho_completo_diretorio_app>:/usr/share/nginx/html -d -p 8090:80 nome_da_imagem:tag
```

 Confirmar que container foi criado, está rodando, e que foi publicado atraves da porta 8080:
```console
docker container ls
docker ps
```

Acessar a aplicacao recem publicada atraves do link abaixo:
[http://localhost:8090](http://localhost:8090)

Parar o container:
```console
docker container stop <container_id>
```