# Clone repositories

Move into `labcode-test-environment` directory, run

```bash
bash clone_repositories.sh
```

Then, these repository is cloned:

1. `labcode-sim`
2. `labcode-log-server`
3. `labcode-web-app`

# Edit environmental variables

Copy template file with following command:

```bash
cp labcode-web-app/app/.env.example labcode-web-app/app/.env
```

Then, edit `.env` and replace `your-google-client-id.apps.googleusercontent.com` with correct client ID.

# Build containers

```bash
docker compose build
```

# Run containers

```bash
docker compose up -d
```

# (Only first time) setup database

```bash
docker compose exec log_server sh -c "python -m define_db.models"
```

# Access

lab-sim api: http://localhost:8080/docs

log-server api: http://localhost:8000/docs

web app: http://localhost:5173/