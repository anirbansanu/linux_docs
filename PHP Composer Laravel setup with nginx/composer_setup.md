# How to Install Composer on Linux

Composer is a dependency manager for PHP that allows you to easily manage your PHP dependencies. If you’re a developer working on Linux and want to use Composer for your PHP development, you can follow these simple steps to install Composer on your machine.

## Step 1: Update Your System

Before installing Composer, it’s a good idea to update your system. Run the following command in your terminal app to update your system:

```bash
sudo apt-get update
```

This command will update your system with the latest packages.

## Step 2: Install Composer Dependencies

To install the dependencies required for Composer, run the following command in your terminal app:

```bash
sudo apt-get install curl php-cli php-mbstring git unzip
```

This command will install the required dependencies for Composer on your machine.

## Step 3: Download Composer

To download the Composer installer, run the following command in your terminal app:

```bash
curl -sS https://getcomposer.org/installer -o composer-setup.php
```

This command will download the Composer installer to your current working directory.

## Step 4: Verify the Composer Installer

To verify the Composer installer, run the following command in your terminal app:

```bash
php composer-setup.php --check
```

This command will verify the installer and ensure that it’s not corrupted.

## Step 5: Install Composer

To install Composer globally on your machine, run the following command in your terminal app:

```bash
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

This command will install Composer globally on your machine.

## Step 6: Verify Composer Installation

To verify that Composer is installed correctly, run the following command in your terminal app:

```bash
composer --version
```

This command will display the version of Composer installed on your machine. If the command displays the version of Composer, then Composer has been successfully installed.

---

Congratulations! You have successfully installed Composer on your Linux machine. You can now use Composer to manage your PHP dependencies for your web applications and software.
