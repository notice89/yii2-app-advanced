<p align="center">
    <a href="https://github.com/yiisoft" target="_blank">
        <img src="https://avatars0.githubusercontent.com/u/993323" height="100px">
    </a>
    <h1 align="center">Yii 2 Advanced Project Template</h1>
    <br>
</p>

Yii 2 Advanced Project Template is a skeleton [Yii 2](http://www.yiiframework.com/) application best for
developing complex Web applications with multiple tiers.

The template includes three tiers: front end, back end, and console, each of which
is a separate Yii application.

The template is designed to work in a team development environment. It supports
deploying the application in different environments.

Documentation is at [docs/guide/README.md](docs/guide/README.md).

[![Latest Stable Version](https://img.shields.io/packagist/v/yiisoft/yii2-app-advanced.svg)](https://packagist.org/packages/yiisoft/yii2-app-advanced)
[![Total Downloads](https://img.shields.io/packagist/dt/yiisoft/yii2-app-advanced.svg)](https://packagist.org/packages/yiisoft/yii2-app-advanced)
[![Build Status](https://travis-ci.org/yiisoft/yii2-app-advanced.svg?branch=master)](https://travis-ci.org/yiisoft/yii2-app-advanced)

DIRECTORY STRUCTURE
-------------------

```
common
    config/              contains shared configurations
    mail/                contains view files for e-mails
    models/              contains model classes used in both backend and frontend
    tests/               contains tests for common classes    
console
    config/              contains console configurations
    controllers/         contains console controllers (commands)
    migrations/          contains database migrations
    models/              contains console-specific model classes
    runtime/             contains files generated during runtime
backend
    assets/              contains application assets such as JavaScript and CSS
    config/              contains backend configurations
    controllers/         contains Web controller classes
    models/              contains backend-specific model classes
    runtime/             contains files generated during runtime
    tests/               contains tests for backend application    
    views/               contains view files for the Web application
    web/                 contains the entry script and Web resources
frontend
    assets/              contains application assets such as JavaScript and CSS
    config/              contains frontend configurations
    controllers/         contains Web controller classes
    models/              contains frontend-specific model classes
    runtime/             contains files generated during runtime
    tests/               contains tests for frontend application
    views/               contains view files for the Web application
    web/                 contains the entry script and Web resources
    widgets/             contains frontend widgets
vendor/                  contains dependent 3rd-party packages
environments/            contains environment-based overrides
```

ISSUES encountered
--MAP mysql port so it can be accessible remotely. https://github.com/docker-library/mysql/issues/95. It is also possible to include this command from the docker file
--AWS ec2 composer update errors PHP Fatal error: Allowed memory size of 1073741824 bytes exhausted (tried to allocate 144115188075867549 bytes) in phar:///bin/composer.phar/src/Composer/Util/RemoteFilesystem.php on line 179 solution is here https://stackoverflow.com/questions/33299302/composer-update-failed-out-of-memory but since we're using docker, i think it should be executed inside the docker instance.

MOST Commonly used comands
*  sudo df -h .; du -sh -- * | sort -hr 
	list down all files and folders with disk usage
*  docker-compose kill
	Kill all services
* docker-compose up -d 
	start all container
* docker-compose build
	build all container and apply all the changes if there's any chagnes in the docker file
* docker-compose run --rm backend yii migrate
        Execute migrations
* docker run -p 3306:3306 --name yii2advanced_mysql_1_bridge -e MYSQL_ROOT_PASSWORD=rootP@ssw0rd032611 -d mysql:5.7 
        make mysql accessible from SQLYOG
*  docker stop $(docker ps -a -q)
	stops all container 
* docker rm $(docker ps -a -q) 
	removes all stopped container 
* docker system prune -a
	Removeds all unused containers and images
* docker-compose logs --tail="all" -f 
	Display all container logs



DOCKER IMplemenation notes. 
* No such file or directory. When we see this error upon running yii2 migrate go to common/config/main-local.php and set the host from localhost to mysql. 
* Removing Containers will delete all the saved mysql DATA
* docker-compose kill to shutdown containers because using docker-compose down or stop may break mysql container 
* use docker-compose up -d when starting or restarting the the containers because using start may break mysql container. 
* If docker is not running well, try restarting the docker service or restarting the entire system. 
* backend error 502 was fixed by adding .htaccess in backend/web/. then adding this line below. Reference https://stackoverflow.com/questions/51310258/yii2-the-requested-url-site-login-was-not-found-on-this-server
[code]
Options +FollowSymLinks
IndexIgnore */*

RewriteEngine on

RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule . index.php
[/code]








