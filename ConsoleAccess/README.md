# Console Access and debug ports

## Basics
The [command line option](../cli-args/README.md) **--enable-debug-ports** enables a port on each worker to which a telnet connection can be established.
The ports default configuration for the debug ports is to start of base port 10000 for Worker 0 and go up for every worker.
So if there are 8 workers in total (including task workers) the debug ports will be 10000 through 10007.
When the debug ports are enabled the following line will be printed on application startup:
```
[5.1820 Startup] Worker debug ports enabled: 10000 - 10007
```

The debug ports allow for execution of certain commands and any controller.
The reason to execute a controller through the debug port instead of a regular HTTP request is that by using the debug port the request can be executed on a specific worker, while a
regular HTTP request can be served by any worker. 

If the application is executed in a container (see ./app/bin/start_containers) the debug ports are not exposed by default.
To access them the telnet command needs to be executed from within the Swoole container or the ports need to be exposed to the host.

## Connecting

To connect to worker 0 (from within the container) execute:
```
$ telnet localhost 10000
```

This will produce a prompt like:
```
W0>>>
```
The number denotes the Worker ID. If the worker is a task worker the prompt will be:
```
TW0>>>
```

## Executing commands

Help is available with:
```
W0>>> help
```
And for specific topic with:
```
W0>>> help TOPIC
```
For example

## Executing controllers

The "execute" command provided by the ControllerExecutor module allows for execution of any controller.
```
W0>>> help ControllerExecutor
W0>>> help execute
W0>>> execute GET /api/request-test
```