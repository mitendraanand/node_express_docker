# Simple web app Docker

This is a quick and dirty node.js app cobbled together for the purposes of demonstrating how to Dockerize/containerize a simple app.

Exposes web server on port 8080 as per ./app.js

See **Dockerfile** for more details

Commands To Create Docker Image and Running It.

Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\git\docker\express_webapp> docker build --rm -f "Dockerfile" -t expresswebapp:latest "."
Sending build context to Docker daemon 18.84MB
Step 1/8 : FROM alpine
latest: Pulling from library/alpine
aad63a933944: Pull complete
Digest: sha256:b276d875eeed9c7d3f1cfa7edb06b22ed22b14219a7d67c52c56612330348239
Status: Downloaded newer image for alpine:latest
---> a187dde48cd2
Step 2/8 : LABEL maintainer="mitendra@gmail.com"
---> Running in e39ec7127e53
Removing intermediate container e39ec7127e53
---> 15a9a0c88149
Step 3/8 : RUN apk add --update nodejs nodejs-npm
---> Running in deef4c2c6b2a
fetch http://dl-cdn.alpinelinux.org/alpine/v3.11/main/x86_64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.11/community/x86_64/APKINDEX.tar.gz
(1/8) Installing ca-certificates (20191127-r1)
(2/8) Installing c-ares (1.15.0-r0)
(3/8) Installing libgcc (9.2.0-r4)
(4/8) Installing nghttp2-libs (1.40.0-r0)
(5/8) Installing libstdc++ (9.2.0-r4)
(6/8) Installing libuv (1.34.0-r0)
(7/8) Installing nodejs (12.15.0-r1)
(8/8) Installing npm (12.15.0-r1)
Executing busybox-1.31.1-r9.trigger
Executing ca-certificates-20191127-r1.trigger
OK: 64 MiB in 22 packages
Removing intermediate container deef4c2c6b2a
---> 473175b9b03b
Step 4/8 : COPY . /src
---> 9ff2e727bc6c
Step 5/8 : WORKDIR /src
---> Running in 0924964fb95a
Removing intermediate container 0924964fb95a
---> 8ba2059993d4
Step 6/8 : RUN npm install
---> Running in b43e70a20a07
audited 262 packages in 10.33s

4 packages are looking for funding
run `npm fund` for details

found 6 vulnerabilities (3 low, 2 moderate, 1 critical)
run `npm audit fix` to fix them, or `npm audit` for details
---> 6d1069227da9
Step 7/8 : EXPOSE 8080
Removing intermediate container 546c1725f963
---> 0807e4db0a7a
Step 8/8 : ENTRYPOINT ["node", "./app.js"]
---> Running in f222cc70d2e7
Removing intermediate container f222cc70d2e7
---> f9cb353e1296
Successfully tagged expresswebapp:latest
SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host. All files and directories
added to build context will have '-rwxr-xr-x' permissions. It is recommended to double check and reset permissions for sensitive files and directories.
PS C:\git\docker\express_webapp> docker image ls expresswebapp:latest
REPOSITORY TAG IMAGE ID CREATED SIZE

PS C:\git\docker\express_webapp> docker image ls
REPOSITORY TAG IMAGE ID CREATED SIZE
basic latest f9cb353e1296 21 minutes ago 69.8MB
expresswebapp latest f9cb353e1296 21 minutes ago 69.8MB
alpine latest a187dde48cd2 7 days ago 5.6MB

PS C:\git\docker\express_webapp> ls

    Directory: C:\git\docker\express_webapp

Mode LastWriteTime Length Name

---

d----- 31-03-2020 03:10 node_modules
-a---- 31-03-2020 03:08 216 circle.yml
-a---- 31-03-2020 03:13 332 Dockerfile
-a---- 31-03-2020 03:10 43230 package-lock.json
-a---- 31-03-2020 03:08 421 package.json
-a---- 31-03-2020 03:12 244 README.md

PS C:\git\docker\express_webapp> docker image ls
REPOSITORY TAG IMAGE ID CREATED SIZE
basic latest f9cb353e1296 24 minutes ago 69.8MB
expresswebapp latest f9cb353e1296 24 minutes ago 69.8MB
alpine latest a187dde48cd2 7 days ago 5.6MB
PS C:\git\docker\express_webapp> docker run expresswebapp

# Below commands runs the app directly

PS C:\git\docker\express_webapp> node .\app.js

# This runs the containerized apps

PS C:\git\docker\express_webapp> docker run -p 4000:8080 expresswebapp
