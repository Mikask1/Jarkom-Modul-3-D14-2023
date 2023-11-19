## Nomor 1
Lakukan konfigurasi sesuai dengan peta yang sudah diberikan.
- Aura
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.198.4.10
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.198.1.10
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.198.2.10
	netmask 255.255.255.0

auto eth4
iface eth4 inet static
	address 192.198.3.10
	netmask 255.255.255.0
```
- Heiter
```
auto eth0
iface eth0 inet static
	address 192.198.1.2
	netmask 255.255.255.0
	gateway 192.198.1.10
```


- Himmel
```
auto eth0
iface eth0 inet static
	address 192.198.1.1
	netmask 255.255.255.0
	gateway 192.198.1.10
```

- Denken
```
auto eth0
iface eth0 inet static
	address 192.198.2.2
	netmask 255.255.255.0
	gateway 192.198.2.
```

- Eisen 
```
auto eth0
iface eth0 inet static
	address 192.198.2.3
	netmask 255.255.255.0
	gateway 192.198.2.1
```

- Lawine 
```
auto eth0
iface eth0 inet static
	address 192.198.3.2
	netmask 255.255.255.0
	gateway 192.198.3.1
```

- Linie 
```
auto eth0
iface eth0 inet static
	address 192.198.3.3
	netmask 255.255.255.0
	gateway 192.198.3.1
```

- Lugner

```
auto eth0
iface eth0 inet static
	address 192.198.3.4
	netmask 255.255.255.0
	gateway 192.198.3.1
```

- Frieren
```
auto eth0
iface eth0 inet static
	address 192.198.4.2
	netmask 255.255.255.0
	gateway 192.198.4.1
```
- Flamme
```
auto eth0
iface eth0 inet static
	address 192.198.4.3
	netmask 255.255.255.0
	gateway 192.198.4.1
```

- Fern
```
auto eth0
iface eth0 inet static
	address 192.198.4.4
	netmask 255.255.255.0
	gateway 192.198.4.1
```

- Client 
```
auto eth0
iface eth0 inet dhcp
```

### Simpan di `.bashrc`

DHCP Relay
 
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.198.0.0/16
```

DNS Server 
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install bind9 -y  
```


DHCP Server
```
echo nameserver 192.198.1.2 > /etc/resolv.conf  
apt-get update
apt install isc-dhcp-server -y
````
DHCP Relay 

	apt-get update
	apt install isc-dhcp-relay -y
	


Load Balancer

	echo nameserver 192.198.1.2 > /etc/resolv.conf  
	apt-get update
	apt-get install nginx -y
	apt-get install lynx -y
	apt-get install apache2-utils -y
	service nginx start

Database Server

	echo nameserver 192.198.1.2 > /etc/resolv.conf
	apt-get update
	apt-get install mariadb-server -y
	service mysql start



Workers PHP

	
	echo nameserver 192.198.1.2 > /etc/resolv.conf
	apt-get update
	apt-get install nginx -y
	apt-get install wget -y
	apt-get install unzip -y
	apt-get install lynx -y
	apt-get install htop -y
	apt-get install apache2-utils -y
	apt-get install php7.3-fpm php7.3-common php7.3-mysql php7.3-gmp php7.3-curl php7.3-intl php7.3-mbstring php7.3-xmlrpc php7.3-gd php7.3-xml php7.3-cli php7.3-zip -y
	
	service nginx start
	service php7.3-fpm start

Workers Laravel

	echo nameserver 192.198.1.2 > /etc/resolv.conf
	apt-get update
	apt-get install lynx -y
	apt-get install mariadb-client -y
	apt-get install -y lsb-release ca-certificates   apt-transport-https software-properties-common gnupg2
	curl -sSLo /usr/share/keyrings/deb.sury.org-php.gpg https://packages.sury.org/php/apt.gpg
	sh -c 'echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
	apt-get update
	apt-get install php8.0-mbstring php8.0-xml php8.0-cli   php8.0-common php8.0-intl php8.0-opcache php8.0-readline php8.0-mysql php8.0-fpm php8.0-curl unzip wget -y
	apt-get install nginx -y
	service nginx start
	service php8.0-fpm start


Client 
	
	apt update
	apt install lynx -y
	apt install htop -y
	apt install apache2-utils -y
	apt-get install jq -y




## DNS Server

Pada `dnss.sh` di /root

```
echo '
zone "riegel.canyon.d14.com" {
	type master;
	file "/etc/bind/riegel.canyon/riegel.canyon.d14.com";
};

zone "granz.channel.d14.com" {
	type master;
	file "/etc/bind/granz.channel/granz.channel.d14.com";
};' > /etc/bind/named.conf.local
```
```
mkdir /etc/bind/riegel.canyon
mkdir /etc/bind/granz.channel
```
```
echo ';
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     riegel.canyon.d14.com. root.riegel.canyon.d14.com. (
                         2022100601;    ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      riegel.canyon.d14.com.
@       IN      A       192.198.2.3   ; IP Load Balancer' > /etc/bind/riegel.canyon/riegel.canyon.d14.com
```
```
echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     granz.channel.d14.com. root.granz.channel.d14.com. (
                         2022100601;    ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      granz.channel.d14.com.
@       IN      A       192.198.2.3     ; IP Load Balancer' > /etc/bind/granz.channel/granz.channel.d14.com
```
```
echo 'options {
      directory "/var/cache/bind";

      forwarders {
              192.168.122.1;
      };

      // dnssec-validation auto;
      allow-query{any;};
      auth-nxdomain no;    # conform to RFC1035
      listen-on-v6 { any; };
};' > /etc/bind/named.conf.options
```
```
service bind9 start
```

## Nomor 1-5
DHCP Server

Pada `dhcps.sh` di /root

```
echo 'INTERFACESv4="eth0"' > /etc/default/isc-dhcp-server
```
```
echo 'subnet 192.198.1.0 netmask 255.255.255.0 {
} 
subnet 192.198.3.0 netmask 255.255.255.0 {
	range 192.198.3.16 192.198.3.32;
	range 192.198.3.64 192.198.3.80;
	option routers 192.198.3.10;
	option broadcast-address 192.198.3.255;
	option domain-name-servers 192.198.1.2;
	default-lease-time 180;
	max-lease-time 5760;
}

subnet 192.198.4.0 netmask 255.255.255.0 {
	range 192.198.4.12 192.198.4.20;
	range 192.198.4.160 192.198.4.168;
	option routers 192.198.4.10;
	option broadcast-address 192.198.4.255;
	option domain-name-servers 192.198.1.2;
	default-lease-time 720;
	max-lease-time 5760;
}' > /etc/dhcp/dhcpd.conf
```
```
service isc-dhcp-server restart
```

DHCP Relay

Pada dhcpr.sh di /root

```
echo'
SERVERS="192.198.1.1" # IP DHCP Server
INTERFACES="eth1 eth2 eth3 eth4"
OPTIONS=""' > /etc/default/isc-dhcp-relay
```
```
echo 'net.ipv4.ip_forward=1' > /etc/sysctl.conf
service isc-dhcp-relay restart
```

## Nomor 6

PHP Workers

Pada `phpw.sh` di /root

```
cd /var/www
curl -L -o granz.channel.d14.com.zip "https://drive.google.com/uc?export=download&id=1ViSkRq7SmwZgdK64eRbr5Fm1EGCTPrU1" && unzip granz.channel.d14.com.zip && rm granz.channel.d14.com.zip && mv modul-3 granz.channel.d14.com
```
```
echo '
server {
    listen 80;
    server_name _;

    root /var/www/granz.channel.d14.com;
    index index.php index.html index.htm;

    
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.3-fpm.sock;  # Sesuaikan versi PHP dan socket
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    
    }
}' > /etc/nginx/sites-available/default
```
```
service nginx restart
service php7.3-fpm start
```


- Load Balancer
Pada `lb.sh` di /root

```
echo 'upstream phpserver  {
	server 192.198.3.1; #IP Lawine
	server 192.198.3.2; #IP Linie
	server 192.198.3.3; #IP Lugner
}

server {
	listen 80;
	server_name riegel.canyon.d14.com;

	location / {
		proxy_pass http://phpserver;
	}
}

upstream laravelserver  {
	server 192.198.4.1:8001; #IP Frieren
	server 192.198.4.2:8002; #IP Flamme
	server 192.198.4.3:8003; #IP Fern
}

server {
	listen 80;
	server_name granz.channel.d14.com;

	location / {
		proxy_pass http://laravelserver;
	}
}

server {
        listen 80;
        server_name granz.channel.d14.com;

        location / {
    allow 192.173.3.69;
    allow 192.173.3.70;
    allow 192.173.4.167;
    allow 192.173.4.168;
    deny all;
                proxy_pass http://phpserver;

        }

        location ~ /its {
	proxy_pass https://www.its.ac.id;
        proxy_set_header Host www.its.ac.id;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
server {
    listen 80;
    server_name riegel.canyon.d14.com www.riegel.canyon.d14.com;
      location / {
        proxy_pass http://laravelserver;
    }
}' >  /etc/nginx/sites-available/default
```
```
service nginx restart
```








## Nomor 7
Pada salah satu Client
```
apt install apache2-utils -y
ab -n 1000 -c 100 http://riegel.canyon.d14.com
```

## Nomor 8
Pada semua PHP Worker
```
apt install htop
```
## Nomor 9
Lihat Grimoire

## Nomor 10
Pada LB Eisen 
```
mkdir /etc/nginx/rahasisakita
```
```
htpasswd -c /etc/nginx/.htpasswd netics
```
```
password : ajkd14
```

`nano /etc/nginx/sites-available/default` di dalamnya 
	
	auth_basic "Administrator's Area";
	auth_basic_user_file /etc/nginx/rahasisakita/htpasswd;



## Nomor 11
Pada LB Eisen

edit `nano /etc/nginx/sites-available/default` dan tambahkan : 

	location ~ /its {
	    proxy_pass https://www.its.ac.id;
	    proxy_set_header Host www.its.ac.id;
	    proxy_set_header X-Real-IP $remote_addr;
	    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	}

## Nomor 12 
Pada LB Eisen

edit `nano /etc/nginx/sites-available/default` dan tambahkan : 
	
	location / {
	    allow 192.198.3.69;
	    allow 192.198.3.70;
	    allow 192.198.4.167;
	    allow 192.198.4.168;
	    deny all;
	    proxy_pass http://phpserver;
	    
	}


## Nomor 13

Pada database server:
```
echo nameserver 192.198.1.3  > /etc/resolv.conf
apt-get update
apt-get install mariadb-server -y
```
`nano /etc/mysql/my.cnf` kemudian edit kemudian edit
dan tambahkan : 


	[mysqld]
	skip-networking=0
	skip-bind-addres
 
Menjadi : 

	!includedir /etc/mysql/conf.d/
	!includedir /etc/mysql/mariadb.conf.d/
	[mysqld]
	skip-networking=0
	skip-bind-address

Kemudian edit file `/etc/mysql/mariadb.conf.d/50-server.cnf` dan ganti `bind-adress` menjadi `0.0.0.0`

Kemudian restart mysql.

Setelah itu login mysql dengan menggunakan `mysql -u root `
Kemudian lakukan 
```
CREATE DATABASE KAMAL;
CREATE USER 'kamal'@'%' IDENTIFIED BY 'kamal';
CREATE USER 'kamal'@'localhost' IDENTIFIED BY 'kamal';
GRANT ALL PRIVILEGES ON . TO 'kamal'@'%';
GRANT ALL PRIVILEGES ON . TO 'kamal'@'localhost';
```

Kemudian cek dari worker


# Nomor 14



Pada worker php install composer dan git 
```
wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
mv composer.phar /usr/local/bin/composer
```
```
apt-get install git -y
```	
Kemudian clone repo tersebut dan lakukan composer update

	cd /var/www && git clone https://github.com/martuafernando/laravel-praktikum-jarkom
	cd /var/www/laravel-praktikum-jarkom 
	composer update 


dbb.sh :

```
wget https://getcomposer.org/download/2.0.13/composer.phar
chmod +x composer.phar
apt-get install git -y
```
```
cd /var/www && git clone https://github.com/martuafernando/laravel-praktikum-jarkom
cd /var/www/laravel-praktikum-jarkom 
composer update 
cp .env.example .env
```

```
echo '
APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=192.198.2.1
DB_PORT=3306
DB_DATABASE=KAMAL
DB_USERNAME=kamal
DB_PASSWORD=kamal

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"' > /var/www/laravel-praktikum-jarkom/.env
```
```
php artisan key:generate
php artisan config:cache
php artisan migrate
php artisan db:seed
php artisan storage:link
php artisan jwt:secret
php artisan config:clear
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
```
```
echo '
server {
    listen 8002;

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
      include snippets/fastcgi-php.conf;
      fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

    location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;
}' >  /etc/nginx/sites-available/default
```






Lalu edit file `/var/www/laravel-praktikum-jarkom/.env` menjadi :
```
APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_DEPRECATIONS_CHANNEL=null
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=192.198.2.1
DB_PORT=3306
DB_DATABASE=KAMAL
DB_USERNAME=kamal
DB_PASSWORD=kamal

BROADCAST_DRIVER=log
CACHE_DRIVER=file
FILESYSTEM_DISK=local
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

MEMCACHED_HOST=127.0.0.1

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
AWS_USE_PATH_STYLE_ENDPOINT=false

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_HOST=
PUSHER_PORT=443
PUSHER_SCHEME=https
PUSHER_APP_CLUSTER=mt1

VITE_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
VITE_PUSHER_HOST="${PUSHER_HOST}"
VITE_PUSHER_PORT="${PUSHER_PORT}"
VITE_PUSHER_SCHEME="${PUSHER_SCHEME}"
VITE_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}" 
```

Kemudian lakukan command berikut pada directory `/var/www/laravel-praktikum-jarkom`
```
php artisan key:generate
php artisan config:cache
php artisan migrate
php artisan db:seed
php artisan storage:link
php artisan jwt:secret
php artisan config:clear
chown -R www-data.www-data /var/www/laravel-praktikum-jarkom/storage
```

Lalu edit config nginx dengan menggunakan `nano /etc/nginx/sites-available/default` menjadi 
```
server {
    listen [port number];

    root /var/www/laravel-praktikum-jarkom/public;

    index index.php index.html index.htm;
    server_name _;

    location / {
            try_files $uri $uri/ /index.php?$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
      include snippets/fastcgi-php.conf;
      fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
    }

    location ~ /\.ht {
            deny all;
    }

    error_log /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;
}
```
Kemudian testing menggunakan lynx localhost:port tergantung yang sudah diassigned



## Nomor 15

Pada salah satu client yaitu  buat `register.json` untuk register 

```
{
    "username": "kamal",
    "password": "kamal"
}
```

Kemudian testing dari client 
```
ab -n 100 -c 10 -p register.json -T application/json http://192.198.4.2:8002/api/auth/register
```

## Nomor 16
Buat nano `login.json` yang berisi 
```
{
    "username": "kamal",
    "password": "kamal"
}
```

Lalu jalankan 
```
ab -n 100 -c 10 -p login.json -T application/json http://192.198.4.2:8002/api/auth/login
```
# Nomor 17
```
curl -X POST -H "Content-Type: application/json" -d @login.json http://192.198.4.2:8002/api/auth/login > login_output.txt
```
```
token=$(cat login_output.txt | jq -r '.token')
```
```
ab -n 100 -c 10 -H "Authorization: Bearer $token" http://192.198.4.2:8002/api/me
```


# Nomor 18
Pada LB 


	server {
	    listen 80;
	    server_name riegel.canyon.d14.com www.riegel.canyon.d14.com;
	
	    location / {
	        proxy_pass http://laravelserver;
	    }
	} 


Testing dari client 
```
ab -n 100 -c 10 -p login.json -T application/json http://riegel.canyon.d14.com/api/auth/login
```

# Nomor 19 

Pada laravel worker gunakan script berikut



		
		[www]
		user = www-data
		group = www-data
		listen = /run/php/php8.0-fpm.sock
		listen.owner = www-data
		listen.group = www-data
		php_admin_value[disable_functions] = exec,passthru,shell_exec,system
		php_admin_flag[allow_url_fopen] = off
		; Choose how the process manager will control the number of child processes.
		pm = dynamic
		pm.max_children = 15 
		pm.start_servers = 12 
		pm.min_spare_servers = 2 
		pm.max_spare_servers = 13
		'


		[www]
		user = www-data
		group = www-data
		listen = /run/php/php8.0-fpm.sock
		listen.owner = www-data
		listen.group = www-data
		php_admin_value[disable_functions] = exec,passthru,shell_exec,system
		php_admin_flag[allow_url_fopen] = off
		; Choose how the process manager will control the number of child processes.
		pm = dynamic
		pm.max_children = 25 
		pm.start_servers = 22 
		pm.min_spare_servers = 3 
		pm.max_spare_servers = 23


		
		[www]
		user = www-data
		group = www-data
		listen = /run/php/php8.0-fpm.sock
		listen.owner = www-data
		listen.group = www-data
		php_admin_value[disable_functions] = exec,passthru,shell_exec,system
		php_admin_flag[allow_url_fopen] = off
		; Choose how the process manager will control the number of child processes.
		pm = dynamic
		pm.max_children = 30
		pm.start_servers = 25 
		pm.min_spare_servers = 4 
		pm.max_spare_servers = 25

Lalu testing dari client 











# Nomor 20

Tambahkan pada config nginx di LB

	
	
	upstream worker {
	    least_conn;
	    server 192.198.4.1:8001;
	    server 192.198.4.2:8002;
	    server 192.198.4.3:8003;
	}
	
	server {
	    listen 81;
	    server_name riegel.canyon.d14.com www.riegel.canyon.d14.com;
	
	    location / {
	        proxy_pass http://laravelserver;
	    }

Lalu test dari client




****
