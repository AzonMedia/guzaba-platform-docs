# Routing

## Overview

There are two set of routes:
- public ones used by Vue
- API ones - some of these are used by the Vue templates to hydrate the controllers and others are API endpoints for pulling/updating data

To avoid collision between the two the public routes look like "/login" while the Api routes always are prefixed with "/api". This is to say that the controller that hydrates the Vue template "/login" is "/api/login". This separation is needed as Vue paths can be invoked directly (copy/paste of URL) and this means that the client wants to invoke the Vue template, not to do an API request.

The server side needs to know only about the "/api" routes while the client side (Vue) needs to use both - the normal routes for switching templates and the "/api" routes to interact with the server.

Another special route that is served by the server side and is not an "/api" route is "/" - this serves the initial Vue template by serving the ./public/index.html file.

All the static resources are served by Swoole static handler and are not going through the Swoole workers.

## Controllers

The controllers should declare their routing like:
```php
<?php

namespace GuzabaPlatform\Platform\Authentication\Controllers;

use GuzabaPlatform\Platform\Application\GuzabaPlatform as GP;

class Login extends Controller
{

    public const ROUTES = [
        GP::API_ROUTE_PREFIX.'/login'   => [
        //'/login'   => [
            Method::HTTP_GET_HEAD_OPT       => [self::class, 'main'],
            Method::HTTP_POST               => [self::class, 'login'],
        ],
    ];
}
```

At application start the [Guzaba2\Routing\ControllerDefaultRoutingMap](https://github.com/AzonMedia/guzaba2/blob/master/src/Guzaba2/Routing/ControllerDefaultRoutingMap.php) class will autogenerate a routing map from all controllers (based on the $ns_prefixes argument provided to the contructor of the class).

Every controller MUST define the above constant even if empty (which means the controller will not be included in the routing map). If the constant is not defined an exception will be thrown.

## Models

The models (children of ActiveRecord) MAY define an optional route like:
```php
<?php

namespace GuzabaPlatform\Platform\Authentication\Models;

class User extends ActiveRecord
{
    protected const CONFIG_DEFAULTS = [
        'route'                 => '/user',
    ];
}
```

At application start the [Guzaba2\Routing\ActiveRecordDefaultRoutingMap](https://github.com/AzonMedia/guzaba2/blob/master/src/Guzaba2/Routing/ActiveRecordDefaultRoutingMap.php) class will autogenerate a routing map from all models (based on the $ns_prefixes and the $api_route_prefix arguments provided to the contructor of the class ).

If a model defines a default route the following entry will be automatically added to the routing table:
```php
$route = [
    $api_route_prefix.$default_route                            => [
        Method::HTTP_POST                           => [ActiveRecordDefaultController::class, 'create'],
    ],
    $api_route_prefix.$default_route.'/{uuid}'                       => [
        Method::HTTP_GET_HEAD_OPT                   => [ActiveRecordDefaultController::class, 'view'],
        Method::HTTP_PUT | Method::HTTP_PATCH       => [ActiveRecordDefaultController::class, 'update'],
        Method::HTTP_DELETE                         => [ActiveRecordDefaultController::class, 'delete'],
    ],
];
```

The [Guzaba2\Orm\ActiveRecordDefaultController](https://github.com/AzonMedia/guzaba2/blob/master/src/Guzaba2/Orm/ActiveRecordDefaultController.php) class is a controller that provides CRUD operation over the ActiveRecord models.

## Additional routes

Additional (hardcoded or from another source) routes along to the above can be defined and all routes are to be merged with Azonmedia\Routing\Router::merge_routes() and the resulting array provided to [Azonmedia\Routing\RoutingMapArray](https://github.com/AzonMedia/routing/blob/master/src/RoutingMapArray.php) class which in turn is to be provided to [Azonmedia\Routing\Router](https://github.com/AzonMedia/routing/blob/master/src/Router.php).

## Routing map

The resulting routing map will be automatically generated in ./app/startup_generated/routing_map.php in human readable form.