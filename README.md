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

## 7. Create user

1. Access to http://localhost:8000/docs#/users/create_users__post
2. Click "Try it out"
3. Enter email address to "email"
4. Click "Execute"
5. You will obtain response as follows:
```
{
  "id": 1,
  "email": "example@gmail.com"
}
```
6. Memo the value of "id" as user ID

## 8. Create Project

1. Access to http://localhost:8000/docs#/projects/create_projects__post
2. Click "Try it out"
3. Enter project name to "name"
4. Enter user ID obtained at user creation to "user_id"
5. Click "Execute"
6. You will obtain response as follows:

```{
  "id": 1,
  "name": "test_project",
  "user_id": 1,
  "created_at": "2025-02-25T10:44:18.911007",
  "updated_at": "2025-02-25T10:44:18.911017"
}
```
6. Memo the value of "id" as project ID.

## 9. Run experiment

1. Access to http://0.0.0.0:8080/docs#/default/run_experiment_run_experiment_post
2. Click "Try it out"
3. Enter project ID obtained at project creation to "project_id"
4. Enter protocol name to "protocol_name"
5. Enter user ID obtained at user creation to "user_id"
5. Click "Execute"

## 10. Access to Experiment tracking UI

Access to http://localhost:5173/