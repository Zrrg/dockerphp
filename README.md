# DockerPHP

## Creates Apache/PHP server via Docker

Made by [DockerWebDev](https://dockerwebdev.com/tutorials/docker-php-development/) manual.

## SSL certificates for local development

- Install [mkcert](https://github.com/FiloSottile/mkcert#installation)

    mkcert -install

-Locate the generated rootCA.pem file by entering `mkcert -CAROOT` in your terminal. 
-For Firefox, open Firefox’s menu and choose Options, then Privacy & Security. Scroll to the bottom and click View Certificates. Select the Authorities tab, click Import…, open the rootCA.pem file, and restart the browser.

- Create locally-trusted development certificates for your development domain:

    mkcert localhost 127.0.0.1 ::1

## Files that would go into docker image

- Rename files to cert.pem and cert-key.pem.
- Move these keys in ssl folder.
- Edit apache config in apache folder if needed.

## Build the PHP Docker image 

    docker image build -t php8 .

## Launch a PHP Container

    docker run -it --rm  -p 8080:80 -p 443:443 --name php8site -v "$PWD":/var/www/html

Take note, `-v $PWD` wouldn't be working on Windows, you have to specify full path in Linux notation: 

    -v /c/projects/mysite:/var/www/html

Or use alternative way described next.

## Launch a PHP Docker Containter with Docker Compose

Put docker-compose.yml into PHP project directory. Then run:

    docker-compose up

You may use `docker-compose up -d` form for detached from terminal launch.
    
Use `docker-compose down` to shut down the server.

