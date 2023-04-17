# Docker

### 1. Build 1 image:

```bash
docker build -t image_name .
```

`-t` : tag

`.` : folder hiện tại

### 2. Run 1 container:

```bash
docker run -d -p 3001:3000 docker/getting-started
```

View logs

```bash
docker logs <container-id>
```

`-d` : detached, run background

`-p` : port

`3001:3000` : 3001 là port trên máy tính (localhost:3001), 3000 là port của docker

### 3. Danh sach toan bo cac containers:

```bash
docker ps -a
```

`ps`: process status

`-a`: --all

### 4. Remove 1 container by `container-id`:

```bash
docker rm <container-id>
```

`rm`: remove

`-f`: force

### 5. Đặt lại tên cho image

```bash
docker tag getting-started1 sangtd/getting-started
```

`tag`: Định danh image getting-started1 (local) cho repo sangtd/getting-started (docker hub)

### 6. Push image to docker hub

```bash
docker push sangtd/getting-started
```

push image getting-started1 to docker hub with repo sangtd/getting-started

### 7. Create a volume (giữ lại data giữa các lần chạy container - where the last one left off)

```bash
docker volume create todo-db
```

### 8. Tạo 1 container và mount với volume todo-db

```bash
docker run -dp 3000:3000 --mount type=volume,src=todo-db,target=/etc/todos getting-started
```

The `--mount` option tells Docker to create a volume mount,

### 9. Kiểm tra nơi docker lưu trữ data volume todo-db

```bash
docker volume inspect todo-db
```

### 10. Khác nhau giữa volume mounts và bind mounts.

-   A `volume mount` is a great choice when you need somewhere persistent to store your application data.
-   A `bind mount` is another type of mount, which lets you share a directory from the host’s filesystem into the container. When working on an application, you can use a bind mount to mount source code into the container

### 11.

`docker exec <container-id> cat /data.txt`

### 12.

`docker run -it ubuntu ls /`

### 13. Run a container for `bind mount` `host directory` into `container directory`

```bash
docker run -dp 3000:3000 -w /app --mount type=bind,src="$(pwd)",target=/app node:18-alpine sh -c "yarn install && yarn run dev"
```

`-dp`: <=> `-d -p`
`-w`: set `working directory` that the command will run from
`--mount type=bind,src="$(pwd)",target=/app`: bind mount the current directory from the host(local pc) into the `/app` directory in the container
`node:18-alpine`: image
`sh -c "yarn install && yarn run dev"`: the command, starting a shell using `sh`

### 14. Watch the logs

```bash
docker logs -f <container-id>
```
