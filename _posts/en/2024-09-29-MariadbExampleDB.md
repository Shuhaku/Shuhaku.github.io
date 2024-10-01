---
title: '[Docker] Example MariaDB Database'
date: 2024-09-29 12:00:00 +0000
categories: [Docker, MariaDB]
tags: [Docker, MariaDB]
author: Shuhaku
mermaid: true
---

> This post may contain errors.  
> Please use it for reference only. 🥹
{: .prompt-warning }

## Development Environment

* M1 Macbook
* Docker version 24.0.2

## Example MariaDB Database

To practice SQL queries, you'll need a real database with dat in it.
This time, we will explore how to install an example database provided by MySQL into a MariaDB instance running in Docker.

You can find various example databases on the MySQL website here:

[dev.mysql.com](https://dev.mysql.com/doc/index-other.html)

Once you access the link:

You'll be able to download various example databases in tar or zip format.

For this example, I downloaded the world-db and transffered it to my Docker container.

```
docker cp world-db.zip (your-mariadb-container-name):/(your-db-location)/world-db.zip
```

---

Next, unzip the file
```
unzip world-db.zip
```

---

Now, connect to MariaDB and create the world database;
```
CREATE DATABASE world;
```

---

Go back to your container and install the unzipped world.sql file
```
mariadb -u root -p world < /(your-db-location)/world.sql
```

---

You should now be able to see the generated tables and data by using SQL queries,
You can now view and interact with the tables and data in the world database.
