# WebChat - Node.JS graphql webservice

This project is a CRUD to the WebChat React Client interface built in Node.JS.

The main objective of the project is to study programming languages and
techniques, it has not been improved for deployment on a production server,
only development environment.

You can use the [WebChat - React Client Interface](https://github.com/rstriquer/webchat-react-client)
to use as front-end interface of this project or just use GraphQL to browse the
resources it provides.

For more options of front end projects look in my profile for a project with the
name webchat that has "client" in its name, descriptive or even in their README
files.

Application developed following tutorial from https://www.youtube.com/watch?v=LvfJ2wEpMrs&list=PLMhAeHCz8S3_VYiYxpcXtMz96vePOuOX3
The full course is spreaded between some few github projects, this interface is 
based on the last one, provided here https://github.com/hidjou/node-graphql-react-chat-app/tree/class-15
The original project have all (back-end and front-end) in the same project, one
of the ideas of this project, in addition to studying the languages separately,
is to make it possible for the front-end to be used to study other back-end
languages and vice versa in a simpler way.

# Pre requirements:

* git 2.17.1
* npm 6.14.6
* docker 19.03.12

# Installation

Afther cloning the project you can follow the itens bellow to get it running

## Run and configure the database

The system cames with a MySQL docker compose file, you just go to the project
folder and run ```docker-compose up -d```, it will start a container with a
MySQL server in it. After that you MUST manualy create a database with a client
such as DBeaver.

**IMPORTANT**: After create the database you got to configure it at a ".env"
file. You can use the ".env.example" as a template, if you will.

The docker-compose.yml and the ".env.example" files are configured to run as is,
if you just copy the ".env.example" file to a ".env" file.

PS: Yes, I know, it has passwords on it! But this project was made to facilitate
the learning of a programming language, not this security standard.

To turn off the docker container you run ```docker-compose down``` at
project root directory level.

## migrations

To create the database tables you run the migrations, if you wish only to try
the system you can run the seeders. But first you run migration anyway
```bash
npx sequelize-cli db:migrate:all
```

Then you run the seeders, but it's not mandatory
```bash
npx sequelize-cli db:seed:all
```

After playing around you can undo the seeders, but bere in mind you'd got to
add manually the first chat user after that. Bellow command to undo seeders
```bash
npx sequelize-cli db:seed:undo:all
```

If you wish a fresh start you can even find the create table as well
```bash
npx sequelize-cli db:migrate:undo:all
```


## possible bug 01

If you are seen this line:
```bash
[nodemon] Internal watch failed: ENOSPC: System limit for number of file watchers reached, watch '/home/yourhome/yourprojectsdirectory/webchat-nodejs-server'
```

It is possible you need to raise the inotify value of your system. To do so you
just run the sequence below
```bash
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

## Possible bug 02

If you are trying to use PostgreSQL it seams to have an issue with the case
sensitive PostgreSQL demand which I could not track to the source yet. therefore
I recomend you stick to MySQL. Don't exitate in tell me about it if you found
something, though.


## Build and run the environment

Now (after creating the database and run the migrations) you must install the
packages dependencies
```bash
npm i
```

And start the server
```bash
npm run dev
```
