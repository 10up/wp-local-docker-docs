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

### PHPStorm

Helpful documentation links:
- https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html
- https://www.jetbrains.com/help/phpstorm/servers.html

*NOTE: the above documents have a lot of information that isn't relevant to our specific setup; use them mostly as reference*

1. Ensure Xdebug is enabled for the environment using the `ENABLE_XDEBUG` environment variable.
2. Ensure the following configuration is set in `site-name-test/config/php-fpm/docker-php-ext-xdebug.ini`:
```
xdebug.remote_enable = 1
xdebug.remote_autostart = 1
xdebug.remote_host = host.docker.internal
```
3. Download and install the Chrome XDebug Helper extension (or XDebug extension for whichever browser you use): https://chrome.google.com/webstore/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc
- *NOTE: If you have set `xdebug.remote_autostart = 1` in `docker-php-ext-xdebug.ini`, you will not need this extension
4. When visiting the site in your browser, use the extension to set your mode to "Debug", as this will set a specific Cookie value, enabling a connection from XDebug
5. In PHPStorm, open Settings -> Languages & Frameworks -> PHP -> Servers and click the "+" (Add New Server) button to add a new server with the following settings:
- `Name` should match the setting within your `docker-compose.yml` file from the following line: `PHP_IDE_CONFIG: serverName=site-name-test`. Note the `serverName=site-name-test` value. `Name` should match the value of `serverName` **exactly**.
- `Host` should match the host you access the site in the browser with, excluding `.test`. E.G. `site-name.test` becomes `site-name` for the `Host` field.
- `Port` can leave as default `80`.
- `Use path mappings` should be enabled, and you will need to setup 1 mapping; your local `site-name-test/wordpress` folder should be mapped to `/var/www/html`
6. In PHPStorm, open Settings -> Languages & Frameworks -> PHP -> Debug and ensure the following settings are configured:
- `Can accept external connections` should be enabled
- `Force break at first line when no path mapping specified` can be enabled, though it is more convenient to disable it (once you've ensured your path mapping works properly at least once)
- `Force break at first line when a script is outside the project` can be enabled, though it is more convenient to disable it
7. In PHPStorm, run the "Start Listening for PHP Debug Connections" tool ![Markup on 2021-03-18 at 09:26:34](https://user-images.githubusercontent.com/4182573/111633599-0f050f00-87cc-11eb-8449-6a4131f06043.png)
8. Within your project, set a breakpoint in a PHP file where you know will be executed
9. Reload the page and you should immediately see the Debug tool window open in PHPStorm, breaking on the line you have added the breakpoint to

