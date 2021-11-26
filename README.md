# jobrunr-sample
Sample project to learn how to use jobrunr https://github.com/jobrunr/jobrunr

## Prerequisites

Java 17

## how to run

1. Run mysql database via docker
2. Run one instance of the app with dashboard enabled
3. Run more instances without the dashboard.

### Run mysql server

The easiest way to run mysql is to use docker.

1. Install docker
2. Run `docker run -d --name=mysql-server -p 3306:3306 -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=<<CHANGE ME>> mysql`, replace password with yours.
3. Log in to mysql server with `ocker exec -it mysql-server mysql -u root -p`
4. create database `CREATE DATABASE jobrunr;`
5. exit mysql server with `exit`

### Run dashboard app

Dashboard server always uses the same port. Hence, multiple instances of the dashboard app cannot run on the same host.
Dashboard is enabled with the `dashboard` profile.

1. Build the project with `./gradlew build`
2. Run the app `MYSQL_USER=root MYSQL_PASSWORD=<<your pwd>> java -jar -Dspring.profiles.active=dashboard build/libs/jobrunr-sample-1.0.jar`

### Run another app without the dashboard

1. Build the project with `./gradlew build`
2. Run the app `MYSQL_USER=root MYSQL_PASSWORD=<<your pwd>> java -jar build/libs/jobrunr-sample-1.0.jar`

### UI

1. Open [`http://localhost:8000`](http://localhost:8000) in your browser
2. There is one recurring job that runs every 5 minutes and creates ~20 child jobs.