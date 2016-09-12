# Docker Compose for Wildfly (running RBAC Authentication Service) + Postgres

## Running instructions

	docker-compose up -d

The REST interface should be available at:

	http://localhost:8443/services

And you should be able to get the RBAC version accessing:

	http://localhost:8443/service/auth/version

## IMPORTANT

If you are running the server locally, do:

	> sudo vim /etc/hosts

Append the following line to file:

	127.0.0.1 rbac-auth-services

This is needed as the REST Web Service needs
to be addresses with the exact the same name
as "rbac-auth-services", but if the server is
running locally we must associate this name with
localhost.
