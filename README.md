# Ruby-on-Rails Getting Started with Docker-Compose

This project implements all the steps from
[Getting Started with Rails](https://guides.rubyonrails.org/v4.2/getting_started.html)(v4.2)
and [Quickstart: Compose and Rails](https://docs.docker.com/compose/rails/).

In addition to that, a due care is taken about the developer experience in Linux,
and the local user is considered,
see e.g. [this](https://dev.to/acro5piano/specifying-user-and-group-in-docker-i2e) article.

Docker and docker-compose need to be installed in order to take advantage of the dockerized development environment.

After cloning this repository, the project can be run as follows.

Export the local user values this way:
```
$ export UID=${UID}
$ export GID=${GID}
```
These variables will be used to ensure that the files created in the Rails container belong to the local user.

One can start the project this way:
```
$ docker-compose up
```

It is also possible to do various things inside the Rails container like this:
```
$ docker-compose exec web rake db:create
$ docker-compose exec web rake db:migrate
$ docker-compose exec web rails g controller welcome index
```
A clean way to shutdown the project would be to run
```
$ docker-compose down
```
(in a separate terminal).

## Known issues:

### "FATAL: could not open file "global/pg_filenode.map" Permission denied"

This erro may occurr at the first run.
In such case, 
```
$ docker-compose run db bash
root@:/# rm -rf /var/lib/pgsql/data
root@:/# exit
```
 (to be investigated)
