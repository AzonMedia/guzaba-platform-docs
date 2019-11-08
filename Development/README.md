# Development

## Live reloading

During development when the server is started with  ```start_server.php``` it should be restarted manually when new changes are introduced to the code. To avoid manual restarts live reload functionality is provided by the ```continuous_server.php``` script. 
```continuous_server.php``` starts the server by running  ```start_server.php``` and monitors all folders in  ```guzaba-platform/app/src``` for MODIFY and DELETE events. When such event occurs the main process and all its children are killed and the ```start_server.php script``` is executed again. It takes some time for all processes to finish that's why the server is not restarted immediately.
```continuous_server.php``` script is based on [inotify extension](https://www.php.net/manual/en/book.inotify.php).