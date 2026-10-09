# Docker Cheatsheet — Commands That Actually Work

One page. Twenty-eight commands. Each entry tells you **what it does**, **a command you can copy-paste**, and **tags**. No made-up flags — every command verified against the official docs.

> 🌍 Read this project in your language: [中文](README.md) · [Español](README.es.md) · [Português](README.pt.md)

Docs: https://docs.docker.com/

---

## 🖼️ Images

### `docker pull` — download an image from a registry
```bash
docker pull nginx:1.27        # pin a version (don't use :latest in production)
```
🏷️ `#images` `#registry`
### `docker images` — list images on your machine
```bash
docker images                 # REPOSITORY, TAG, size, age
```
🏷️ `#images` `#listing`
### `docker build` — build an image from a Dockerfile
```bash
docker build -t myapp:1.0 .          # -t names it; "." is the build context
```
🏷️ `#images` `#build`
### `docker tag` — retag an image (e.g. before pushing)
```bash
docker tag myapp:1.0 myregistry.com/team/myapp:1.0
```
🏷️ `#images` `#registry`
### `docker push` — push an image to a registry
```bash
docker login && docker push myregistry.com/team/myapp:1.0
```
🏷️ `#images` `#registry` `#deploy`
### `docker rmi` — delete a local image
```bash
docker rmi myapp:1.0          # fails if a container still uses it; -f to force
```
🏷️ `#images` `#cleanup`
### `docker image prune` — delete unused images
```bash
docker image prune            # dangling only (safe)
docker image prune -a         # ALL unused — re-downloads hurt on slow networks
```
🏷️ `#images` `#cleanup` `#disk-space`

---

## 📦 Container lifecycle

### `docker run` — the one command that starts most containers
```bash
docker run -d --name web -p 8080:80 -v webdata:/usr/share/nginx/html nginx:1.27
# -d detached, --name easy handle, -p host:container, -v volume:mount
```
🏷️ `#containers` `#run` `#must-know`
### `docker ps` — list containers
```bash
docker ps       # running only
docker ps -a    # everything, including dead ones
```
🏷️ `#containers` `#listing`
### `docker start` / `stop` / `restart` — lifecycle controls
```bash
docker stop web && docker start web    # or: docker restart web
```
🏷️ `#containers` `#lifecycle`
### `docker rm` — delete a container
```bash
docker rm web       # stopped only
docker rm -f web    # stop AND delete, right now
```
🏷️ `#containers` `#cleanup`
### `docker run --rm` — throwaway containers
```bash
docker run --rm -it ubuntu:24.04 bash   # gone when you exit — great for experiments
```
🏷️ `#containers` `#testing`

---

## 🔍 Inside the container & logs

### `docker exec -it` — open a shell in a running container
```bash
docker exec -it web sh    # sh exists everywhere; try bash if it fails
```
🏷️ `#debug` `#shell`
### `docker logs` — read a container's output
```bash
docker logs -f --tail 100 web   # follow live, last 100 lines
```
🏷️ `#logs` `#debug`
### `docker cp` — copy files in and out
```bash
docker cp web:/etc/nginx/nginx.conf ./      # container -> host
docker cp ./index.html web:/usr/share/nginx/html/  # host -> container
```
🏷️ `#files` `#debug`

---

## 💾 Volumes & networks

### `docker volume` — persistent data
```bash
docker volume create webdata    # named volume (survives container deletion)
docker volume ls                # list them
```
🏷️ `#volumes` `#data`
### `docker volume rm` — delete a volume (data goes with it)
```bash
docker volume rm webdata        # ⚠️ deletes the data — double-check the name
```
🏷️ `#volumes` `#cleanup` `#danger`
### `docker network` — container networking
```bash
docker network create mynet                       # containers on mynet resolve each other by name
docker run -d --name api --network mynet myapp:1.0
docker network inspect mynet                      # see who's attached
```
🏷️ `#networking`

---

## 📝 Dockerfile quick reference

### Essential instructions
```dockerfile
FROM node:22-alpine        # base image — always pin a version
WORKDIR /app               # following paths are relative to /app
COPY package*.json ./      # manifests first (better layer caching)
RUN npm ci --omit=dev      # install deps at build time
COPY . .                   # then the source
EXPOSE 3000                # documents the port (does NOT publish it)
CMD ["node", "server.js"]  # default command; ENTRYPOINT + CMD = fixed binary + default args
```
🏷️ `#dockerfile` `#build`
### Minimal working example
```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8000
CMD ["python", "app.py"]
```
```bash
docker build -t hello-py:1.0 . && docker run -d --name hello-py -p 8000:8000 hello-py:1.0
```
🏷️ `#dockerfile` `#example`

---

## 🐳 Docker Compose in practice

### `docker compose up` / `down` — multi-container apps
```bash
docker compose up -d        # build (if needed) + start everything, detached
docker compose down         # stop + remove containers/networks (volumes stay)
docker compose down -v      # also delete named volumes — ⚠️ data loss
```
🏷️ `#compose` `#deploy`
### `docker compose logs` / `ps` / `exec` — operate the stack
```bash
docker compose ps                               # status of every service
docker compose logs -f web                      # follow one service
docker compose exec db psql -U postgres         # run a command in the db service
```
🏷️ `#compose` `#ops`
### Sample `compose.yaml` — web + database
```yaml
services:
  web:
    build: .
    ports: ["3000:3000"]
    depends_on: [db]
  db:
    image: postgres:16
    environment: {POSTGRES_PASSWORD: example}
    volumes: [pgdata:/var/lib/postgresql/data]
volumes: {pgdata:}
```
🏷️ `#compose` `#example` `#postgres`

---

## 🧹 Cleanup

### `docker system prune` — the big red button
```bash
docker system prune                # stopped containers, unused networks/images (asks first)
docker system prune -a --volumes   # ⚠️ EVERYTHING unused — read twice, run once
```
🏷️ `#cleanup` `#danger` `#disk-space`
### `docker container prune` — remove stopped containers only
```bash
docker container prune        # safe-ish: running containers are untouched
```
🏷️ `#cleanup` `#containers`

---

## 🩺 Debugging

### `docker inspect` — full JSON details of anything
```bash
docker inspect -f '{{.State.Status}}' web   # running / exited / dead
```
🏷️ `#debug` `#inspect`
### `docker stats` — live resource usage
```bash
docker stats --no-stream       # one snapshot (script-friendly); drop the flag for live view
```
🏷️ `#debug` `#monitoring`
### `docker top` — processes inside a container
```bash
docker top web                # is your app actually running in there?
```
🏷️ `#debug` `#processes`
### Container won't start? The three-step drill
```bash
docker logs web               # 1. read the error — 90% of answers are here
docker inspect web            # 2. check State.ExitCode, mounts, and env
docker run --rm -it --entrypoint sh myapp:1.0   # 3. bypass CMD, explore the image yourself
```
🏷️ `#debug` `#troubleshooting` `#must-know`

---

## Contributing

Found a wrong command, an outdated flag, or a bad translation? Pull requests are welcome — keep entries to the format above (one-liner / bash block / tags) and **only real, verified commands; when in doubt, leave it out**.

## License

MIT © 2026 Guangyi Zhao. See [LICENSE](LICENSE).
