---
title: '[Docker] Using MariaDB in Docker'
date: 2024-09-14 12:00:00 +0000
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

## Usage

![1_docker_pull](/assets/img/dev/2024-09-14/1_docker_pull.png)

```
docker pull mariadb
```

_Pull the MariaDB image from Docker Hub._

---

<br>

![2_docker_run](/assets/img/dev/2024-09-14/2_docker_run.png)

```
docker run --name my-mariadb -e MARIADB_ROOT_PASSWORD=myPassword -p 3306:3306 -d mariadb
```

_`docker run`: Run a Docker container._

_`--name my-mariadb`: Name the container "my-mariadb"._

_`-e MARIADB_ROOT_PASSWORD=myPassword`: Set the root user password for MariaDB via environment variable._

_`-p 3306:3306`: Map port 3306 of the host to port 3306 inside the container, allowing external access to MariaDB in Docker._

_`-d mariadb`: Run the container in detached mode._

---

<br>

![3_docker_ps](/assets/img/dev/2024-09-14/3_docker_ps.png)

```
docker ps
```

_Display currently running Docker containers._

---

<br>

![4_docker_exec](/assets/img/dev/2024-09-14/4_docker_exec.png)

```
docker exec -it (mariadb_container_name) bash
```

_Access the Bash shell inside the MariaDB container._

---

<br>

![5_mariadb](/assets/img/dev/2024-09-14/5_mariadb.png)

```
mariadb -u root -p
```

_Attempt to access the database using the password set during `docker run`._

_Display a list of all databases._

_At this point, only the default MariaDB system databases will be present._

---

```
create database (DB_name);
```

_Create a new database._

---

```
use (DB_name);
```

_Switch to the selected database._

---

<br>

![6_create_table](/assets/img/dev/2024-09-14/6_create_table.png)

```
CREATE TABLE Account ( account_id INT AUTO_INCREMENT PRIMARY KEY, username VARCHAR(50) NOT NULL, email VARCHAR(100) UNIQUE NOT NULL, password VARCHAR(255) NOT NULL, created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP );
```

_Create a sample Account table._

---

<br>

![7_insert_db](/assets/img/dev/2024-09-14/7_insert_db.png)

```
INSERT INTO Account (username, email, password) VALUES ('john_doe', 'john@example.com', 'password123'), ('jane_smith', 'jane@example.com', 'securepwd456'), ('bob_johnson', 'bob@example.com', 'strongpass789');
```


_Insert some sample data into the Account table._

---

<br>

![8_select_db](/assets/img/dev/2024-09-14/8_select_db.png)

```
SELECT * FROM Account;
```

_View the inserted data._

---
