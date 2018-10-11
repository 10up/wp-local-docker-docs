## Configuration

If you have not used WP Snapshots with WP Local Docker yet, you'll first need to configure WP Snapshots with your AWS
credentials. To configure, run `10updocker wpsnapshots configure <repository>` (e.g. `10updocker wpsnapshots configure 10up`). You will then be prompted to enter
your AWS credentials and a few other configuration details. Once complete, the configuration will be available across
all of your WP Local Docker environments.

## Pulling an Environment

`10updocker wpsnapshots pull <snapshot-id>` This command pulls an existing snapshot from the repository into your current
environment, replacing your database and wp-content. This command must be run from withing your environment directory 
(by default, this is somewhere within `~/wp-local-docker-sites/<environment>/`). 

## Searching for an Environment

`10updocker wpsnapshots search <search-term>` with searches the repository for snapshots. `<search-text>` will be 
compared against project names and authors. Searching for "*" will return all snapshots.

## Other Commands

`10updocker wpsnapshots <command>` is the general form for all WP Snapshots commands. `<command>` is passed directly to 
WP Snapshots, so any command that WP Snapshots accepts will work in this form. Any command that requires a WordPress
environment (pull, create, etc) needs to be run from somewhere within an environment directory (by default, this is
somewhere within `~/wp-local-docker-sites/<environment>/`).
