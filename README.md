# **PgBouncer**
Here's [why you'd use it](https://www.percona.com/blog/2018/06/27/scaling-postgresql-with-pgbouncer-you-may-need-a-connection-pooler-sooner-than-you-expect/) and here's [where you can read more about it](https://github.com/bitnami/containers/tree/main/bitnami/pgbouncer#configuration).

The only real purpose of this repo is to document how PgBouncer is configured and run with Docker as well as make it easy to test changes locally before propogating changes to its production environment (ie Google Cloud Run Services or AWS ECS/EC2).

## **Get Up and Running**
#### **Install Docker:**
[Docker for Desktop](https://docs.docker.com/desktop/mac/install/)

#### **Create Postgres Volume:**
```sh
$ docker volume create --name postgres_data
```

#### **Run It:**
```sh
$ docker-compose up
```

#### **PSQL:**
Add the following to `~/.pg_service.conf`:
```conf
[pgbouncer]
host=localhost
port=6432
dbname=postgres
user=postgres
password=password
```
and run:
```sh
$ psql service=pgbouncer
```

## **Configuration**
Configuration is done via environment variables in `docker-compose.yml`.

## **Deployment**
There's no real need to setup automatic deploys since PgBouncer is more of a "set it and forget it" type thing. However, you could automate deployments via a bash script or CI/CD pipeline that runs the CLI commands as opposed to opening Google Cloud Console or AWS Console and making updates manually.

How you automate it will depend on where it's hosted.
