# Summary
This guide provides instructions for:
* Installing Postgres on Ubuntu 20.04
* Configuring an indexing database for use with Graph
* Configuring an agent database for use with the Graph agent and service
* Making sure the database is accessible on the local network

## Acknowledgements and Disclaimer
The contents of this guide has been pulled together from a variety of sources. It has been tested on Ubuntu Server 18.04 and 20.04. Your mileage may vary. Most of the Postgres install detail has been pulled from koen84's install scripts and edited for manual installation - https://github.com/koen84/Graph-tools/blob/master/install/postgres.sh

## Prerequisites
First and foremost, it is assumed that you have decided on your architecture per the earlier part of this guide series - VMs or containers, storage sizing and redundancy, Eth node choice. At all times, this guide will use the reference architecture from the first page for all instructions. This guide is not intended for absolute beginners. It assumes some knowledge of using a linux terminal. Before you get started you will need to have your Ubuntu server instance up and running and up to date. Your server will require an internet connection. This guide assumes that you are logged into the server using a non-root account with SUDO access. Security will not be covered in this guide.

Additional packages that may need to be installed:
gnupg - `sudo apt-get install gnupg`

It is assumed that the latest stable version of Postgres will be installed. At time of writing this guide that is Postgres13.


# Install Postgres
Firstly, add the Postgres repo to package sources

`sudo su -c "echo 'deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main' > /etc/apt/sources.list.d/pgdg.list"`

```wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - && sudo apt-get update && sudo apt-get install -y postgresql```

If the install is successful you should see a confirmation message:

```
Success. You can now start the database server using:

    pg_ctlcluster 13 main start
```

## Configure the postgres database user
`sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'changeme';"` Set the password "changeme" as you see fit and make a note of it

## Create databases
`sudo -u postgres createdb graph-node`

`sudo -u postgres createdb graph-agent`

## Configure Postgres for remote access
If your database will be accessed remotely, you need to update the Postgres configuration to allow connections from remote hosts:

Open `/etc/postgresql/13/main/postgresql.conf` in an editor, find `#listen_addresses = 'localhost'` and change it to `listen_addresses = '*'` (or if you have very specific interfaces that will allow access the database, you can use those instead for additional security)

Open `/etc/postgresql/13/main/pg_hba.conf` in an editor and add `host  all  all 0.0.0.0/0 md5` to the top of the file. Again, if you want to restrict scope to specific subnets or IP addresses you can choose to do so here for additional security.

Restart the Postgres service so changes take effect. `sudo systemctl restart postgresql@13-main.service`

## Test database remote access
From another server, run a quick telnet test to check that the database server is now responding on the postgres port:
`telnet <postgresServer> 5432`

If succesfully connected, the output should look something like:
```
$ telnet graphpostgres-0 5432
Trying 192.168.10.12...
Connected to graphpostgres-0.localdomain.
Escape character is '^]'.
```

If you get a timeout error, it is likely your database is not open to the rest of your network.

