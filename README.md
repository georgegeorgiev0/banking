# banking
##### Download dependencies and run the application
```
./start.sh
```
To run the application, you have to define the environment variables, default values of the variables are defined inside `start.sh`

```
- SERVER_ADDRESS    `[IP Address of the machine]`
- SERVER_PORT       `[Port of the machine]`
- DB_USER           `[Database username]`
- DB_PASSWD         `[Database password]`
- DB_ADDR           `[IP address of the database]`
- DB_PORT           `[Port of the database]`
- DB_NAME           `[Name of the database]`
```

Default env variables 

```
SERVER_ADDRESS=localhost \
SERVER_PORT=8000 \
DB_USER=root \
DB_PASSWD=codecamp \
DB_ADDR=localhost \
DB_PORT=3306 \
DB_NAME=banking \
```

There is a sanity check in case no env variable is provided.

##### Endpoints
```
/customers - GET
/customers/{id} - GET
/customers/{customer_id}/account - POST
/customers/{customer_id}/account/{account_id} - POST

```

### To start the application first do the mysql database configuration and be sure to start it.

You can use any one of the following procedure to make a database instance, and make the changes to your `start.sh` file accordingly 
1. `docker-compose.yml` file. This contains the init script to generate and tables and insert the default data. You just need to bring the container up

    To start the docker container, run the `docker-compose up` inside the `resources/docker` folder
 
2. `resources/database.sql` this contains the SQL for generating the tables. In case you don't want to use the docker-compose file you can use this file to generate tables and insert the default data

### Generate mocks
`./generate-mocks.sh`

### Run unit tests
  `./run-tests.sh`

When all the above is done. Start both shell scripts from banking and [banking-auth](https://github.com/georgegeorgiev0/banking-auth) repositories.

Endpoints are protected. To use banking microservice it is needed to login in to banking-auth microservice.

Default port for banking-auth microservice is 8181

### Request to login
Method - Post

```
localhost:8181/auth/login
```

Body - JSON

```
{
    "username": "admin",
    "password": "abc123"
}
```

Response 

```
{
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjdXN0b21lcl9pZCI6IiIsImFjY291bnRzIjpudWxsLCJ1c2VybmFtZSI6ImFkbWluIiwicm9sZSI6ImFkbWluIiwiZXhwIjoxNjcxNTMyMjMyfQ.It8zFPJljG3IVTjufW4fEycVWLEmAf9HtQjTez2mfm8",
    "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaF90b2tlbiIsImNpZCI6IiIsImFjY291bnRzIjpudWxsLCJ1biI6ImFkbWluIiwicm9sZSI6ImFkbWluIiwiZXhwIjoxNjc0MTIwNjMyfQ.sDQFaDBSGRXsxaJBZF79QC9qbVmVjgHjVF5NfS-sEEQ"
}
```

### How to use access_token in endpoints in Postman

Navigate to Authorization section. Select Bearer Token. Fill the response from the auth login step.


