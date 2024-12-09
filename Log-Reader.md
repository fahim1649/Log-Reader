# Log-Reader

This command installs the apache2-utils package, which includes the htpasswd tool used for creating and managing password files.
```javascript
sudo apt-get install apache2-utils -y
```
This command creates a new password file at /etc/nginx/.htpasswd with a user named logreader-user1. You'll be prompted to enter and confirm a password for this user.
```javascript
sudo htpasswd -c /etc/nginx/.htpasswd logreader-user1
```
> Add Another User to the Existing Password File
> This command adds a new user named another-user2 to the existing password file /etc/nginx/.htpasswd. You'll be prompted to enter and confirm a password for this new user.
Note that the -c option is not used here, as it's only required when creating a new password file. Since the file already exists, we can simply add a new user to it using the above command.
```javascript
sudo htpasswd /etc/nginx/.htpasswd another-user2
```
>


This command opens the default Nginx configuration file in the vi editor. You'll need to add the following configuration block to enable authentication:
```javascript
sudo vi /etc/nginx/sites-available/default
```

```javascript
 server {
        listen 7794 default_server;
        listen [::]:7794 default_server;

        server_name 165.232.184.235:7794;
        root /root/EnvironmentFiles/WASEEL_AUTOMATION_LOGS;
        autoindex on;
        autoindex_format json;

        location /{
          auth_basic "Restricted Authentication";
          auth_basic_user_file "/etc/nginx/.htpasswd";
       }
}
```
This command tests the Nginx configuration for any syntax errors.
```javascript
sudo nginx -t
```
This command reloads the Nginx service to apply the changes made to the configuration file.
```javascript
sudo systemctl reload nginx
```
