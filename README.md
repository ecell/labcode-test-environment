# How to setup
## 1. Clone this repository

Clone this repository with following command:

```bash
git clone git@github.com:fuku-inc/labcode-test-environment.git
```

## 2. Clone service repositories

Move into `labcode-test-environment` directory, run

```bash
bash clone_repositories.sh
```

Then, these repository is cloned:

1. `labcode-sim`
2. `labcode-log-server`
3. `labcode-web-app`

## 3. Edit environmental variables

Copy template file with following command:

```bash
cp labcode-web-app/app/.env.example labcode-web-app/app/.env
```

Then, edit `labcode-web-app/app/.env` and replace `your-google-client-id.apps.googleusercontent.com` with correct client ID.

## 4. Build containers

```bash
docker compose build
```

## 5. Run containers

```bash
docker compose up -d
```

## 6. (Only first time) setup database

```bash
docker compose exec log_server sh -c "python -m define_db.models"
```

## 7. Access each service

lab-sim api: http://localhost:8080/docs

log-server api: http://localhost:8000/docs

web app: http://localhost:5173/