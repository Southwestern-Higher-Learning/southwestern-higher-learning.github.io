# Structure of the Backend

```
TutorAppBackend/
├── .github/
│   └── workflows/
│       ├── main.yml
│       └── pl.yml
├── project/
│   ├── app/
│   │   ├── api/
│   │   │   ├── <various python files>
│   │   │   └── <create new routes in this folder>
│   │   ├── migrations/
│   │   │   └── models/
│   │   │       └── <various SQL files>
│   │   ├── models/
│   │   │   ├── pydnatic.py
│   │   │   ├── tortoise.py  -- Define new models for TortoiseORM
│   │   │   └── utils.py
│   │   ├── config.py   -- Other configuration shouldn't need
│   │   ├── db.py       -- configure database connection
│   │   └── main.py     -- Setup routes and extensions, and start
│   ├── db/
│   │   └── <files for local database development>
│   ├── .coverage
│   ├── .coveragerc
│   ├── .dockerignore
│   ├── .flake8
│   ├── .isort.cfg
│   ├── aerich.ini
│   ├── Dockerfile        -- Dockerfile for local development
│   ├── Dockerfile.prod   -- Dockerfile for production, build and push to another registry
│   ├── entrypoint.sh
│   ├── rquirements.txt
│   └── setup.cfg
├── .env
├── docker-compose.yml
└── tutorappcreds.json     -- If using Cloud SQL Proxy
```