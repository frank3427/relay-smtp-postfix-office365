Postfix Mail Relay
======================

Contains:

* Postfix, running in a simple relay mode
* RSyslog

Processes are managed by supervisord, including cronjobs

The container provides a simple proxy relay for local environments where you can have private servers without an Internet connection and, therefore, without access to external mail retransmissions. You must provide the container with your external mail relay address and your credentials. The configuration is done on Office 365, but it can work with any type of server.


Exports
-------

* Postfix on `25`

Variables
---------

* `RELAY_HOST_NAME=relay.example.com`: A DNS name for this relay container (usually the same as the Docker's hostname)
* `ACCEPTED_NETWORKS=192.168.0.0/16 172.16.0.0/12 10.0.0.0/8`: A network (or a list of networks) to accept mail from
* `EXT_RELAY_HOST=smtp.office365.com`: External relay DNS name
* `EXT_RELAY_PORT=587`: External relay TCP port
* `SMTP_LOGIN=`: Login to connect to the external relay (required, otherwise the container fails to start)
* `SMTP_PASSWORD=`: Password to connect to the external relay (required, otherwise the container fails to start)
* `USE_TLS=`: Remote require tls. Might be "yes" or "no". Default: no.
* `TLS_VERIFY=`: Trust level for checking the remote side cert. (none, may, encrypt, dane, dane-only, fingerprint, verify, secure). Default: may.

Example
-------

Launch Postfix container:

    $ docker run -d -h my-host-relay.example.com --name="my-host-relay" -e SMTP_LOGIN=username-for-relay-office365 -e SMTP_PASSWORD=password-office365 -p 25:25 denispaiva/relay-smtp-postfix-office365
