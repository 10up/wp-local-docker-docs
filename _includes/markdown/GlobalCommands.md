## Clearing Shared Cache
WP CLI, WP Snapshots, and npm (when building the development version of WordPress) all utilize cache to speed up 
operations and save on bandwidth in the future. 

`10updocker cache clear` Clears the WP CLI, WP Snapshots, and npm (for WordPress core development) caches.

## Updating Docker Images
`10updocker image update` Will determine which of the docker images utilized by WP Local Docker are present on your
system and update them to the latest version available. 
