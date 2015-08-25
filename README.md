###PG DUMP ON DOCKER
---

This Dockerfile is ``debian:jessie``, the version that is compatible with ``postgres 9.4+``. The following is a list of image names and their corresponding postgres version.

	wheezy (oldstable) 	9.1+134
	jessie (stable)   	9.4+165
	stretch (testing) 	9.4+169
	sid (unstable) 			9.4+169
	
Check out this link to find out more about different versions and their images

	https://packages.debian.org/search?keywords=postgresql-client

First, let's build the container

	docker build -t pg_dump .

We just tagged this container as ``pg_dump`` using the ``-t`` flag.

Currently my postgres container has an alias of ``db``. What is an alias? In the ``--link``, the second input (after colon), is the ``alias``

	docker run -it --link db:db pg_dump -U postgres -h db -d mydb_production >> mydb_prod.sql

In other words, this command will still work if I changed it to,

	docker run -it --link postgres:db pg_dump -U postgres -h db -d mydb_production >> mydb_prod.sql

That is assuming I named my container ``postgres`` (right before the colon in ``postgres:db``). The format goes like this: ``<name_of_container:alias_of_container>``

