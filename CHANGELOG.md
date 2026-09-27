# Changelog

All notable changes to SecureShare will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2024-07-14

### Added
- Client-side AES-256-GCM encryption for all file uploads
- Anonymous file sharing without user registration
- Flexible expiration periods (24 hours, 7 days, 30 days, 3 months, 6 months, 1 year)
- Rate limiting (5 uploads per 15 minutes per IP)
- File type validation and security filtering
- PostgreSQL database with Drizzle ORM
- Automated file cleanup for expired content
- IP address hashing for privacy protection
- Comprehensive abuse reporting system
- Responsive React frontend with Tailwind CSS
- RESTful API with Express.js backend
- Docker support for easy deployment
- Comprehensive documentation and security guidelines

### Security
- All files encrypted client-side before upload
- Server never has access to encryption keys or unencrypted content
- Blocked executable file types (.exe, .js, .sh, etc.)
- Rate limiting to prevent abuse
- IP address hashing for privacy
- Automatic file expiration and cleanup

### Features
- Drag-and-drop file upload interface
- Real-time upload progress tracking
- Shareable download links with embedded encryption keys
- Download count tracking
- Functional footer with FAQ, Privacy Policy, and Terms of Service
- Mobile-responsive design
- Dark/light theme support

### Technical
- TypeScript throughout frontend and backend
- PostgreSQL database with connection pooling
- Vite for fast development and optimized builds
- Radix UI components with shadcn/ui styling
- Express.js API with comprehensive middleware
- Automated testing and validation
- Production-ready deployment configuration