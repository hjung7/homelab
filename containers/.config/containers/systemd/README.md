## nginx.conf for n8n
With default config for nginx, n8n doesn't update executions.
Use the settings below to make it work.
```
server {
        listen              443 ssl http2;
        server_name         <subdomain.example.com>;
        ssl_certificate     /etc/pki/tls/certs/<certs.pem>;
        ssl_certificate_key /etc/pki/tls/private/<key.pem>;
        location / {
                proxy_pass http://127.0.0.1:5678;
                proxy_http_version 1.1;
                proxy_set_header Cookie $http_cookie;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Upgrade $http_upgrade;
                proxy_connect_timeout 300s;
                proxy_read_timeout 300s;
                proxy_send_timeout 300s;
        }
}
```
