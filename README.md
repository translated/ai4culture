# Ai4Europeana Application
Repository containing the docker images for europeana Backend and Frontends

## Requirements
1. `Mysql` database for the backend
2. `S3` bucket for file saving
3. `Smtp` server for sending emails
4. `FBK` for subtitle generation
5. For the sign-in with europeana you must have the credentials from `Europeana` to enable `SSO`

## Components
- [Frontend](#frontend) - Main webapp client for europeana
- [Sub-player](#sub-player) - Platform for video subtitling
- [Backend](#backend) - Handles the data for both the main client and the sub-player

## Frontend 
- [link-zip](https://github.com/humanstech/ai4europeana/releases/download/v0.1.2/ai4europeana-fe.zip) The zip contains the source code for the frontend client

### Start Docker
1. unzip the file
2. run the following command in the unzipped folder
```shell
sh build_and_deploy.sh <app_name> <api_url> <port>

# Example 
sh build_and_deploy.sh Ai4Europeana http://api.europeana.com 3000
```
3. This will build the docker image and run it on the specified port
4. The frontend is server by an nginx server and can be accessed on `http://localhost:<port>`

## Sub-player 
- [link-zip](https://github.com/humanstech/ai4europeana/releases/download/v0.1.2/ai4europeana-subtitler.zip) (platform for video subtitling) The zip contains the source code for the frontend sub-player

### Start Docker
1. unzip the file
2. run the following command in the unzipped folder
```shell
sh build_and_deploy.sh <api_url> <port>

# Example
sh build_and_deploy.sh http://api.europeana.com 3001
```
3. This will build the docker image and run it on the specified port
4. The sub-player is server by an nginx server and can be accessed on `http://localhost:<port>`

## Backend 
- [link-docker-image-registry](public.ecr.aws/k2u7h0h2/humans-europeana-backend)
- Handles the data for both the main client and the sub-player

### Start Docker
```shell
# You can run the backend docker image with the following command
# Remember to fill each env placeholder with the correct value
docker run \
    -p 80:80 \
    -e PORT=80 \
    -e HOST=0.0.0.0 \
    -e NODE_ENV=development \
    -e APP_KEY=your16charappkey \
    -e APP_NAME=yourappname \
    -e DRIVE_DISK=local \
    -e CACHE_VIEWS=true \
    -e STORAGE_DISK=s3 \
    -e FRONTEND_URL=yourfrontendurl \
    -e ACCESS_TOKEN_SECRET=youraccesstokensecret \
    -e ACCESS_TOKEN_EXPIRE_IN=1d \
    -e ACCESS_TOKEN_EXPIRE_AFTER_DAYS=1 \
    -e REFRESH_TOKEN_SECRET=yourrefreshtokensecret \
    -e REFRESH_TOKEN_EXPIRE_IN=1w \
    -e REFRESH_TOKEN_EXPIRE_AFTER_WEEKS=1 \
    -e S3_KEY=yours3key \
    -e S3_SECRET=yours3secret \
    -e S3_BUCKET=yours3bucket \
    -e S3_REGION=yours3region \
    -e S3_CLOUDFRONT_URL=yours3cloudfronturl \
    -e DB_CONNECTION=mysql \
    -e DB_HOST=yourdbhost \
    -e DB_PORT=3306 \
    -e DB_DATABASE=yourdatabase \
    -e DB_USERNAME=yourdbusername \
    -e DB_PASSWORD=yourdbpassword \
    -e SMTP_HOST=yoursmtpserver \
    -e SMTP_PORT=587 \
    -e SMTP_USERNAME=yoursmtpusername \
    -e SMTP_PASSWORD=yoursmtppassword \
    -e SMTP_SENDER=yoursmtpsender \
    -e FBK_API_URL=yourfbkapiurl \
    -e PRIVATE_EVENT_SECRET=yourprivateeventsecret \
    -e PRIVATE_JOB_SECRET=yourprivatejobsecret \
    -e EVENT_INVITATION_EXPIRES_AFTER_HOURS=1 \
    -e INVITE_TOKEN_EXPIRE_AFTER_HOURS=1 \
    -e EUROPEANA_ENDPOINT_API_KEY=youreuropeanaapikey \
    -e EUROPEANA_CLIENT_ID=youreuropeanaclientid \
    -e EUROPEANA_CLIENT_SECRET=youreuropeanaclientsecret \
    -e EUROPEANA_TOKEN_SECRET=youreuropeanatokensecret \
    public.ecr.aws/k2u7h0h2/humans-europeana-backend:v1.1.2

  # You can also create a .env file with the following content and run the docker image with the following command
  docker run -e-file .env public.ecr.aws/k2u7h0h2/humans-europeana-backend:v1.1.2
```

### Essential Envs in order to run the backend

```dotenv
### Essential backend Envs:
PORT=80
HOST=0.0.0.0
NODE_ENV=development/staging/production
APP_KEY= # Must be 16 characters long
APP_NAME=
DRIVE_DISK=local
CACHE_VIEWS=true/false
STORAGE_DISK=s3

FRONTEND_URL=

# JWT configuration
ACCESS_TOKEN_SECRET=
ACCESS_TOKEN_EXPIRE_IN=1d
ACCESS_TOKEN_EXPIRE_AFTER_DAYS=1
REFRESH_TOKEN_SECRET=
REFRESH_TOKEN_EXPIRE_IN=1w
REFRESH_TOKEN_EXPIRE_AFTER_WEEKS=1

# AWS S3 connection configuration
S3_KEY=
S3_SECRET=
S3_BUCKET=
S3_REGION=
S3_CLOUDFRONT_URL=

# Database configuration (The backend was developed using MySQL)
DB_CONNECTION=mysql
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
SMTP_SENDER= # Email address used to send emails

# FBK endpoint used to generate automatically subtitles for a video in the desired target languages
FBK_API_URL=

# Used to generate the hash that allows to access a private event or video
PRIVATE_EVENT_SECRET=
PRIVATE_JOB_SECRET=

# After how many hours the event invitation will expire
EVENT_INVITATION_EXPIRES_AFTER_HOURS=

# After how many hours the invite token will expire
INVITE_TOKEN_EXPIRE_AFTER_HOURS=

# Authentification detail to access the europeana records api (https://api.europeana.eu/record/v2/search.json)
EUROPEANA_ENDPOINT_API_KEY=

# Openid details to enable SSO with the europeana provider
EUROPEANA_CLIENT_ID=
EUROPEANA_CLIENT_SECRET=
EUROPEANA_TOKEN_SECRET= # Used to encrypt europeana tokens, can be any string
```

### Optional Envs with default or optional values
```dotenv
# Misc configuration for europeana integration
EUROPEANA_OPENID_SCOPE='openid email profile annotations'
EUROPEANA_OPENID_REALM_URL='https://auth.europeana.eu/auth/realms/europeana'
EUROPEANA_OPENID_RESOURCE='https://auth.europeana.eu/auth/realms/europeana/protocol/openid-connect'
EUROPEANA_ANNOTATIONS_URL=https://annotation-api.acceptance.eanadev.org/annotation/

# Used to retrieve videos from the europeana platform
EUROPEANA_ENDPOINT_API=https://api.europeana.eu/record/v2/search.json

# Used for server errors monitoring
SENTRY_DSN=
SENTRY_ENVIRONMENT=(development/staging/production)
```
