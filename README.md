# GuzabaPlatform Documentation

## Introduction

[GuzabaPlatform](https://github.com/AzonMedia/guzaba-platform) is a plugin based system for building applications ranging from presentational websites to corporate applications.
It is based on the [Guzaba 2 Framework](https://github.com/AzonMedia/guzaba2).

## Deployment in containers

There is a [docker-compose file](https://github.com/AzonMedia/guzaba-platform/blob/master/app/dockerfiles/GuzabaPlatformDev/docker-compose.yml) with preset environment variables available at [./app/dockerfiles/GuzabaPlatformDev/](https://github.com/AzonMedia/guzaba-platform/tree/master/app/dockerfiles/GuzabaPlatformDev). 

Before the application is started it needs to be deployed on the host system in an empty directory with:

```
$ echo "{}">composer.json
$ composer config minimum-stability dev
$ composer require guzaba-platform/guzaba-platform
```
This will install GuzabaPlatform and run the GuzabaPlatformInstaller package that will create the needed directories & files in the root of the project.
While the GuzabaPlatform depends on PHP 7.4 and Swoole these requirements are not enforced in the composer.json file as it needs to be possible to bootstrap the application from any environment and the applicattion will be always started in a container which already contains everything needed. 

To deploy the application in containers execute:
```
$ ./app/bin/start_containers
```
This will start the following containers:
- swoole (in interactive mode) on port 8081
- redis on port 6379 (exported for debug purpose)
- mysql on port 3306 (exported for debug purpose)
- phpmyadmin on port 8085
- phpredisadmin on port 8086

The login for phpmyadmin is "root" : "somerootpass".

The login for phpredisadmin is "admin" : "admin".

**NOTE - on first run:** On the first start of the application the database needs to be imported in MySQL. This can be done through phpmyadmin or directly over the exposed port 3306.
The database dump is available at [./app/database/guzaba2.sql](https://github.com/AzonMedia/guzaba-platform/blob/master/app/database/guzaba2.sql).

After the containers are started there will be no application running yet on port 8081. This needs to be started manually. To get into the container:
```
$ docker exec -it guzabaplatformdev_swoole_1 /bin/bash
```
If the above command produces an error this is most probably related to the container name. It may differ. To find the correct name list all the running containers with:
```
$ docker ps
```  

**NOTE - on first run:** The front end needs to be compiled - inside the container execute:
```
$ cd /home/local/app/public_src
$ ./build_prod
```

There is no need to set up local configuration in the ./app/registry because the [environment file](https://github.com/AzonMedia/guzaba-platform/blob/master/app/dockerfiles/GuzabaPlatformDev/guzaba-platform.env) contains all the needed variables.

To start the application inside the container do:
```
$ /home/local/app/bin/start_server
```

## Direct application startup

There is also a [docker-compose file](https://github.com/AzonMedia/guzaba-platform/blob/master/app/dockerfiles/GuzabaPlatform/docker-compose.yml) allowing the application to be started along with the other containers (instead of starting the swoole container in interactive mode):
```
$ /home/local/app/bin/start_server_in_container
```

## Manual install

```
# require GuzabaPlatform
$ composer require guzaba-platform/guzaba-platform

# Create local configuration
$ cp app/registry/local.php.dist app/registry/local.php

# Build the front end
$ app/public_src/build_prod
```

Change the settings in your ```app/registry/local.php``` so you can connect to the MySQL and to the Redis server. 

## Packages

The GuzabaPlatform is comprised of multiple [Composer](https://getcomposer.org/) packages.
Some of these packages are components for GuzabaPlatform and others are just dependencies and there are few main/special packages all of which you can find below.

#### Main packages

The following packages are neither GuzabaPlatform components, neither base modules used by these.
These can be installed with `composer require`.
Usually the only one needed to be installed is GuzabaPlatform with `composer require guzaba-platform/guzaba-platform`. This will install all of these.

- [guzaba-platform/guzaba-platform](https://packagist.org/packages/guzaba-platform/guzaba-platform) - the [GuzabaPlatform](https://github.com/AzonMedia/guzaba-platform) itself
- [guzaba-platform/guzaba-platform-installer](https://packagist.org/packages/guzaba-platform/guzaba-platform-installer) - the [installer of GuzbaPlatform](https://github.com/AzonMedia/guzaba-platform-installer). It is always installed with GuzabaPlatform. It has its package type set to "composer-plugin"
- [guzaba-platform/guzaba-platform-docs](https://packagist.org/packages/guzaba-platform/guzaba-platform-docs) - [GuzabaPlatform documentation](https://github.com/AzonMedia/guzaba-platform-docs)
- [guzaba/guzaba2](https://packagist.org/packages/guzaba/guzaba2) - the [Guzaba 2 Framework](https://github.com/AzonMedia/guzaba2) that powers GuzabaPlatform

#### List of available components

The following GuzabaPlatform components are available as packages through [Packagist](https://packagist.org/).
The GuzabaPlatform components have their package type set to "guzaba-platform-component" in composer.json and have their GitHub repository name starting with "component".
You can use the given names with the `composer require` command.
- [guzaba-platform/request-caching](https://packagist.org/packages/guzaba-platform/request-caching) - [Request caching component](https://github.com/AzonMedia/component-request-caching) (injects a new middleware)

#### List of the components in development 
You can use the given names with the `composer require` command. 
- [guzaba-platform/assets](https://packagist.org/packages/guzaba-platform/assets) - [Digital assets management component](https://github.com/AzonMedia/component-assets)
- [guzaba-platform/cart](https://packagist.org/packages/guzaba-platform/cart) - [Shopping cart component](https://github.com/AzonMedia/component-cart)
- [guzaba-platform/catalog](https://packagist.org/packages/guzaba-platform/catalog) - [Catalog component](https://github.com/AzonMedia/component-catalog) (can be used as products catalog/store front)
- [guzaba-platform/cms](https://packagist.org/packages/guzaba-platform/cms) - [CMS component](https://github.com/AzonMedia/component-cms)
- [guzaba-platform/crud](https://packagist.org/packages/guzaba-platform/crud) - [CRUD component](https://github.com/AzonMedia/component-crud)
- [guzaba-platform/payments-integrations](https://packagist.org/packages/guzaba-platform/payments-integrations) - [Payments integrations component](https://github.com/AzonMedia/component-payments-integrations)
- [guzaba-platform/payments-integration-epaybg](https://packagist.org/packages/guzaba-platform/payments-integration-epaybg) - [Payments integration with Epay.bg component](https://github.com/AzonMedia/component-payments-integration-epaybg)
- [guzaba-platform/roles](https://packagist.org/packages/guzaba-platform/roles) - [Roles management component](https://github.com/AzonMedia/component-roles)
- [guzaba-platform/tags](https://packagist.org/packages/guzaba-platform/tags) - [Tags component](https://github.com/AzonMedia/component-tags)
- [guzaba-platform/users](https://packagist.org/packages/guzaba-platform/users) - [Users management component](https://github.com/AzonMedia/component-users)

#### List of modules

Additional packages that are used by GuzabaPlatform but are not GuzabaPlatform components.
These packages have their package type set to "library" repository name starting with "module".
These still can be installed individually with `composer require` but usually these will be installed as part of the components listed above.
- [guzaba-platform/cart-base](https://packagist.org/packages/guzaba-platform/cart-base) - [Shopping cart module](https://github.com/AzonMedia/module-cart-base) - contains interfaces
- [guzaba-platform/catalog-base](https://packagist.org/packages/guzaba-platform/catalog-base) - [Catalog module](https://github.com/AzonMedia/module-catalog-base) - contains interfaces
- [guzaba-platform/components-base](https://packagist.org/packages/guzaba-platform/components-base) - [Components module](https://github.com/AzonMedia/module-components-base) - interfaces needed to be implemented by every GuzabaPlatform module
- [guzaba-platform/payments-integrations-base](https://packagist.org/packages/guzaba-platform/payments-integrations-base) - [Payments Integrations module](https://github.com/AzonMedia/module-payments-integrations-base) - contains interfaces
- [guzaba-platform/tags-base](https://packagist.org/packages/guzaba-platform/tags-base) - [Tags module](https://github.com/AzonMedia/module-tags-base) - contains interfaces


## Basic Topics

- [Routing](./Routing)
- [Command Line Arguments](./cli-args)
- [Development](./Development)
- [Components](./Components)