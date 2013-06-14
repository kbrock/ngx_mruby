## What's ngx_mruby

ngx_mruby - It is mruby embedded in an nginx server. Similar to mod_mruby, which works for apache.

nginx modules can be implemeted by mruby scripts on nginx installed ngx_mruby.

## How to use

### Install prerequesites
    mac:
        brew install
        Install pcre lib

### Download

        git clone git://github.com/matsumoto-r/ngx_mruby.git
        cd ngx_mruby
        git submodule init
        git submodule update

        mkdir nginx
        wget http://nginx.org/download/nginx-1.2.2.tar.gz
        tar -xzf nginx-1.2.2.tar.gz -c nginx

### Build

* sample mruby build (example: include some mrbgems)

        mruby_root=/usr/local/src/mruby (I did not need ...)

* ngx_mruby build

        ./configure --enable-mrbgems --with-ngx-src-root=nginx/nginx-1.2.2 --with-ngx-config-opt="--prefix=/usr/local/nginx.new --with-ld-opt=-L/usr/local/lib" --with-mruby-root=./mruby
        make


### Install

    mac with homebrew:
        make install

    linux:
        sudo make install

### Change /usr/local/nginx.new/nginx.conf

        bind port 8080; #was 80

        location /mruby {
            mruby_content_handler /usr/local/nginx.new/html/hello.mrb;
        }

### Create mruby script /usr/local/nginx.new/html/hello.mrb

        Nginx.rputs(Time.now.to_s + "hello mruby world for nginx.")

### Start nginx

        /usr/local/nginx.new/sbin/nginx

### open http://localhost:8080/mruby

        Sat Jul 28 18:05:51 2012 hello mruby world for nginx.

Display above. Welcome mruby world for nginx!!


# License
under the MIT License:

* http://www.opensource.org/licenses/mit-license.php

