# Configuring SSL for PowerDNS API

This page provides a step-by-step guide to configuring SSL for the PowerDNS API using Nginx as a reverse proxy.

## Prerequisites

Before proceeding, ensure that:
- You have a domain name pointing to your server.
- Nginx is installed on your server.
- You have obtained an SSL certificate (e.g., using Let's Encrypt).

## Steps

### 1. Install Certbot and Obtain SSL Certificate

Install Certbot on your system if not already present:
```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx
```

Obtain an SSL certificate for your domain:
```bash
sudo certbot --nginx -d yourdomain.com
```
Follow the prompts to complete the certificate generation.

### 2. Configure Nginx as a Reverse Proxy

Edit your Nginx configuration file or create a new one for the PowerDNS API (e.g., `/etc/nginx/sites-available/powerdns`):
```nginx
server {
    listen 443 ssl;
    server_name yourdomain.com;

    ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;

    location / {
        proxy_pass http://localhost:8081;  # Replace with your PowerDNS API endpoint
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Activate the configuration by creating a symlink:
```bash
sudo ln -s /etc/nginx/sites-available/powerdns /etc/nginx/sites-enabled/
```

Test the configuration for syntax errors:
```bash
sudo nginx -t
```

Reload Nginx:
```bash
sudo systemctl reload nginx
```

### 3. Verify the Configuration

Access `https://yourdomain.com` in a web browser to ensure the SSL is working correctly. You can also test using curl:
```bash
curl -k https://yourdomain.com
```

### 4. Automate SSL Certificate Renewal

Ensure the Certbot renewal timer is active:
```bash
sudo systemctl status certbot.timer
```

Test the renewal process:
```bash
sudo certbot renew --dry-run
```

---

By following these steps, you have successfully configured SSL for the PowerDNS API using Nginx as a reverse proxy.