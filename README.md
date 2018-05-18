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

After any changes inside the configuration file, and before any reload, you can test it, like so:

```shell
nginx -t
```

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
```

# Use gzip to compress files

```
#inside of server context
server {
    
    # Enable Gzip
    gzip on;

    # Minimum for file in BYTES to start compress resource
    gzip_min_length 100;

    # Compression level, more compression -> more CPU usage.
    # The higher is the number, te higher compression is applied
    # Level higher than 5 also have very little effect
    # Recomenden value between 2 and 4
    gzip_comp_level 3;

    # Specify the types of files to compress
    gzip_types text/plain;
    gzip_types text/css;
    gzip_types text/javascript;

    # Disable compression for user header that mean, its wen from "Internet Explorer 6"
    gzip_disable "msie6";

}
```