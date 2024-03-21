# EASY GUACAMOLE SETUP

## COPY REPO and run below commands:

## For production remember to change env variables.
## Default login/pass to guacamole is guacadmin/guacadmin

```
docker pull guacamole/guacamole
```

```
MSYS_NO_PATHCONV=1 docker run --rm guacamole/guacamole /opt/guacamole/bin/initdb.sh --postgresql > initdb.sql
```

```
docker compose up -d guacdb
```

```
docker cp initdb.sql guacamoledb:/initdb.sql
docker exec -it guacamoledb bash
```
Inside container:
```
psql -U $POSTGRES_USER -c "CREATE DATABASE $POSTGRES_DATABASE;"
cat initdb.sql | psql -U $POSTGRES_USER -d $POSTGRES_DATABASE
exit
```

```
docker compose down
docker compose up -d
```