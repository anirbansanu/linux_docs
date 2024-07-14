Sure! Here is a step-by-step guide for deploying a Laravel project on AWS using Nginx:

### Documentation for Deploying a Laravel Project to AWS with Nginx

#### Prerequisites
- A Laravel project ready for deployment.
- An AWS account.
- AWS CLI installed and configured.
- SSH client (e.g., PuTTY, Terminal).

#### Steps

1. **Set Up an AWS EC2 Instance:**
   - Log in to your AWS Management Console.
   - Navigate to the EC2 Dashboard and click on "Launch Instance."
   - Choose an Amazon Machine Image (AMI). For Laravel, an Ubuntu Server AMI is recommended.
   - Select an instance type (t2.micro is suitable for small projects and is free-tier eligible).
   - Configure the instance details, add storage, and add tags as needed.
   - Configure the security group to allow HTTP (port 80), HTTPS (port 443), and SSH (port 22) access.
   - Review and launch the instance. Download the key pair (.pem file) when prompted, and keep it secure.

2. **Connect to Your EC2 Instance:**
   - Open your terminal or SSH client.
   - Connect to your instance using the key pair:
     ```sh
     ssh -i /path/to/your-key-pair.pem ubuntu@your-ec2-public-dns
     ```

3. **Install Required Software:**
   - Update the package list and install necessary software:
     ```sh
     sudo apt update
     sudo apt install nginx php-fpm php-mysql php-xml php-mbstring php-zip curl unzip git
     sudo apt install mysql-server
     ```
   - Install Composer globally:
     ```sh
     curl -sS https://getcomposer.org/installer | php
     sudo mv composer.phar /usr/local/bin/composer
     ```

4. **Set Up MySQL Database:**
   - Secure MySQL installation:
     ```sh
     sudo mysql_secure_installation
     ```
   - Log in to MySQL and create a new database and user:
     ```sh
     sudo mysql -u root -p
     ```
     ```sql
     CREATE DATABASE your_database_name;
     CREATE USER 'your_database_user'@'localhost' IDENTIFIED BY 'your_database_password';
     GRANT ALL PRIVILEGES ON your_database_name.* TO 'your_database_user'@'localhost';
     FLUSH PRIVILEGES;
     EXIT;
     ```

5. **Deploy Your Laravel Project:**
   - Transfer your Laravel project files to the EC2 instance. You can use SCP (Secure Copy Protocol) or SFTP for this:
     ```sh
     scp -i /path/to/your-key-pair.pem -r /path/to/your-laravel-project ubuntu@your-ec2-public-dns:/var/www/laravel
     ```
   - Connect to your EC2 instance and navigate to the Laravel project directory:
     ```sh
     cd /var/www/laravel
     ```
   - Install Laravel dependencies:
     ```sh
     composer install
     ```
   - Set the appropriate permissions:
     ```sh
     sudo chown -R www-data:www-data /var/www/laravel
     sudo chmod -R 775 /var/www/laravel/storage
     sudo chmod -R 775 /var/www/laravel/bootstrap/cache
     ```

6. **Configure Nginx:**
   - Create a new server block configuration file for your Laravel project:
     ```sh
     sudo nano /etc/nginx/sites-available/laravel
     ```
   - Add the following configuration:
     ```nginx
     server {
         listen 80;
         server_name your-domain.com;

         root /var/www/laravel/public;
         index index.php index.html index.htm;

         location / {
             try_files $uri $uri/ /index.php?$query_string;
         }

         location ~ \.php$ {
             include snippets/fastcgi-php.conf;
             fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
             fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
             include fastcgi_params;
         }

         location ~ /\.ht {
             deny all;
         }
     }
     ```
     Replace `your-domain.com` with your actual domain name.

   - Enable the new server block configuration:
     ```sh
     sudo ln -s /etc/nginx/sites-available/laravel /etc/nginx/sites-enabled/
     ```
   - Test the Nginx configuration and restart Nginx:
     ```sh
     sudo nginx -t
     sudo systemctl restart nginx
     ```

7. **Update Environment Configuration:**
   - Open your Laravel project’s `.env` file and update the database configuration:
     ```env
     DB_CONNECTION=mysql
     DB_HOST=127.0.0.1
     DB_PORT=3306
     DB_DATABASE=your_database_name
     DB_USERNAME=your_database_user
     DB_PASSWORD=your_database_password
     ```
   - Generate a new application key:
     ```sh
     php artisan key:generate
     ```

8. **Run Database Migrations:**
   - Migrate your database:
     ```sh
     php artisan migrate
     ```

9. **Set Up a Domain Name (Optional):**
   - If you have a domain name, you can point it to your EC2 instance's public IP address using your domain registrar's DNS settings.
   - Update your Nginx server block configuration to use your domain name instead of the public IP.

10. **Secure Your Application:**
    - It's recommended to secure your Laravel application using HTTPS. You can use Let's Encrypt to obtain a free SSL certificate:
      ```sh
      sudo apt install certbot python3-certbot-nginx
      sudo certbot --nginx
      ```
    - Follow the prompts to complete the SSL certificate installation.

#### Troubleshooting
- **500 Internal Server Error:** Check the Nginx error logs (`/var/log/nginx/error.log`) for details.
- **Database Connection Errors:** Verify your `.env` file for correct database credentials and ensure MySQL is running.
- **Permission Issues:** Ensure that the `storage` and `bootstrap/cache` directories are writable by the web server.

By following these steps, you should be able to successfully deploy your Laravel project on AWS with Nginx.