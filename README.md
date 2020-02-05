# Vagrant + Xdebug + Visual Studio Code
HOW-TO: Use Xdebug with Visual Studio Code on a Vagrant Machine

### Required
- Vagrant 2.2.6
- Virtual Box 5
- Visual Studio Code 1.41.1
- PHP Debug extension by Felix Becker
  https://github.com/felixfbecker/vscode-php-debug

### Tested with 
- Laravel/Homestead Box 9.1.0 (Ubuntu 18.04.03 LTS / PHP 7.4)



## VAGRANT
<code>vagrant up</code>

<code>vagrant ssh</code>



## XDEBUG

### Download xdebug

<code>sudo apt-get install php-xdebug</code>

### Configure xdebug

<code>sudo nano /etc/php/7.4/mods-available/xdebug.ini</code>

copy and paste

<blockquote>

zend_extension=xdebug.so

xdebug.remote_enable = 1

xdebug.remote_connect_back=1

xdebug.remote_autostart = true

xdebug.remote_port = 9000 #optional

</blockquote>

### Do symbolic linking
<code>sudo ln -s /etc/php/7.4/mods-available/xdebug.ini /etc/php/7.4/fpm/conf.d/20-xdebug.ini</code>

<code>sudo ln -s /etc/php/7.4/mods-available/xdebug.ini /etc/php/7.4/cli/conf.d/20-xdebug.ini</code>

https://blog.theodo.com/2016/08/configure-xdebug-phpstorm-vagrant/

### Do restart
PHP
<code>sudo systemctl restart php7.4-fpm</code>

Nginx
<code>sudo systemctl restart nginx</code>

### Check if xdebug is enabled with php
<code>php -v</code>



## VISUAL STUDIO CODE

### Configuration
<code>{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Pentadiet",
            "type": "php",
            "request": "launch",
            "port": 9000,
            "pathMappings": {
                "/home/vagrant/laravel/": "${workspaceRoot}",
            },
            "log": true
        },
    ]}  
 </code>
