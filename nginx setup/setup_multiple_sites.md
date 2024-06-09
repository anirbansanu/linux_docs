# Setting Up Multiple Virtual Hosts with Nginx on Linux Mint

To set up multiple virtual hosts (websites) using Nginx on your local computer with Linux Mint OS, you need to create separate server blocks for each site. Here’s how to do it:

## 1. Install Nginx and PHP

If you haven't already installed Nginx and PHP, you can do so with the following commands:

```sh
sudo apt update
sudo apt install nginx php-fpm
```

## 2. Create Directory Structure

Create a directory for each website:

```sh
sudo mkdir -p /var/www/site1.local
sudo mkdir -p /var/www/site2.local
sudo mkdir -p /var/www/site3.local
sudo mkdir -p /var/www/site4.local
sudo mkdir -p /var/www/site5.local
sudo mkdir -p /var/www/site6.local
sudo mkdir -p /var/www/site7.local
sudo mkdir -p /var/www/site8.local
sudo mkdir -p /var/www/site9.local
sudo mkdir -p /var/www/site10.local
```

## 3. Set Directory Permissions

Ensure the directories are readable by Nginx:

```sh
sudo chown -R $USER:$USER /var/www/site1.local
sudo chown -R $USER:$USER /var/www/site2.local
sudo chown -R $USER:$USER /var/www/site3.local
sudo chown -R $USER:$USER /var/www/site4.local
sudo chown -R $USER:$USER /var/www/site5.local
sudo chown -R $USER:$USER /var/www/site6.local
sudo chown -R $USER:$USER /var/www/site7.local
sudo chown -R $USER:$USER /var/www/site8.local
sudo chown -R $USER:$USER /var/www/site9.local
sudo chown -R $USER:$USER /var/www/site10.local
sudo chmod -R 755 /var/www/site1.local
sudo chmod -R 755 /var/www/site2.local
sudo chmod -R 755 /var/www/site3.local
sudo chmod -R 755 /var/www/site4.local
sudo chmod -R 755 /var/www/site5.local
sudo chmod -R 755 /var/www/site6.local
sudo chmod -R 755 /var/www/site7.local
sudo chmod -R 755 /var/www/site8.local
sudo chmod -R 755 /var/www/site9.local
sudo chmod -R 755 /var/www/site10.local
```

## 4. Create Sample Index Pages

Create an `index.php` file in each directory:

```sh
echo "<?php phpinfo(); ?>" > /var/www/site1.local/index.php
echo "<?php phpinfo(); ?>" > /var/www/site2.local/index.php
echo "<?php phpinfo(); ?>" > /var/www/site3.local/index.php
echo "<?php phpinfo(); ?>" > /var/www/site4.local/index.php
echo "<?php phpinfo(); ?>" > /var/www/site5.local/index.php
echo "<?php phpinfo(); ?>" > /var/www/site6.local/index.php
echo "<?php phpinfo(); ?>" > /var/www/site7.local/index.php
echo "<?php phpinfo(); ?>" > /var/www/site8.local/index.php
echo "<?php phpinfo(); ?>" > /var/www/site9.local/index.php
echo "<?php phpinfo(); ?>" > /var/www/site10.local/index.php
```

## 5. Create Nginx Server Blocks

Create separate configuration files for each site in `/etc/nginx/sites-available`. For example:

```sh
sudo nano /etc/nginx/sites-available/site1.local
```

Add the following configuration for `site1.local`:

```nginx
server {
    listen 80;
    server_name site1.local;
    root /var/www/site1.local;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.4-fpm.sock; # Adjust PHP version if needed
    }

    location ~ /\.ht {
        deny all;
    }
}
```

Repeat this process for each site (site2.local, site3.local, etc.).

## 6. Enable the Server Blocks

Enable the server blocks by creating symbolic links in the `/etc/nginx/sites-enabled` directory:

```sh
sudo ln -s /etc/nginx/sites-available/site1.local /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/site2.local /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/site3.local /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/site4.local /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/site5.local /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/site6.local /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/site7.local /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/site8.local /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/site9.local /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/site10.local /etc/nginx/sites-enabled/
```

## 7. Update `/etc/hosts` File

Edit the `/etc/hosts` file to map the local domain names to `localhost`:

```sh
sudo nano /etc/hosts
```

Add the following lines:

```plaintext
127.0.0.1 site1.local
127.0.0.1 site2.local
127.0.0.1 site3.local
127.0.0.1 site4.local
127.0.0.1 site5.local
127.0.0.1 site6.local
127.0.0.1 site7.local
127.0.0.1 site8.local
127.0.0.1 site9.local
127.0.0.1 site10.local
```

## 8. Test Nginx Configuration and Restart

Test the Nginx configuration for syntax errors and then restart Nginx:

```sh
sudo nginx -t
sudo systemctl restart nginx
```

## 9. Access the Websites

Open your web browser and visit `http://site1.local`, `http://site2.local`, etc. You should see the PHP info page for each site.

By following these steps, you can host multiple websites on your local machine using Nginx and PHP on Linux Mint.
