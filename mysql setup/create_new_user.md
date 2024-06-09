# How to Create a New User in MySQL

To create a new user in MySQL, you'll need to follow these steps:

1. **Access MySQL**: First, you need to access the MySQL command line interface. You can do this by running:
   ```bash
   mysql -u root -p
   ```
   You'll be prompted to enter your root password.

2. **Create a New User**: Once you're logged into MySQL, you can create a new user with the `CREATE USER` command. For example, to create a user named `newuser` with a password `password`, you would run:
   ```sql
   CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
   ```
   Replace `'newuser'` with the desired username and `'password'` with the desired password.

3. **Grant Privileges**: By default, the new user will not have any privileges. You can grant specific privileges to the user using the `GRANT` command. For example, to grant all privileges on all databases to the `newuser`, you would run:
   ```sql
   GRANT ALL PRIVILEGES ON *.* TO 'newuser'@'localhost';
   ```
   If you want to grant specific privileges or limit access to certain databases, you can modify the command accordingly.

4. **Flush Privileges**: After granting privileges, you need to flush the privileges to ensure that the changes take effect. Run:
   ```sql
   FLUSH PRIVILEGES;
   ```

5. **Exit MySQL**: Once you've created the new user and granted privileges, you can exit the MySQL prompt by typing:
   ```sql
   exit;
   ```

That's it! You've successfully created a new user in MySQL. The new user can now log in with the provided username and password and access the specified databases with the granted privileges.
