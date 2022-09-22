#R&D Laradock

## Introduce
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.
___

## Quick Overview
docker-v: Docker version 18.03.1-ce, build 9ee9f40
docker-compose -v: docker-compose version 1.19.0, build 9e633ef

1. Clone Laradock inside your PHP project:

    ```
        git clone https://github.com/nhuongph/docker.git
    ```

2. Enter the laradock folder and rename env-example to .env.

    ```
        cp env-example .env
    ```

3. Run your containers:

    ```
        docker-compose up -d nginx postgres redis
    ```

4. Open your project’s .env file and set the following:


        #Database
        DB_CONNECTION=pgsql
        DB_HOST=postgres
        DB_PORT=5432
        DB_USERNAME=nhuongph
        DB_PASSWORD=secret
        #Redis
        REDIS_HOST=redis


5. That's it! enjoy :)

#Getting Started

##Requirements

    > Git
    
    > Docker >= 1.12

##Installation

### Docker

- https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce

- https://docs.docker.com/compose/install/

### Setup docker

1. Configuration

    \- Edit your web server sites configuration.

    ```
        cp env-example .env
    ```

    \- At the top, change the APPLICATION variable to your project path.

    ```
        APPLICATION=/var/www/
    ```

2. Setup for Multiple Projects:

    \- Go to nginx/sites and create config files to point to different project directory when visiting different domains.
    
    \- Change the default names ```*.conf```. You can rename the default config file, edit the content file or add new the config files.

    > If you use Chrome 63 or above for development, don’t use .dev

3. Add the domains to the hosts files.

    
        127.0.0.1. project-1.test
        127.0.0.1. project-2.test
    

### Usage

- Build the enviroment and run it using docker-compose

    ```
        docker-compose up -d nginx postgres redis
    ```

- Enter the Workspace container, to execute commands like (Artisan, Composer, Gulp, …)

    ```
        docker-compose exec workspace bash
    ```

    Alternatively

    ```
        docker exec -it {workspace-container-id} bash
    ```

- Update your project configurations to use the database host

    Open your PHP project’s .env file or whichever configuration file you are reading from.

    
        DB_CONNECTION=pgsql
        DB_HOST=postgres
        DB_PORT=5432
        DB_USERNAME=nhuongph
        DB_PASSWORD=secret
        
        REDIS_HOST=redis


- Open your browser and visit your address. Ex: ``http://localhost/``

### Enter a Container (run commands in a running Container)

- First list the current running containers with ``docker ps``

- Enter any container using:

    ```
        docker-compose exec {container-name} bash
    ```
    
    Example: enter MySQL container

    ```
        docker-compose exec postgres bash
    ```
    
    Or

    ```
        docker-compose exec postgres postgres --version
    ```

- To exit a container, type exit.

### Build/Re-build Containers

- If you do any change to any Dockerfile make sure you run this command, for the changes to take effect:

    ```
        docker-compose build
    ```

- Optionally you can specify which container to rebuild (instead of rebuilding all the containers):

    ```
        docker-compose build {container-name}
    ```

- You might use the --no-cache option if you want full rebuilding 

    ```
        docker-compose build --no-cache {container-name}
    ```

### View the Log files

- The NGINX Log file is stored in the logs/nginx directory.

    However to view the logs of all the other containers (MySQL, PHP-FPM,…) you can run this:

    ```
        docker-compose logs {container-name}
    ```

### Use Adminer

- Run the Adminer Container (adminer) with the docker-compose up command. Example:

    ```
        docker-compose up -d adminer
    ```

- Open your browser and visit the localhost on port 8080. http://localhost:8080

### Use Minio

1. Configure Minio: - On the workspace container, change INSTALL_MC to true to get the client. 
    
    Set MINIO_ACCESS_KEY and MINIO_ACCESS_SECRET if you wish to set proper keys

2. Run the Minio Container (minio) with the docker-compose up command. Example:

    ```
        docker-compose up -d minio
    ```

3. Open your browser and visit the localhost on port 9000 at the following URL: http://localhost:9000

4. Create a bucket either through the webui or using the mc client:

    ```
        mc mb minio/bucket
    ```

5. When configuring your other clients use the following details:

        S3_HOST=http://minio
        S3_KEY=access
        S3_SECRET=secretkey
        S3_REGION=us-east-1
        S3_BUCKET=bucket

### Caddy (Run Site on SSL with Let’s Encrypt Certificate)

> Note: You need to Use Caddy here Instead of Nginx

1. To go Caddy Folders and Edit CaddyFile


        $root@server:~/laravel/laradock# cd caddy
        $root@server:~/laravel/laradock/caddy# vim Caddyfile


2. Remove https://twilio.dev


        https://twilio.dev
        root /var/www/calling/calling-twilio/public


3. And replace with your https://yourdomain.com


        https://yourdomain.com
        root /var/www/public


4. Run Your Caddy Container

    ```
        docker-compose up -d caddy
    ```
    
5. View your Site in the Browser Securely Using HTTPS (https://yourdomain.com)

### Use PgAdmin

1. Run the pgAdmin Container (pgadmin) with the `docker-compose up`` command. Example:

        docker-compose up -d postgres pgadmin

2 - Open your browser and visit the localhost on port 5050: http://localhost:5050

    UserName: pgadmin4@pgadmin.org
    Password: admin


## Happy Coding :)

:relaxed: :relaxed: :relaxed: :relaxed: :relaxed: :relaxed::relaxed: :relaxed: :relaxed: :relaxed: :relaxed: :relaxed:  
:beers: :beers: :beers: :beers: :beers: :beers: :beers: :beers: :beers: :beers: :beers: :beers:  
:dancer: :dancer: :dancer: :dancer: :dancer: :dancer: :dancer: :dancer: :dancer: :dancer: :dancer: :dancer:  
