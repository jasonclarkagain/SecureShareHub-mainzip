# Deployment Guide

This guide covers various deployment options for SecureShare.

## Prerequisites

- Node.js 18+
- PostgreSQL database
- 2GB+ RAM recommended
- SSL certificate for production (recommended)

## Environment Variables

Copy `.env.example` to `.env` and configure:

```bash
# Required
DATABASE_URL=postgresql://username:password@host:port/database

# Optional
NODE_ENV=production
PORT=5000
```

## Quick Deploy Options

### 1. Replit (Recommended for Testing)

1. Fork this repository on Replit
2. Set the `DATABASE_URL` environment variable
3. Run `npm run db:push`
4. Click "Deploy"

### 2. Railway

1. Connect your GitHub repository
2. Set environment variables
3. Deploy automatically

### 3. Render

1. Connect your repository
2. Set build command: `npm run build`
3. Set start command: `npm start`
4. Configure environment variables

### 4. Heroku

```bash
# Create app
heroku create your-secureshare-app

# Add PostgreSQL
heroku addons:create heroku-postgresql:mini

# Deploy
git push heroku main

# Initialize database
heroku run npm run db:push
```

## Self-Hosted Deployment

### Option A: Docker (Recommended)

1. Clone the repository:
```bash
git clone https://github.com/yourusername/secureshare.git
cd secureshare
```

2. Build and run with Docker Compose:
```bash
docker-compose up -d
```

3. Initialize the database:
```bash
docker-compose exec app npm run db:push
```

### Option B: Manual Setup

1. Install dependencies:
```bash
npm install
```

2. Build the application:
```bash
npm run build
```

3. Set up PostgreSQL database and configure `.env`

4. Initialize database:
```bash
npm run db:push
```

5. Start the application:
```bash
npm start
```

### Option C: PM2 (Process Manager)

1. Install PM2:
```bash
npm install -g pm2
```

2. Create ecosystem file `ecosystem.config.js`:
```javascript
module.exports = {
  apps: [{
    name: 'secureshare',
    script: 'dist/index.js',
    instances: 'max',
    exec_mode: 'cluster',
    env: {
      NODE_ENV: 'production',
      PORT: 5000
    }
  }]
}
```

3. Start with PM2:
```bash
pm2 start ecosystem.config.js
pm2 save
pm2 startup
```

## Nginx Configuration

Create `/etc/nginx/sites-available/secureshare`:

```nginx
server {
    listen 80;
    server_name your-domain.com;

    # Redirect to HTTPS
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name your-domain.com;

    # SSL configuration
    ssl_certificate /path/to/your/cert.pem;
    ssl_certificate_key /path/to/your/key.pem;

    # Security headers
    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;
    add_header X-XSS-Protection "1; mode=block";
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains";

    # File upload size limit
    client_max_body_size 100M;

    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_cache_bypass $http_upgrade;
    }
}
```

## Database Setup

### PostgreSQL Configuration

1. Create database:
```sql
CREATE DATABASE secureshare;
CREATE USER secureshare_user WITH PASSWORD 'your-password';
GRANT ALL PRIVILEGES ON DATABASE secureshare TO secureshare_user;
```

2. Update connection string:
```bash
DATABASE_URL=postgresql://secureshare_user:your-password@localhost:5432/secureshare
```

### Database Migrations

Initialize or update schema:
```bash
npm run db:push
```

## Security Considerations

### Production Checklist

- [ ] Use HTTPS in production
- [ ] Set strong database passwords
- [ ] Configure firewall rules
- [ ] Set up regular backups
- [ ] Monitor application logs
- [ ] Keep dependencies updated
- [ ] Configure rate limiting at proxy level
- [ ] Set up file cleanup monitoring

### Environment Security

```bash
# Secure file permissions
chmod 600 .env

# Use environment variables in production
export DATABASE_URL="your-connection-string"
```

## Monitoring

### Health Check

The application provides a health endpoint:
```bash
curl http://your-domain.com/api/health
```

### Log Monitoring

Monitor application logs for:
- Rate limit violations
- File upload errors
- Database connection issues
- Security events

### File Cleanup

The application automatically cleans up expired files. Monitor the cleanup process:
- Check logs for cleanup activity
- Monitor disk space usage
- Verify expired files are removed

## Scaling

### Horizontal Scaling

For high traffic:
1. Use a load balancer
2. Run multiple application instances
3. Share uploads directory (NFS/S3)
4. Use Redis for session storage

### Database Scaling

For large datasets:
1. Use connection pooling
2. Set up read replicas
3. Monitor query performance
4. Consider partitioning large tables

## Backup Strategy

### Database Backups

```bash
# Daily backup
pg_dump $DATABASE_URL > backup-$(date +%Y%m%d).sql

# Restore backup
psql $DATABASE_URL < backup-20241214.sql
```

### File Backups

```bash
# Backup uploads directory
tar -czf uploads-backup-$(date +%Y%m%d).tar.gz uploads/
```

## Troubleshooting

### Common Issues

1. **Database connection errors**
   - Check DATABASE_URL format
   - Verify database is running
   - Check network connectivity

2. **File upload failures**
   - Check disk space
   - Verify uploads directory permissions
   - Check file size limits

3. **Rate limiting issues**
   - Check IP configuration
   - Verify rate limit settings
   - Monitor for abuse

### Debug Mode

Enable debug logging:
```bash
NODE_ENV=development npm start
```

## Support

For deployment issues:
1. Check application logs
2. Verify environment configuration
3. Test database connectivity
4. Monitor system resources