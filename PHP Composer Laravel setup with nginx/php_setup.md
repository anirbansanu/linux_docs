# Installing PHP 7.4 and PHP 8.1 with Nginx on Linux

To install PHP 7.4 and PHP 8.1 alongside each other with Nginx on your Linux system, follow these steps:

## 1. Add PHP Repository

First, add the `ondrej/php` repository, which contains various PHP versions. Open a terminal and run:

```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update
```

## 2. Install PHP 7.4 and PHP 8.1

Install PHP 7.4 and PHP 8.1 along with necessary extensions:

```bash
sudo apt install php7.4 php7.4-fpm php7.4-mysql php7.4-mbstring php7.4-xml
```
####  For php 8.1
```bash
sudo apt install php8.1 php8.1-fpm php8.1-mysql php8.1-mbstring php8.1-xml php8.1-common php8.1-curl php8.1-gd php8.1-imagick php8.1-soap php8.1-zip php8.1-intl
```
## 3. Configure Nginx to Use PHP-FPM for Each Version

Edit Nginx server block configuration files for PHP 7.4 and PHP 8.1:

```bash
sudo nano /etc/nginx/sites-available/default
```

For PHP 7.4:

```nginx
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
}
```

For PHP 8.1:

```nginx
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
}
```

Save the changes and exit the editor.

## 4. Install Additional PHP Extensions

Depending on your requirements, install additional PHP extensions for each PHP version. Common extensions include `php7.4-common`, `php7.4-curl`, `php7.4-gd`, `php7.4-imagick`, and others. Similarly, install the corresponding extensions for PHP 8.1.

```bash
sudo apt install php7.4-common php7.4-curl php7.4-gd php7.4-imagick ...
sudo apt install php8.1-common php8.1-curl php8.1-gd php8.1-imagick ...
```

## 5. Verify PHP Installation

Create PHP info files for each PHP version to verify installation and configuration. Create new files named `info.php` in your web server's document root (usually `/var/www/html`) for PHP 7.4 and PHP 8.1 with the following content:

For PHP 7.4:

```php
<?php
phpinfo();
```

For PHP 8.1:

```php
<?php
phpinfo();
```

Save the files and access them in your web browser by navigating to `http://your_server_ip/info.php` and `http://your_server_ip/info.php` respectively. You should see pages displaying PHP information for both versions.

That's it! You now have PHP 7.4 and PHP 8.1 installed and configured to work with Nginx on your Linux system.
