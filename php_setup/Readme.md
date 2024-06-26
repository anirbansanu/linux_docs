## Managing and Setting Multiple PHP and PHP-FPM Versions

This documentation will guide you through the process of managing and setting multiple PHP and PHP-FPM versions on a Debian-based system (such as Ubuntu, Linux Mint, or Kali Linux) using the `update-alternatives` tool.

### Prerequisites
- A Debian-based Linux distribution.
- Administrative (sudo) access to your system.

### Step 1: Add the PHP Repository
To ensure you have access to the latest PHP versions, add the repository maintained by Ondřej Surý.

1. **Add the repository**:
   ```bash
   sudo add-apt-repository ppa:ondrej/php
   sudo apt update
   ```

### Step 2: Install Multiple PHP Versions
Install the desired PHP versions along with their extensions. Here, we will install PHP 7.4, PHP 8.1, and PHP 8.2.

1. **Install PHP 7.4**:
   ```bash
   sudo apt install php7.4 php7.4-fpm php7.4-mysql php7.4-mbstring php7.4-xml php7.4-common php7.4-curl php7.4-gd php7.4-imagick php7.4-soap php7.4-zip php7.4-intl
   ```

2. **Install PHP 8.1**:
   ```bash
   sudo apt install php8.1 php8.1-fpm php8.1-mysql php8.1-mbstring php8.1-xml php8.1-common php8.1-curl php8.1-gd php8.1-imagick php8.1-soap php8.1-zip php8.1-intl
   ```

3. **Install PHP 8.2**:
   ```bash
   sudo apt install php8.2 php8.2-fpm php8.2-mysql php8.2-mbstring php8.2-xml php8.2-common php8.2-curl php8.2-gd php8.2-imagick php8.2-soap php8.2-zip php8.2-intl
   ```

### Step 3: Register PHP Versions with `update-alternatives`
Register each installed PHP version with the `update-alternatives` tool.

1. **Register PHP 7.4**:
   ```bash
   sudo update-alternatives --install /usr/bin/php php /usr/bin/php7.4 74
   ```

2. **Register PHP 8.1**:
   ```bash
   sudo update-alternatives --install /usr/bin/php php /usr/bin/php8.1 81
   ```

3. **Register PHP 8.2**:
   ```bash
   sudo update-alternatives --install /usr/bin/php php /usr/bin/php8.2 82
   ```

### Step 4: Set the Default PHP Version
Use the `update-alternatives` tool to set the default PHP version.

1. **Configure the default PHP version**:
   ```bash
   sudo update-alternatives --config php
   ```

   This command will display a list of available PHP versions. Select the version you want to set as the default by entering the corresponding number.

   Example output:
   ```
   There are 3 choices for the alternative php (providing /usr/bin/php).

     Selection    Path             Priority   Status
   ------------------------------------------------------------
   * 0            /usr/bin/php8.2   82        auto mode
     1            /usr/bin/php7.4   74        manual mode
     2            /usr/bin/php8.1   81        manual mode
     3            /usr/bin/php8.2   82        manual mode

   Press <enter> to keep the current choice[*], or type selection number: 2
   ```

2. **Select the desired version** by typing the corresponding number and pressing Enter.

### Step 5: Verify the Default PHP Version
Check the current default PHP version to ensure the switch was successful.

1. **Verify the PHP version**:
   ```bash
   php -v
   ```

### Managing PHP-FPM
If you are using PHP-FPM, you need to update the default PHP-FPM version as well.

1. **Register PHP-FPM versions**:
   ```bash
   sudo update-alternatives --install /usr/sbin/php-fpm php-fpm /usr/sbin/php-fpm7.4 74
   sudo update-alternatives --install /usr/sbin/php-fpm php-fpm /usr/sbin/php-fpm8.1 81
   sudo update-alternatives --install /usr/sbin/php-fpm php-fpm /usr/sbin/php-fpm8.2 82
   ```

2. **Configure the default PHP-FPM version**:
   ```bash
   sudo update-alternatives --config php-fpm
   ```

3. **Verify the PHP-FPM version**:
   ```bash
   php-fpm -v
   ```

### Switching Between PHP Versions
To switch between different PHP versions at any time, use the `update-alternatives --config php` command and select the desired version.

### Switching Between PHP-FPM Versions
To switch between different PHP-FPM versions at any time, use the `update-alternatives --config php-fpm` command and select the desired version. After switching, restart the PHP-FPM service to apply the changes.

1. **Restart the PHP-FPM service**:
   ```bash
   sudo systemctl restart php7.4-fpm
   sudo systemctl restart php8.1-fpm
   sudo systemctl restart php8.2-fpm
   ```

### Summary
By following these steps, you can easily manage and switch between multiple PHP and PHP-FPM versions on your Debian-based system using the `update-alternatives` tool. This allows you to test and run applications with different PHP versions as needed.

If you encounter any issues or have further questions, please refer to the official documentation or seek support from the community.