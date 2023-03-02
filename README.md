# Integrated Resource Planning System IRPS
<a href="https://github.com/chiajunshen/shrdc_custom_frappe_docker/blob/master/LICENSE">
    <img alt="GitHub" src="https://img.shields.io/github/license/chiajunshen/shrdc_custom_frappe_docker.svg?color=blue">
</a>
<a href="https://github.com/chiajunshen/shrdc_custom_frappe_docker/releases">
    <img alt="Releases" src="https://img.shields.io/github/release/chiajunshen/shrdc_custom_frappe_docker?color=success" />
</a>
<a href="https://github.com/chiajunshen/shrdc_custom_frappe_docker/releases">
    <img alt="Downloads" src="https://img.shields.io/github/downloads/chiajunshen/shrdc_custom_frappe_docker/total.svg?color=success" />
</a>
<a href="https://github.com/chiajunshen/shrdc_custom_frappe_docker/issues">
      <img alt="Issues" src="https://img.shields.io/github/issues/chiajunshen/shrdc_custom_frappe_docker?color=blue" />
</a>
<a href="https://github.com/chiajunshen/shrdc_custom_frappe_docker/pulls">
    <img alt="GitHub pull requests" src="https://img.shields.io/github/issues-pr/chiajunshen/shrdc_custom_frappe_docker?color=blue" />
</a>

<br>

# ERPNext Home Page
![ERPNext Home Page](images/homepage1.png)
![](images/homepage2.png)

<br>

# Frepple Integration 
![Frepple Integration](images/Frepple.png)

<br>

# Barcode Scanning System
![Barcode Scanning System](images/Barcode%20Scanning%20System.png)

<br>

# Autocount
![Autocount](images/Autocount.png)

<br>

# SQL Account
![SQL Account](images/pic1.png)

<br>

## For Frepple User
In order to utilise the full integration between ERPNext and Frepple, you will need a running instance of Frepple software. To install Frepple software in both Windows and Linux refer to [this document](https://docs.google.com/document/d/1P4U1rZszydwy2LmVAuC4lvYPl-dFw86LSC8Fz8zRsIE/edit?usp=sharing).

<br>

## For ERPNext User

### 1. Integrated Resource Planning System IRPS
1. Prerequisites:
    - Windows: Docker Desktop
    - Ubuntu: Docker Engine, Docker Compose
    - Mac: Docker Desktop

2. The installation of this release includes the following:
    - [ERPNext Version 12](https://github.com/frappe/erpnext)
    - [Metabase Integration](https://github.com/chiajunshen/shrdc_frappe_metabase)
    - [Telegram Integration](https://github.com/chiajunshen/shrdc_erpnext_telegram)
    - [Enhanced Frepple Integration](https://github.com/msf4-0/ERPNext-Frepple-Enhanced-Integration)
    - [Barcode Scanning System](https://github.com/leexy0/barcode_shrdc)
    - [Autocount](https://github.com/msf4-0/ERPNext-Autocount-Integration)
    - [SQL Account](https://github.com/msf4-0/ERPNext-SQL-Accounting-Integration)

3. For Windows & MacOS user, start from `Section 3`.
4. For Ubuntu user, start from `Section 4`.

### 2. Pre-Setup: Windows/MacOS
1. The setup guide is tested to work on `Windows 10`, `Ubuntu 18.04` and `macOS Mojave 10.14.6`

2. For Windows and MacOS, create a folder.

3. Open a Powershell terminal, navigate to the newly created folder.

4. Go to `Section 5: Setup`.

### 4. Pre-Setup: Ubuntu
1. Open a terminal.

2. Create a user called `frappe`. (You can give a name of your preference to replace `frappe`)
    - `sudo adduser frappe`

3. You may be promted to give a password for the newly created user `frappe`. Remember this password, you will need it for the next step.

4. Log into the user `frappe`
    - `su - frappe`

5. Create a folder called `frappe_docker`. Again, folder name is of your preference. Navigate into the new directory.
    - `mkdir frappe_docker`
    - `cd frappe_docker`

6. Go to `Section 5: Setup`.

### 5. Setup

1. Clone this repo.
    - `git clone https://github.com/msf4-0/IRPS-SQL_Accounting-Autocount-frepple`

2. Navigate to the cloned folder.
    - `cd IRPS-SQL_Accounting-Autocount-frepple`

3. In `enx-example`, you can change the variables that would be used in this installation process to your preference such as the following:
    - Server port to host ERPNext,`ERPNEXT_SERVER_PORT`. Default is `8000`.
    - Database port,`MARIADB_SERVER_PORT`. Default is `3306`.
    - Site name `SITE_NAME`. Default is `custom-erpnext-nginx`.
    
    Note: 
    - You can leave these variables as it's provided if all the specified ports are not occupied.
    - Upon successful setup, you can access ERPNext via port number `ERPNEXT_SERVER_PORT`.
    - For Metabase Integration, you would need to connect to Mariadb via `MARIADB_SERVER_PORT`.

4. Copy environment variables from the `env-example` file into `.env` file using this command `cp env-example .env`.

5. Start all the docker containers by this command `docker-compose -p <project_name> up -d`.
    
    Note: 
    - Replace `<project_name>` to your preference.
    - For example, `docker-compose -p project1 up -d`

6. Monitor the site creation progress by logging into the `<project_name>-site-creator-1` container. To do this step, use this command `docker logs <project_name>-site-creator-1 -f`. 
    
    Note:
    - Replace `<project_name>` to the same project name as in step 4.
    - For example, `docker logs project1-site-creator-1 -f`.
    - If you face `no such container` error, try with `docker logs project1-site-creator_1 -f` or `docker logs project1_site-creator_1 -f`.

7. After the `<project_name>-site-creator-1` container display `Scheduler is disabled`, login to `<project_name>-erpnext-python-1` container. Use `docker exec -it --user root <project_name>-erpnext-python-1 /bin/bash` to login into this container as a root user.
    
    Note:
    - Replace `<project_name>` to the same project name selected in step 4.
    - For example, `docker exec -it --user root project1-erpnext-python-1 /bin/bash`.
    - If you face `no such container` error, try with `docker exec -it --user root project1-erpnext-python_1 /bin/bash` or `docker exec -it --user root project1_erpnext-python_1 /bin/bash`.
 
 
8. Once you login in into `<project_name>-erpnext-python-1` container, by default, you will be in the `~:/home/frappe/frappe-bench/sites` directory. Navigate out to `~:/home/frappe/frappe-bench` directory by typing `cd ..`.

9. Now, apply the new changes in Frepple app by running this command `bench --site <site_name> migrate`.
    
    Note:
    - Replace `<site_name>` to the same name as specified in the .env file. Refer to step 3 and 4.
    - For example, `bench --site custom-erpnext-nginx migrate`

10. After the process `Compiling Python files...` is finished, you will be back in the `~:/home/frappe/frappe-bench` directory. This means the `bench migrate` process is completed. Type `exit` to exit from `<project_name>-erpnext-python-1` container.

11. Now, you can open any browser such as `Google Chrome` and access ERPNext via `http://localhost:<ERPNext_Server_Port>` or `http://<Your_IP_address>:<ERPNext_Server_Port>`.
    
    Note:
    - Type the selected ERPNext port number in `<ERPNext_Server_Port>` selected in step 4. 
    - For example, `http://localhost:8000` or `http://127.0.0.1:8000`.

12. Default credentials.
    - Username: `Administrator`
    - Password: `admin`

### 6. Stopping Docker Containers
1. To stop all the docker containers related to your `<peoject-name`> project:
    - Open a Powershell terminal, navigate to `IRPS-Enhanced-Frepple-Integration` folder.
    - Run `docker-compose -p <project-name> stop`. 
    - For example, `docker-compose -p project1 stop`.

### 7. Starting Docker Containers
1. To start up all the docker containers related to your `<peoject-name`> project:
    - Open a Powershell terminal, navigate to `IRPS-Enhanced-Frepple-Integration` folder.
    - Run `docker-compose -p <project-name> start`. 
    - For example, `docker-compose -p project1 start`.

### 8. Deleting Docker Containers
1. To remove all the docker containers related to your `<peoject-name`> project:
    - Open a Powershell terminal, navigate to `IRPS-Enhanced-Frepple-Integration` folder.
    - Run `docker-compose -p <project-name> down` or run `docker-compose -p <project-name> down -v` to remove the related Docker Volume.
    - For example, `docker-compose -p project1 down -v`

## Update Custom App
1. Assumptions:
    1. You have a running instance of ERPNext in docker production container.
2. [How to update custom app](https://docs.google.com/document/d/1XCfNE1SoWK3MvIFHlthTw0GBUqfyAD66YM2hoO62CjU/edit?usp=sharing)

## Backup
1. Assumptions:
    1. You have a running instance of ERPNext in docker production container.
2. Alternatives:
    1. [Online Backup (Automatic)](https://docs.google.com/document/d/1nFbnYwB1hkFBeqMrb35IOHjo7M4PF9sRGHR08TtVJ6w/edit?usp=sharing)
    2. [Local Backup (Manual)](https://docs.google.com/document/d/1x_-71FcPrrhF7vvuBX37G0No-TlPxyTQNcQWuN0f8cE/edit?usp=sharing)
    3. [Local Backup (Automatic)](https://docs.google.com/document/d/1Is8J244t_-t4Ue4bbgPr0Y4P20-0wFKE5IkGEPYU-cE/edit?usp=sharing)

## Restore
1. Assumptions:
    1. You have your backup files on your pc (if you perform online backup, you can download the backup files onto your pc).
    2. You have a running instance of ERPNext in docker production container in which you want to restore with the backup files.
2. [Restore](https://docs.google.com/document/d/1yG2N1isESsdtDdfH3aHykIrgD6lnVOLzK0zThKLreHA/edit?usp=sharing)

<br>

## For Developer
- [Reference: Customizing your own shrdc custom frappe docker](https://docs.google.com/document/d/1XxOYM_qhZ0RGI60YM82XHOkEzrn8ywXC98i354Donjc/edit?usp=sharing)

### 1. Introduction

- Fork this repo to build your own image with ERPNext and list of custom Frappe apps.
- Change `nginx/Dockerfile` and add required apps. Refer comments in the file.
- Change `worker/Dockerfile` and add required apps.

Example file uses following apps:

- [Metabase Integration](https://github.com/chiajunshen/shrdc_frappe_metabase)
- [Telegram Integration](https://github.com/chiajunshen/shrdc_erpnext_telegram)
- [Enhanced Frepple Integration](https://github.com/msf4-0/ERPNext-Frepple-Enhanced-Integration)
- [Barcode Scanning System](https://github.com/leexy0/barcode_shrdc)
- [Autocount](https://github.com/msf4-0/ERPNext-Autocount-Integration)
- [SQL Account](https://github.com/msf4-0/ERPNext-SQL-Accounting-Integration)

### 2. Build images

Execute from root of app repo.

For nginx:

```shell
# For version-12
docker build --build-arg=FRAPPE_BRANCH=version-12 --build-arg=GITHUB_OWNER=<github-username> -t custom-erpnext-nginx:v12 nginx

# Example:
docker build --build-arg=FRAPPE_BRANCH=version-12 --build-arg=GITHUB_OWNER=msf4-0 -t custom-erpnext-nginx:version-12 nginx
```

For worker:

```shell
# For version-12
docker build --build-arg=FRAPPE_BRANCH=version-12 --build-arg=GITHUB_OWNER=<github-username> -t custom-erpnext-worker:version-12 worker

# Example:
docker build --build-arg=FRAPPE_BRANCH=version-12 --build-arg=GITHUB_OWNER=msf4-0 -t custom-erpnext-worker:version-12 worker
```

### 3. Push images to Docker Hub
1. Tag the images bulilt from Step 2 with the format: 
`docker tag <Image Name>:<Version> <Docker Hub Username>/<Image Name>:<Version>`

For nginx:
```shell
docker tag custom-erpnext-nginx:version-12 shrdc/custom-erpnext-nginx:version-12
```

For worker:
```shell
docker tag custom-erpnext-worker:version-12 shrdc/custom-erpnext-worker:version-12
```

Reference: [Steps to create a Docker Hub, and push images to it.](https://docs.docker.com/get-started/04_sharing_app/)

2. To push to Docker Hub, run `docker push` with the tagged name created before. 

```shell
docker push shrdc/custom-erpnext-nginx:version-12
docker push shrdc/custom-erpnext-worker:version-12
```

3. Possible troubleshoot:
When you face `denied: requested access to the resource is denied` when pushing images, run `docker login` and enter your credentials. Then push image again.

### 4. (Optional) Configure `env-example`
1. You may need to change the `DOCKER_USERNAME` in `env-example` to the username of the Docker Hub account in which you have pushed your images to.
2. Copy `env-example` into `.env` by running `cp env-example .env`.

### 5. Start up
1. The following commands should be executed on the `~/some/path/Integrated-Resource-Planning-System-IRPS` directory
2. `docker-compose -p <project_name> up -d`
3. `docker logs <project_name>_site-creator_1 -f`
    1. If you got a `no such container` error, you may need to change to `docker logs <project_name>-site-creator-1 -f`
4. After the `site_creator` container exited, open a browser, you can access ERPNext on `localhost:8000` or `127.0.0.1:8000`.
5. You can push the changes back to this repo (or your own repo if you forked one from this repo).

## License

This software is licensed under the [GNU GPLv3 LICENSE](/LICENSE) © [Selangor Human Resource Development Centre](http://www.shrdc.org.my/). 2021.  All Rights Reserved.
