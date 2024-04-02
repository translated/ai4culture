# Ai4Europeana Application
Repository containing the docker images for europeana Backend and Frontends

# Frontend [link-docker](https://github.com/humanstech/ai4europeana/releases/download/v0.1.0-alpha/ai4europeana-frontend.tar)

### Start Docker
```shell
docker load -i path/to/image/ai4europeana-frontend.tar
# Check that you succesfully loaded the image
docker image ls -a

# Run the docker image
docker run \
  -e VITE_APP_TITLE= \
  -e VITE_API_ENDPOINT= \
  -e VITE_OPEN_SOURCE_URL= \
  ai4europeana-frontend
```

`VITE_APP_TITLE`: used to define the react app title

`VITE_API_ENDPOINT`: the *backend* endpoint

`VITE_OPEN_SOURCE_URL`: endpoint to the *subplayer*

# Subplayer [link-docker](https://github.com/humanstech/ai4europeana/releases/download/v0.1.0-alpha/ai4europeana-subplayer.tar) (platform for video subtitling)

### Start Docker
```shell
docker load -i path/to/image/ai4europeana-subplayer.tar
# Check that you succesfully loaded the image
docker image ls -a

# Run the docker image
docker run \
  -e VITE_APP_ENDPOINT= \
  ai4europeana-subplayer
```

`VITE_APP_ENDPOINT`: the *backend* endpoint

# Backend [link-docker](https://github.com/humanstech/ai4europeana/releases/download/v0.1.0-alpha/ai4europeana-backend.tar)

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

### Essential Envs in order to run the backend with explanation

```dotenv
### Essential Adonis Envs:
PORT=80
HOST=0.0.0.0
NODE_ENV=development/staging/production
APP_KEY=
APP_NAME=
DRIVE_DISK=local
CACHE_VIEWS=true/false
STORAGE_DISK=local/s3

# Frontend endpoint
FRONTEND_URL=

# AWS S3 connection configuration
S3_KEY=
S3_SECRET=
S3_BUCKET=
S3_REGION=
S3_ENDPOINT=
S3_CLOUDFRONT_URL=

# Database configuration
DB_CONNECTION=
DB_HOST=
DB_PORT=
DB_DATABASE=
DB_USERNAME=
DB_PASSWORD=

# SMTP server configuration (Used for sending emails)
SMTP_HOST=
SMTP_PORT=
SMTP_USERNAME=
SMTP_PASSWORD=
SMTP_SENDER=

# FBK endpoint used to generate automatically subtitles for a video in the desired target languages
FBK_API_URL=

# Used to generate the hash that allows to access a private event or video
PRIVATE_EVENT_SECRET=
PRIVATE_JOB_SECRET=

EVENT_INVITATION_EXPIRES_AFTER_HOURS=24
INVITE_TOKEN_EXPIRE_AFTER_HOURS=24

# Used to retrieve videos from the europeana platform
EUROPEANA_ENDPOINT_API=https://api.europeana.eu/record/v2/search.json

# Api key for 'https://api.europeana.eu/record/v2/search.json' endpoint
EUROPEANA_ENDPOINT_API_KEY= 

# Openid details to enable SSO with the europeana provider
EUROPEANA_CLIENT_ID=
EUROPEANA_CLIENT_SECRET=
EUROPEANA_API_KEY=
EUROPEANA_TOKEN_SECRET=
```

### Optional Envs with default or nullable values

```dotenv
# Used for SSO login with the europeana provider
EUROPEANA_OPENID_SCOPE='openid email profile annotations'
EUROPEANA_OPENID_REALM_URL='https://auth.europeana.eu/auth/realms/europeana'
EUROPEANA_OPENID_RESOURCE='https://auth.europeana.eu/auth/realms/europeana/protocol/openid-connect'
EUROPEANA_ANNOTATIONS_URL=https://annotation-api.acceptance.eanadev.org/annotation/

SENTRY_DSN=
SENTRY_ENVIRONMENT= (development/staging/production)
```
