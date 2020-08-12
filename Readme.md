# Docker - mao na massa

Para seguir com esses exercicios, primeiramente baixe o Docker Desktop para sua plataforma (Windows, Linux ou Mac) atraves do link abaixo:
[Docker Desktop](https://www.docker.com/products/docker-desktop)

Depois, clone este repo e bora iniciar:

```console
git clone https://github.com/jonaopower/intro.docker.git
cd intro.docker
```

## Exemplo 1 - Criando um container via linha de comando

Baixar imagem NGINX do registry Docker Hub

```console
docker pull nginx:latest
```

Baixar imagem APACHE 2.4.33 alpine do registry Docker Hub

```console
docker pull httpd:2.4.33-alpine
```

Listar as imagens disponiveis localmente

```console
docker image ls
```

Verificar as camadas da imagem recem criada:

```console
docker history nome_da_imagem:tag
docker history id_imagem
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

Criar o arquivo "Dockerfile" (sem extensao e com D maiusculo) e adicionar o seguinte conteudo:

```Dockerfile
FROM nginx:latest
WORKDIR /usr/share/nginx/html
COPY app/ .
```

Fazer build da imagem:

```console
docker build -t nome_da_imagem:tag .
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

## Exemplo 4 - Push de imagem para registry (Docker Hub)

Para este exemplo, é necessário ter uma conta no [Docker Hub](https://hub.docker.com).

- Autenticar o Docker Desktop no registry padrao (Docker Hub):

```console
docker login
```

- Verificar o ID da imagem a que será enviada para o Docker HUB

```console
docker image ls
```

- Adicionar uma tag (ou versao) na imagem

```console
docker tag id_imagem hubusername/nome_imagem:tag
```

- Enviar imagem para docker HUB

```console
docker push hubusername/nome_imagem
```
