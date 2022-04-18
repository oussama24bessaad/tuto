# Angular 11 CRUD example with MySQL Database

In this tutorial, we will learn how to build a full stack Angular 11 within a CRUD App. The back-end server uses Spring Boot with Spring Web MVC for REST Controller and Spring Data JPA for interacting with MySQL database. Front-end side is made with Angular 11, HTTPClient & Router.

We will build a full-stack Tutorial Application in that:

- Each Tutorial has id, title, description, published status.
- We can create, retrieve, update, delete Tutorials.
- We can also find Tutorials by title.
- The images below shows screenshots of our System.

Add an object:

![spring-boot-angular-11-crud-example-add-tutorial](spring-boot-angular-11-crud-example-add-tutorial.png)

Retrieve all objects:

![spring-boot-angular-11-crud-example-retrieve-all-tutorial](spring-boot-angular-11-crud-example-retrieve-all-tutorial.png)

Click on **Edit** button to go to a Tutorial page:

![spring-boot-angular-11-crud-example-retrieve-one-tutorial](spring-boot-angular-11-crud-example-retrieve-one-tutorial.png)

On this Page, you can:

- change status to *Published* using **Publish** button
- delete the Tutorial using **Delete** button
- update the Tutorial details with **Update** button

![spring-boot-angular-11-crud-example-update-tutorial](spring-boot-angular-11-crud-example-update-tutorial.png)

Search Tutorials by title:

![spring-boot-angular-11-crud-example-search-tutorial](spring-boot-angular-11-crud-example-search-tutorial.png)

## Angular 11 & Spring Boot CRUD Architecture
This is the application architecture we will build:

![spring-boot-angular-11-crud-example-architecture](spring-boot-angular-11-crud-example-architecture.png)

- Spring Boot exports REST Apis using Spring Web MVC & interacts with MySQL Database using Spring Data JPA.
- Angular Client sends HTTP Requests and retrieve HTTP Responses using axios, shows data on the components. We also use Angular Router for navigating to pages.

## Run the Angular 10 App
You can run this App with command: 
```bash
ng serve --port 8081
```
If the process is successful, open Browser with Url: [http://localhost:8081/](http://localhost:8081/) and check it.
