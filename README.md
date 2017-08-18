# Docker Compose for Wildfly (running RBAC Authentication Service) + Postgres

## Running instructions

Insert your LDAP CREDENTIALS in the following file: env-vars/rbac-wildfly-vars.env

    LDAP_CREDENTIALS=<INSERT_YOUR_LDAP_CREDENTIALS_HERE>

Start service

	docker-compose up -d

The REST interface should be available at:

	http://localhost:8443/service

And you should be able to get the RBAC version accessing:

	http://localhost:8443/service/auth/version

## Systemd Integration

To integrate this as a systemd service, do:

    make install

To remove the systemd service and its additional files:

    make uninstall

## Host IP mapping

The RBAC images have the following names:

  - RBAC management studio: sirius-rbac.lnls.br
  - RBAC auth services: sirius-rbac-auth.lnls.br

If running on the same host, with the same
docker network, the mapping must be the internal
docker IP, such as 172.18.0.3. This is necessary
as the port mapping between the container/host
might change and the docker DNS services knows
how to deal with this. If running on the same,
but the actual IP is used, the docker DNS service
will not be used and the services will try to
use the actual specified port, which could be
incorrect due to container/host port mapping.

So, in summary, if running services on the same
host, use

  extra_hosts:
    - "sirius-rbac.lnls.br:172.18.0.3"
    - "sirius-rbac-auth.lnls.br:172.18.0.4"

where 172.18.0.3 and 172.18.0.4 are the internal
docker IPs

If running the services on different host, just use
the destination IPs.

## IMPORTANT

If you are running the server locally, do:

	> sudo vim /etc/hosts

Append the following line to file:

	127.0.0.1 rbac-auth-services

    or


	127.0.0.1 sirius-rbac.lnls.br

This is needed as the REST Web Service needs
to be addresses with the exact the same name
as "rbac-auth-services" or "sirius-rbac.lnls.br",
but if the server is running locally we must
associate this name with localhost.
