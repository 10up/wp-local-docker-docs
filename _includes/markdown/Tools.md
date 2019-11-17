## phpMyAdmin

[phpMyAdmin](https://www.phpmyadmin.net/) is available as part of the global services stack that is deployed to support all of the environments.

Access phpMyAdmin by navigating to [http://localhost:8092](http://localhost:8092).
* Username: `wordpress`
* Password: `password`

## MailCatcher

[MailCatcher](https://mailcatcher.me/) is available as part of the global services stack that is deployed to support all of the environments. It is preconfigured to catch mail sent from any of the environments created by WP Local Docker. 

Access MailCatcher by navigating to [http://localhost:1080](http://localhost:1080).

## PHPMemcachedAdmin

[PHPMemcachedAdmin](https://github.com/elijaa/phpmemcachedadmin) is available within each environment. It enables you
to view basic memcache stats as well as execute based memcache commands.

Access PHPMemcachedAdmin by appending `/__memcacheadmin/` to your environment's hostname. For example, if your hostname
is `docker.test`, you can access PHPMemcachedAdmin at `docker.test/__memcacheadmin/`

## Xdebug

Xdebug is included in the php images and is nearly ready to go out of the box. Make sure your IDE is listening for
PHP debug connections and set up a path mapping to your local environment's `wordpress/` directory to `/var/www/html/`
in the container.

### Visual Studio Code
1. Install the [PHP Debug](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug) extension.
2. In your project, go to the Debug view, click "Add Configuration..." and choose PHP environment. A new launch configuration will be created for you.
3. Set the `pathMappings` parameter to your local `wordpress` directory. Example:
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
