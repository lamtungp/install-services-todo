### Install OpenSSL
```
sudo apt update
sudo apt install openssl
```

### Generate ssl
```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout selfsigned.key -out selfsigned.crt
```

### Config nginx (/etc/nginx/sites-available/default)
```
server {
    listen 443 ssl;
    server_name ec2-******.us-east-2.compute.amazonaws.com;

    ssl_certificate /home/ubuntu/selfsigned.crt;
    ssl_certificate_key /home/ubuntu/selfsigned.key;

    location / {
        proxy_pass http://localhost:4000; # whatever port your app runs on
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```