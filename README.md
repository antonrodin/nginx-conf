# My Nginx Config Files and CheatSheet

* Conf file: /etc/nginx
* Log file: /var/log/nginx/
* Php-fpm file: /etc/php-fpm.d/www.conf

## Basic commands

* service nginx status (Should run with every conf changes)
* service nginx reload
* service nginx status
* service nginx stop
* service nginx start
* service nginx help (They are some more)

## Workers
The 'auto' value sets the number of workers to the number of cores availables of the CPU
worker_processes auto;

If you want to know the number of cores that you have, the shell command "nproc" show you that. Also the 'lscpu' provides a lot of more details about CPU.


## Connections

With 2 worker processes and 1024 conections, the number of maximum conections is 2*1024. The maximum amount of connections that you server can handle is known by "ulimit -u"

```shell
worker_processes 2;

events {
    worker_connections 1024;
    
    # Accept all new connection simultaniusly
    multi_accept on;
    use epoll;
}
´´´