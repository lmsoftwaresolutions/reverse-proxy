# Folder Structure

```
dev-reverse-proxy/
├─ docker-compose.yml
├─ nginx/
│  ├─ nginx.conf
│  └─ certs/       # self-signed certificates will go here
```

# Generate Self Signed Certificates

Generate self-signed certs for local domains:

Linux:
```
mkdir -p nginx/certs/lmsoftwaresolutions.local
mkdir -p nginx/certs/successscienceacademy.local
mkdir -p nginx/certs/nathkrupa.lmsoftwaresolutions.local
```
Windows:
```
mkdir nginx\certs\lmsoftwaresolutions.local
mkdir nginx\certs\successscienceacademy.local
mkdir nginx\certs\nathkrupa.lmsoftwaresolutions.local
```
# lmsoftwaresolutions.local
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout nginx/certs/lmsoftwaresolutions.local/privkey.pem \
  -out nginx/certs/lmsoftwaresolutions.local/fullchain.pem \
  -subj "/CN=lmsoftwaresolutions.local"

# successscienceacademy.local
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout nginx/certs/successscienceacademy.local/privkey.pem \
  -out nginx/certs/successscienceacademy.local/fullchain.pem \
  -subj "/CN=successscienceacademy.local"

# nathkrupa.lmsoftwaresolutions.local
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout nginx/certs/nathkrupa.lmsoftwaresolutions.local/privkey.pem \
  -out nginx/certs/nathkrupa.lmsoftwaresolutions.local/fullchain.pem \
  -subj "/CN=nathkrupa.lmsoftwaresolutions.local"
  ```

# Update /etc/hosts
Add these lines to your local machine:

```
127.0.0.1 lmsoftwaresolutions.local www.lmsoftwaresolutions.local
127.0.0.1 successscienceacademy.local www.successscienceacademy.local
127.0.0.1 nathkrupa.lmsoftwaresolutions.local
```

# How to Run Locally

+ Build/run your frontends (or use placeholders like nginx:alpine for testing).
+ Start the reverse proxy:
```
docker network create web
docker-compose up -d
```

# Access in your browser (given that all other apps are also deployed using docker compose up command)
```
https://lmsoftwaresolutions.local
https://successscienceacademy.local
https://nathkrupa.lmsoftwaresolutions.local
```
Your browser may warn about self-signed certificates. You can click “Proceed” for dev testing.

