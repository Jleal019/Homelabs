Requires: PostgreSQL, guacd, and guacamole frontend

For some reason, this docker-compose doesn't like to have quoted usernames.

PostgreSQL:
  
  -MUST be manually initialized with install script initdb.sql
  -access with psql
  -consider running all 3 services in the same container.
  -Problems will occur if initializing docker image with existing data
  -Initialize User by logging in to guacamole_db and 
   running the follow:
    CREATE USER guac WITH PASSWORD 'd5TtV93P';
    GRANT SELECT,INSERT,UPDATE,DELETE ON ALL TABLES IN SCHEMA public TO guac;
    GRANT SELECT,USAGE ON ALL SEQUENCES IN SCHEMA public TO guac;
  -RUN WITH THE FOLLOWING COMMAND to initialize DB psql -U username -d guacamole_db -a -f myInsertFile
  -Basic psql commands:
    \l lists databases
    \dt list database tables
    \dn list all schemas
    \du list users
  -To test Postgres connection from remote client: install postgres and use the following command
  psql -h <REMOTE HOST> -p <REMOTE PORT> -U <DB_USER> <DB_NAME>
  - To find Postgresql conf file use the command psql -U postgres -c 'SHOW config_file'
  -Ensure `pg_hba.conf` is configured correctly in `/var/lib/postgresql/data`
  -Ensure the line `listen_addresses` is configured correctly in the postgresql.conf file

guacD:

  -listening on port 4822 by default.
  -Must have access to the network with your desired hosts 
  -Changes need to be made to allow Docker host to be accessible. 

guacamole:

  -accessible at http://HOSTNAME:8080/guacamole/
