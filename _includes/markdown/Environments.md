## Create an Environment

`10updocker create` will present you with a series of prompts to configure your environment to suit your needs.
It is recommended that you use the `.test` top level domain (TLD) for your local environments, as this TLD is reserved 
for the testing of software and is not intended to ever be installed into the global Domain Name System.

## Delete an Environment

`10updocker delete <hostname>` will delete an environment with the given hostname. Any local files, docker volumes, and 
databases related to the environment will be deleted permanently.

## Stop an Environment

`10updocker stop <hostname>` will stop an environment from running while retaining all files, docker volumes, and databases
related to the environment.

A special hostname `all` is available that will stop all running environments as well as the global services.

## Start an Environment

`10updocker start <hostname>` will start a preexisting environment.

A special hostname `all` is available that will start all environments as well as the global services.

## Restart an Environment

`10updocker restart <hostname>` will restart all services associated with a preexisting environment.

A special hostname `all` is available that will restart all environments as well as the global services.

## WP Snapshots

See the section on [using WP Snapshots](../wp-snapshots)

## Running WP CLI Commands

Running WP CLI commands against an environment is easy. First, make sure you are somewhere within your environment
directory (by default, this is somewhere within `~/wp-local-docker-sites/<environment>/`). Once within the environment
directory, simply run `10updocker wp <command>`. `<command>` can be any valid command you would otherwise pass directly
to WP CLI.

Examples:
* `10updocker wp search-replace 'mysite.com' 'mysite.test'`
* `10updocker wp site list`

## Shell 

You can get a shell inside of any container in your environment using the `10updocker shell [<service>]` command. If a 
service is not provided, the `phpfpm` container will be used by default. Other available services can vary depending
on the options selected during creation of the environment, but may include:
* `phpfpm`
* `nginx`
* `elasticsearch`
* `memcached`

## Logs

Real time container logs are available using the `10updocker logs [<service>]` command. If a service is not provided,
logs from all containers in the current environment will be shown. To stop logs, type `ctrl+c`. Available services can
vary depending on the options selected during creation of the environment, but may include:
* `phpfpm`
* `nginx`
* `elasticsearch`
* `memcached`
