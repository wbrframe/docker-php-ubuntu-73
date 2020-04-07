# Docker Skeleton for PHP console application on Ubuntu

**Skeleton** - designed to quickly deploy environments PHP console application on Ubuntu. Сontains a minimal tools for begin development.

### Environment
- php-fpm 7.3
- xdebug 2.7.1

### Requirements
Linux, Docker compose, Git.

### Installation
First, create a folder for your project and clone the repository:

```bash
mkdir /var/www/skeleton
cd /var/www/skeleton
git clone https://github.com/wbrframe/docker-php-ubuntu-73.git .
```

Secondly, build a docker image by executing the command:
```bash
docker-compose up -d --build
```

### Starting a debugging session from PhpStorm

Set a breakpoint at the line where PHP source code execution should pause. Right-click on `index.php` and launch `Debug index.php`.

### Starting a debugging session from Command line

Just run:

``` bash
docker-compose exec php php /app/index.php
```

By default, remote host for xDebug set as `xdebug.remote_host=172.18.0.1`.
 
If debugging it does not work, make sure that the IP address of the host bridge is correct.

``` bash
docker network inspect bridge | grep Gateway
```

If necessary change in `docker-configs/php/xdebug.ini`.

### Useful configurations

You can use the predefined scripts in `composer.json` by running the command

```bash
docker-compose exec php composer `<script>`
```

**Availables scripts:**

|  Script name | Description  |
| ------------ | ------------ |
| ci:code-style  | [php-cs-fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer "php-cs-fixer") in `dry-run` mode  |
| ci:code-style-fix  | [php-cs-fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer "php-cs-fixer") without `dry-run` mode  |
| ci:static-analysis  | [phpstan](https://github.com/phpstan/phpstan "phpstan") analysis `src` and `tests` folders with 7 level  |
| ci:composer-validate  | composer validate command  |
