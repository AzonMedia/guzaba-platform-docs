# Error 3b0d54d3-1662-4e84-9f7a-971a30baef83

It is not allowed to run in production mode with authorization provider that does not check/enforce permissions. To bypass this limitation please start the server with the --allow-no-permission-checks-in-production startup option.

The following authorization providers do not check/enforce permissions:
- BypassAuthorizationProvider
- AclCreateAuthorizationProvider
- AclAutomaticCreateAuthorizationProvider

This error may occur when any of these is chosen and the deployment is set to production.
The currently used authorization provider is displayed in the startup messages.

To change the authorization provider please see the registry, Guzaba2\Di\Container config section, the AuthorizationProvider service.
Also the --no-permission-checks CLI option if passed will set the AuthorizationProvider to AclCreateAuthorizationProvider.

This means that the following startup options will result in this error:
```
$ ./start_server --no-permission-checks --deployment=production
```
To bypass it:
```
$ ./start_server --no-permission-checks --deployment=production --allow-no-permission-checks-in-production
```