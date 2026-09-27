# Security Policy

## Reporting Security Vulnerabilities

If you discover a security vulnerability in SecureShare, please report it responsibly:

1. **Do NOT** create a public GitHub issue for security vulnerabilities
2. Email security concerns to: security@jason-clark.org
3. Include as much detail as possible about the vulnerability
4. Allow reasonable time for the issue to be addressed before public disclosure

## Security Features

SecureShare implements multiple layers of security:

### Client-Side Encryption
- All files are encrypted using AES-256-GCM before upload
- Encryption keys are generated in the browser and never sent to the server
- Server has no access to unencrypted file content

### Access Control
- Rate limiting: 5 uploads per 15 minutes per IP address
- File type validation blocks potentially dangerous files
- File size limits prevent resource exhaustion

### Privacy Protection
- IP addresses are cryptographically hashed for abuse prevention
- No user tracking or analytics
- No persistent cookies or session storage

### Data Protection
- Automatic file expiration and deletion
- Secure random filename generation
- Database schema designed for minimal data retention

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |

## Security Best Practices for Deployment

1. Use HTTPS in production
2. Set strong database credentials
3. Configure proper firewall rules
4. Regular security updates
5. Monitor logs for suspicious activity
6. Use environment variables for sensitive configuration

## Threat Model

SecureShare protects against:
- Server-side data breaches (files are encrypted client-side)
- Unauthorized access to files (cryptographic security)
- Resource exhaustion attacks (rate limiting)
- Malicious file uploads (content validation)

SecureShare does NOT protect against:
- Client-side malware or keyloggers
- Social engineering attacks
- Physical access to user devices
- Compromised browser environments

## Acknowledgments

We appreciate security researchers who responsibly disclose vulnerabilities.