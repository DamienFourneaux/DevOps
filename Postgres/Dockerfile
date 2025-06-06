FROM postgres:17.2-alpine

ENV POSTGRES_DB=db \
   POSTGRES_USER=usr \
   POSTGRES_PASSWORD=pwd

COPY postgres-data /docker-entrypoint-initdb.d/

# Define the environment variable for the database
# Define the environment variable for the user
# Define the environment variable for the password
# Copy the SQL scripts to the initialization directory
# The scripts in this directory will be executed in alphabetical order
# when the container is started for the first time
# The scripts can be used to create tables, insert data, etc.
# The scripts can also be used to create the database and user