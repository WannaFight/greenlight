# Greenlight

## Setup
Copy env and populate with data:
```shell
cp .env.template .env
```
For database DSN use somethong like this:
```shell
DB_DSN=postgres://username:password@localhost/databse?sslmode=disable
```

Install additional packages:
```shell
go install github.com/cosmtrek/air@latest  # for live reload
brew install golang-migrate
brew install pre-commit  # style check
pre-commit install
```

Run containers:
```shell
docker compose up -d
docker compose ps  # everything has to be up and running
```

Connect to database using `docker compose exec db psql -U postgres`. Following commands might raise an exception that something is already exists – it's ok:
```shell
CREATE DATABASE greenlight;
CREATE ROLE greenlight WITH LOGIN PASSWORD 'password';
CREATE EXTENSION IF NOT EXISTS citext;
```

Apply migrations. Value of `database` option is `DB_DSN` from environment:
```shell
migrate -path=./migrations -database="postgres://greenlight:password@localhost/greenlight?sslmode=disable" up
```

## Todos
[ ] add init sql (role creation etc) to docker compose\
[ ] move golang with air to docker\
[ ] apply migration inside docker
