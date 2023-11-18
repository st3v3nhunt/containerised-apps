# Postgres

> A docker-compose setup for running [Postgres](https://www.postgresql.org/)
> and [pgAdmin](https://www.pgadmin.org/)

## Usage

Run `docker-compose up --build` to start both Postgres and pgAdmin. After
several seconds the pgAdmin web interface will be available on
[localhost:5431](http://localhost:5431). Login with the credentials as
specified in [.env](.env).

### Connecting pgAdmin to DB

Once pgAdmin is running the connection to the DB can be made. Find the option
to 'Add New Server'. A number of fields need to be completed:

| Section    | Field               | Description                                                                                                              |
| -------    | -----               | -----------                                                                                                              |
| General    | Name                | Something useful like 'dev'                                                                                              |
| Connection | Host name / address | The name of the container for `pg_db` in [docker-compose.yml](docker-compose.yml) -OR- the IP address of the container^1 |
| Connection | Username            | Value of `POSTGRES_USER` from [.env](.env)                                                                               |
| Connection | Password            | Value of `POSTGRES_PASSWORD` from [.env](.env)                                                                           |

NOTE:
**^1** - the IP address of the container can be found by
[executing](https://docs.docker.com/engine/reference/commandline/exec/)
`hostname -I` in the container i.e.
`docker exec <contianer_name> /bin/sh -c "hostname -I"`

## Use of `latest`

Both postgres and pgAdmin containers are set to use the `latest` tag. This
isn't necessarily a good idea and if this was going to be used in a project I'd
advise a specific version be used. Having it set to `latest` in this repo saves
updating it.

## Data storage

The DB has been configured to use a local directory to store data, specifically
`./data`. It might be beneficial to change the directory in which case it is as
simple as updating the path (to one that exists, or will exist e.g.
`$HOME/data/postgres`.

Removing `volumes` will default the container to using the docker managed
volumes. This is a good option if you aren't going to be accessing the data
directly. More information
[here](https://github.com/docker-library/docs/blob/master/postgres/README.md#where-to-store-data).

## References

* [postgres container](https://github.com/docker-library/docs/blob/master/postgres/README.md)
* [pgAdmin container deployment](https://www.pgadmin.org/docs/pgadmin4/latest/container_deployment.html)
