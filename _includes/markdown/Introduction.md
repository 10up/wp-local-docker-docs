WP Local Docker is an easy to use Docker based local development environment for WordPress development that works on Mac,
Windows, and Linux. Any number of environments can be created and may run at the same time<sup>1</sup>, and requests will be routed
appropriately to the correct environment based on the hostname specified during environment creation.
  
Each environment within WP Local Docker is powered by nginx, phpfpm, memcached, and if desired, elasticsearch. PHP versions 
5.5, 5.6, 7.0, 7.1, or 7.2 are all supported. Supporting all environments within WP Local Docker is MySQL container to run
all MySQL databases, WP Snapshots to easily push and pull snapshots of a WordPress installation, PHPMyAdmin to manage 
MySQL databases with a familiar UI, and mailcatcher to catch mail any mail sent from all environments.

In addition to the services required to run WordPress, WP Local Docker will also download and install WordPress as a
single site installation, a Multisite with Subdirectories, a Multisite with Subdomains, or the core development version.

----
<sub>1. Concurrent environments are limited by the available resources of your host machine</sub> 
