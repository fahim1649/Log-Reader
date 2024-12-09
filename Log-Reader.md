# Log-Reader

```javascript
sudo apt-get install apache2-utils -y
```

```javascript
sudo htpasswd -c /etc/nginx/.htpasswd logreader
```

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

```javascript
sudo nginx -t
```

```javascript
sudo systemctl reload nginx
```
