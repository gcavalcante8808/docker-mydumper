MyDumper
--------

This is a gcavalcante8808/mydumper docker image based no alpine 3.6 and Percona MyDumper.

Supported Tags and respective Docker Links
------------------------------------------

 * mydumper 0.9.1 (([mydumper0.9.1/Dockerfile](https://github.com/gcavalcante8808/docker-mydumper/blob/0.9.1/Dockerfile)))

How to see it In Action
-----------------------

You can use ([docker-compose](https://docs.docker.com/compose/install/)) to spin up a MySQL Server and the mysqldumper using the docker-compose.yml file provided in this project in the following way:

```
mkdir test && cd test
wget https://raw.githubusercontent.com/gcavalcante8808/docker-mysqldumper/master/docker-compose.yml
docker-compose up
```

The container for mydumper will start, create the backup then exit with status 0. (You can see the exit code with `docker ps` and logs with `docker logs <CONTAINER>`.

The backups are created with --compress and in the following folder pattern:

<BACKUP_FOLDER>/<DB_NAME>-<DATE>


Needed Environment Variables
----------------------------

The container uses the following environment variables (theh bold ones are **required**) :

 * **DB_HOST**: the IP or hostname of the mysql Server;
 * DB_USER: a user with 'RELOAD' privilege. If not provided, assumes root;
 * DB_NAME: the name of the db that will be saved. Same value as DB_USER if not provided;
 * **DB_PASSWORD**: the password for the user.

S3_SUPPORT
----------

S3 Endpoints are now supported! You need to provide the following env vars:

 * S3_ACCESS_KEY_ID
 * S3_SECRET_ACCESS_KEY
 * S3_ENDPOINT_URL
 * S3_BUCKET
 
The entrypoint will check the existence of 'S3_ACESS_KEY_ID' and will proceed with s3 backup and backup_folder removal.

The support is provided by the Minio Client, check the https://github.com/minio/mc for more details.

The container was tested against a MinioServer and a DigitalOcean Space.

ROADMAP
-------

The Following features mark the roadmap for a more usefull (Aka 1.0) version:

 * DCron support for schedules;
 * Backup All Databases instead of just one.
 * Send Job Status to Prometheus Gateway or Prometheus Aggregate Gateway.
 * Json Logs;
 * WebHooks.

Author
------

Author: Gabriel Abdalla Cavalcante Silva (gabriel.cavalcante88@gmail.com)
