# Cli-args

## Overview

Cli-args are used to overwrite the Application Swoole Server Options, such as **document-root**, **open_http2_protocol**, **socket type** and to reset **Access-Control-Allow-Origin** 

## Command

The console commands extends [Symfony Console Component](https://symfony.com/doc/current/components/console.html).

The console application is created at the very beggining of start_server.php. The command name is **start** but is set as default command and may not be called. 

## Options

Options are not ordered (meaning you can specify them in any order) and are specified with two dashes (e.g. --yell). Options are always optional, and can be setup to accept a value (e.g. --dir=src) or as a boolean flag without a value (e.g. --yell).

*  **document-root** - Add default path to project
  
  Example: --document-root=path/to/root

*  **enable-ssl** - Enable ssl: sock_type = SWOOLE_SOCK_TCP | SWOOLE_SSL

  Example: --enable-ssl

*  **enable-http2** - Enable http2: set open_http2_protocol = TRUE

  Example: --enable-http2

*  **cors-origin** - Add Cross-Origin Resource Sharing
  
  Example: --cors-origin=192.168.0.52
  
* **log-level**  - set the log level for the PSR3- Logger. The possible values are: debug, info, notice, warning, error, critical, alert, emergency. The deault level is **debug**.
  
  Example: --log-level=warning
  
To add more options edit [Start.php](https://github.com/AzonMedia/guzaba-platform/blob/master/app/bin/Start.php)

All options are added in the output property **options** and then passed to [RegistryBackendCli](https://github.com/AzonMedia/registry/blob/master/src/RegistryBackendCli.php) which is the first backend for **GuzabaPlatform** and will overwrite its `CONFIG_DEFAULTS` constant.

**The same structure as [GuzabaPlatform](https://github.com/AzonMedia/guzaba-platform/blob/master/app/src/GuzabaPlatform/Platform/Application/GuzabaPlatform.php) CONFIG_DEFAULTS must be used.**

## Usage

`php app/bin/start_server.php --document-root=public --enable-ssl --enable-http2 --cors-origin=192.168.0.5`
