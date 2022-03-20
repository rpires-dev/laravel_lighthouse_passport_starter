<p align="center">
    <a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="350"></a>
     <a href="https://lighthouse-php.com/" target="_blank"><img src="https://lighthouse-php.com/logo.svg" width="100"></a>&nbsp&nbsp&nbsp
<a href="https://lighthouse-php-auth.com/" target="_blank"><img src="https://lighthouse-php-auth.com/assets/img/safe.svg" width="100"></a>
   

</p>




## About The project

I created this project to kickstart your laravel 8 projects with passport for authentication & lighthouse to serve the graphql 

### Before starting
Make sure to have some sort of database server running, here i will exemplify using a mysql server


### On the console run:

```
cp .env.example .env
php artisan key:generate
composer install
php artisan serve

```

### Set your database credencials in the .env file:

```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=mydatabase_name
DB_USERNAME=mydatabase_user
DB_PASSWORD=mydatabase_password

```

### Run the migrations by:
```  
php artisan migrate

```
### Get the passport client secret by runnning on the console:

``` 
php artisan passport:install
```
It will output something like this:

``` 
Encryption keys generated successfully.
Personal access client created successfully.
Client ID: 1
Client secret: JLWoderz1fMpmnGb0hpvniEQe3Q9o5eFPm0hrOa2
Password grant client created successfully.
Client ID: 2
Client secret: zVVIBaxUhN7Pz7BuAp90WoBUYZaRNtqqWyEoES5c
```
Copy the client secret pertaining to the ID:2 
``` 
Client secret: zVVIBaxUhN7Pz7BuAp90WoBUYZaRNtqqWyEoES5c

```
Paste it on the .env file:

``` 
PASSPORT_CLIENT_ID=2
PASSPORT_CLIENT_SECRET=zVVIBaxUhN7Pz7BuAp90WoBUYZaRNtqqWyEoES5c
```

### Run the GraphQL:

First off let's create a user by:

```
php artisan user
```
Start your GraphQL client by going to your localhost and add the playgroud to the url example: 'http://yourlocalhost/graphql-playground'

On the GraphQL client console type the following query:
```
{
  users(first: 1){
    data {
      id
      email
    }
  }
}

```
Et voilà you should have the query response for the user. 

##EXTRA
### Run a login Mutation

On your project search for the schema.graphql file, and change the the query users to:
``` 
users: [User!]! @guard(with: ["api"]) @paginate(type: "paginator" model: "App\\Models\\User")

```

Return to the GraphQL playground and try to execute the same query, you should get an error like this:

``` 
{
  "errors": [
    {
      "message": "Unauthenticated.",
      "extensions": {
        "guards": [
          "api"
        ],
        "category": "authentication"
      },
      etc..
``` 









