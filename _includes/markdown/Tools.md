## phpMyAdmin

[phpMyAdmin](https://www.phpmyadmin.net/) is available as part of the global services stack that is deployed to support all of the environments.

Access phpMyAdmin by navigating to [http://localhost:8092](http://localhost:8092).
* Username: `wordpress`
* Password: `password`

## MailCatcher

[MailCatcher](https://mailcatcher.me/) is available as part of the global services stack that is deployed to support all of the environments. It is preconfigured to catch mail sent from any of the environments created by WP Local Docker.

Access MailCatcher by navigating to [http://localhost:1080](http://localhost:1080).

## Xdebug

Xdebug is included in the php images but must be manually enabled if you use wp-local-docker 2.7.0 or earlier. To enable Xdebug, set the environment variable `ENABLE_XDEBUG` to `'true'` in the `docker-compose.yml` file in the root of the project. If you use wp-local-docker 2.8.0 or higher, then new environments will have Xdebug enabled by default.

Make sure your IDE is listening for PHP debug connections and set up a path mapping to your local environment's `wordpress/` directory to `/var/www/html/` in the container.

### Visual Studio Code

1. Ensure Xdebug is enabled for the environment using the `ENABLE_XDEBUG` environment variable.
2. Install the [PHP Debug](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug) extension.
3. In your project, go to the Debug view, click "Add Configuration..." and choose PHP environment. A new launch configuration will be created for you.
4. Set the `pathMappings` parameter to your local `wordpress` directory. Example:
```json
"configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9000,
            "pathMappings": {
                "/var/www/html": "${workspaceFolder}/wordpress",
            }
        }
]
```

### Xdebug 3 configuration

Replace the Xdebug configuration file at `config/php-fpm/docker-php-ext-xdebug.ini` with the following:
```
xdebug.mode=debug
xdebug.start_with_request=yes
xdebug.client_host=host.docker.internal
```

Xdebug 3 changes the default port from `9000` to `9003`. If you want to use a custom port, make sure to include it in the configuration file:

```
...
xdebug.client_host=host.docker.internal
xdebug.client_port=<custom_port>
```
