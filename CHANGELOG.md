# Changelog

## [1.0.0] - 2018-08-15
### Added
- CHANGELOG.md file to keep changes between versions.
- README.dm file for repository description.
- docker-compose.yml file with directives to run required containers.
- php/Dockerfile with instructions to raise php-fpm with required extensions and scripts to install Magento2 instance.
- nginx/Dockerfile to raise latest nginx image and copy configuration file from host to container.
- nginx/conf/test.com.conf file with required nginx configuration to run Magento2 instance.
