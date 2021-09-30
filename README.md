# TLBB-docker

## Requirement
- OS: Ubuntu 20.04
- Docker version 20.10.8, build 3967b7d
- Docker-compose version 1.29.2, build 5becea4c

## Set up enviroment
- Install docker: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04
- Install docker-compose: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04

## Set up gameserver
- Copy server files (*Server*, *Public*) to *./server*
- Setup IP for gameserver *./Server/Config*:
    - *LoginInfo.ini*
        ```
        [System]
        LoginID=2
        DBIP=127.0.0.1 ;IP Database
        DBPort=3306 ;Port Database
        DBName=tlbbdb ;table Database
        DBUser=root ;User Database
        DBPassword=tlbb1234 ;Pass Database
        ```
    - *ServerInfo.ini*
        ```
        [Billing]
        Number=1
        IP0=192.168.1.94 ;IP billing
        Port0=12680 ;Port billing
        ```
        ```
        IP0=192.168.1.94 ;IP your VPS
        Port0=3731
        ```
        ```
        IP0=192.168.1.94 ;IP your VPS
        Port0=7384
        ```
    - *ShareMemInfo.ini*
        ```
        DBIP=127.0.0.1		;IP Database
        DBPort=3306		;Port Database
        DBName=tlbbdb		;table Database
        DBUser=root		;User Database
        DBPassword=tlbb1234	;Pass Database
        ```

## Run gameserver
- Run build docker-compose *./<git_folder>/*
    ```
    docker-compose up -d --remove-orphans --build
    ```
- Use MySQL client or some app can exec MySQL connect to Datbase:
    - CREATE DATABASE **tlbbbd**
    - Execute sql *tlbbbd.sql*
    - CREATE DATABASE **web**
    - Execute sql *web2.sql*
    Note: sql files can get from **Resource** under

- Run billing**
- Exec to gamesever container and run gameserver:
    - Run shm - Sharememory
    ```
    docker container exec -it <container-name> /bin/bash
    cd Server
    ./shm start
    ```
    - Run Login
    ```
    docker container exec -it <container-name> /bin/bash
    cd Server
    ./Login
    ```
    - Run World
    ```
    docker container exec -it <container-name> /bin/bash
    cd Server
    ./World
    ```
    - Run Server
    ```
    docker container exec -it <container-name> /bin/bash
    cd Server
    ./Server
    ```

## Another setup for play
- Run billing if you use our source billing
    - Base on: https://github.com/liuguangw/billing_rust
    - Get our billingg resource (already build - 64bit system), extract it
    - Config billing
        ```
        {
            "ip": "192.168.1.94", // IP billing export
            "port": 12680, // Port billingg export
            "db_host": "192.168.1.94", // IP Database
            "db_port": 3306, // Port Database
            "db_user": "root", // User Database
            "db_password": "tlbb1234", // Pass Database
            "db_name": "web", // Table web for billing
            "auto_reg": true,
            "allow_ips": [],
            "transfer_number": 1000,
            "debug_type": 0
        }
        ```
    - *./<billing_folder>/release/*
        ```
            ./billing up
        ```

- Setup for client connect
    - *<client_folder>/Patch/loginserver.txt*
    ```
    VERSION 1
    SERVER_BEGIN
    LÕc Dß½ng,Phi Long TÕi Thiên,1,121,3,1,0,Cøm máy chü LÕc Dß½ng,<IP VPS>:<Port Server>,,,
    SERVER_END
    ```
    Eg:
    ```
    VERSION 1
    SERVER_BEGIN
    LÕc Dß½ng,Phi Long TÕi Thiên,1,121,3,1,0,Cøm máy chü LÕc Dß½ng,192.168.1.94:7384,,,
    SERVER_END
    ```

- Public port:
    ```
    sudo ufw allow 3306
    ```

## Resource
https://drive.google.com/drive/folders/1mjiKzDl3Zqh3r1lO3hnZ_6Q1sYHwkkvi?usp=sharing

## Thankyou to
- Docker build by Hades: https://github.com/DevTLBB/TLBB-Docker
- Biling linux Rust by liuguangw: https://github.com/liuguangw/billing_rust
- Server+Client+Database tlbb-kyniem by Hades: http://www.clbgamesvn.com/diendan/showthread.php?t=320244