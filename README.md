# Clone repositories

```bash
bash clone_repositories.sh
```

# Edit environmental variables

```bash
cp labcode-web-app/app/.env.example labcode-web-app/app/.env
```

edit `.env`

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

# Access

lab-sim api: http://localhost:8080/docs

log-server api: http://localhost:8000/docs

web app: http://localhost:5173/