# Ai4Europeana Application
Repository containing the docker images for europeana Backend and Frontend

# Frontend

### Start Docker
```shell
docker load -i path/to/image/ai4europeana-frontend.tar
# Check that you succesfully loaded the image
docker image ls -a

# Run the docker image
docker run \
  -e VITE_APP_TITLE=ReactStarter \
  -e VITE_API_ENDPOINT= \
  ai4europeana-frontend
```

# Subplayer (platform for video subtitling)

### Start Docker
```shell
docker load -i path/to/image/ai4europeana-subplayer.tar
# Check that you succesfully loaded the image
docker image ls -a

# Run the docker image
docker run \
  -e VITE_APP_TITLE=ReactStarter \
  -e VITE_API_ENDPOINT= \
  -e VITE_OPEN_SOURCE_URL= \
  ai4europeana-subplayer
```

# Backend

### Start Docker
```shell
docker load -i path/to/image/ai4europeana-backend.tar
# Check that you succesfully loaded the image
docker image ls -a

# Run the docker image
# Remember to fill all the envs
docker run \
  -e PORT=80 \
  -e HOST=0.0.0.0 \
  -e NODE_ENV=development \
  -e APP_KEY= \
  -e APP_NAME= \
  -e DRIVE_DISK=local \
  -e CACHE_VIEWS= \
  -e STORAGE_DISK= \
  -e FRONTEND_URL= \
  -e S3_KEY= \
  -e S3_SECRET= \
  -e S3_BUCKET= \
  -e S3_REGION= \
  -e S3_ENDPOINT= \
  -e S3_CLOUDFRONT_URL= \
  -e DB_CONNECTION= \
  -e DB_HOST= \
  -e DB_PORT= \
  -e DB_DATABASE= \
  -e DB_USERNAME= \
  -e DB_PASSWORD= \
  -e SMTP_HOST= \
  -e SMTP_PORT= \
  -e SMTP_USERNAME= \
  -e SMTP_PASSWORD= \
  -e SMTP_SENDER= \
  -e FBK_API_URL= \
  -e PRIVATE_EVENT_SECRET= \
  -e PRIVATE_JOB_SECRET= \
  -e EVENT_INVITATION_EXPIRES_AFTER_HOURS=24 \
  -e INVITE_TOKEN_EXPIRE_AFTER_HOURS=24 \
  -e EUROPEANA_ENDPOINT_API=https://api.europeana.eu/record/v2/search.json \
  -e EUROPEANA_ENDPOINT_API_KEY= \
  -e EUROPEANA_CLIENT_ID= \
  -e EUROPEANA_CLIENT_SECRET= \
  -e EUROPEANA_API_KEY= \
  -e EUROPEANA_TOKEN_SECRET= \
  ai4europeana-backend
```

### Essential Envs in order to run the project with the open source version

```dotenv
### Essential Adonis Envs:
PORT=80
HOST=0.0.0.0
NODE_ENV=development/staging/production
APP_KEY=UUID
APP_NAME=
DRIVE_DISK=local
CACHE_VIEWS=true/false
STORAGE_DISK=local/s3

FRONTEND_URL=

S3_KEY=
S3_SECRET=
S3_BUCKET=
S3_REGION=
S3_ENDPOINT=
S3_CLOUDFRONT_URL=

DB_CONNECTION=
DB_HOST=
DB_PORT=
DB_DATABASE=
DB_USERNAME=
DB_PASSWORD=

SMTP_HOST=
SMTP_PORT=
SMTP_USERNAME=
SMTP_PASSWORD=
SMTP_SENDER=

FBK_API_URL=

PRIVATE_EVENT_SECRET=
PRIVATE_JOB_SECRET=

EVENT_INVITATION_EXPIRES_AFTER_HOURS=24
INVITE_TOKEN_EXPIRE_AFTER_HOURS=24

EUROPEANA_ENDPOINT_API=https://api.europeana.eu/record/v2/search.json

EUROPEANA_ENDPOINT_API_KEY= # Api key for 'https://api.europeana.eu/record/v2/search.json' endpoint

EUROPEANA_CLIENT_ID=
EUROPEANA_CLIENT_SECRET=
EUROPEANA_API_KEY=
EUROPEANA_TOKEN_SECRET=
```

### Optional Envs with default or nullable values

```dotenv
EUROPEANA_OPENID_SCOPE='openid email profile annotations'
EUROPEANA_OPENID_REALM_URL='https://auth.europeana.eu/auth/realms/europeana'
EUROPEANA_OPENID_RESOURCE='https://auth.europeana.eu/auth/realms/europeana/protocol/openid-connect'
EUROPEANA_ANNOTATIONS_URL=https://annotation-api.acceptance.eanadev.org/annotation/

EUROPEANA_ENDPOINT_API=https://api.europeana.eu/record/v2/search.json

SUB_PLATFORM=subplayer (subplayer/matesub)

MATESUB_KEY=
MATESUB_URL=
MATESUB_API_USER_EMAIL=

SENTRY_DSN=
SENTRY_ENVIRONMENT= (development/staging/production)
```
