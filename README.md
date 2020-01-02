# Magento 2 Docker-compose project

This docker-compose project use few containers:
 - nginx
 - php7.3-fpm
 - mariadb
 - mailhog

Docker-compose will clone magento repo, run composer install and magento install
All those could be changed in .env file

Domain name http://mage.localhost
SSH root pass: 123123q
You may want to configure your code changes/sync using ssh connection
 
 # build
 docker-compose build
 # run
 docker-compose up
 # connect using ssh
 ssh -p 2222 root@localhost
 # clean old ssh hash
 ssh-keygen -R [localhost]:2222
 # clean 
 docker-compose down
 # hard clean
 docker-compose down --rmi all -v
 # super hard clean
 docker rm -f $(docker ps -q -a)
 
 docker rmi -f $(docker images -q)
