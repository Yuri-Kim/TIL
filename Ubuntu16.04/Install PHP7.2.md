## Install PHP  

Install PHP7.2 on Ubuntu 16.04  

### Update Ubuntu  

    $ apt-get update && apt-get upgrade  

### Add the PHP repository  

make sure you have the following package installed so you can add repositories  

    $ apt-get install software-properties-common  

add the PHP repository from Onderj  

    $ add-apt-repository ppa:ondrej/php  

update your package list  

    $ apt-get install php7.2  

### Install PHP 7.2  

install PHP7.2  

    $ apt-get install php7.2  

(This command will install additional packages : libapache2-mod-php7.2, libargon2-0, libsodium23, libssl1.1, php7.2-cli, php7.2-common, php7.2-json, php7.2-opcache, php7.2-readline)  

check php version  

    $ php -v  

### Install PHP 7.2 modules  

    $ apt-get install php-pear php7.2-curl php7.2-dev php7.2-gd php7.2-mbstring php7.2-zip php7.2-mysql php7.2-xml  


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQzNzY0MzM1MV19
-->