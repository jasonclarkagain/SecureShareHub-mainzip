# SecureShare - Encrypted File Sharing System

## Overview

SecureShare is a secure file sharing application built with a full-stack TypeScript architecture. It allows users to upload files with client-side encryption, share them via secure links, and download them with automatic decryption. The system emphasizes security, privacy, and user experience through modern web technologies.

## User Preferences

Preferred communication style: Simple, everyday language.

## Recent Changes

**July 2024**
- ✅ Fixed critical file upload issues with FormData handling
- ✅ Added comprehensive footer with functional links (FAQ, Privacy Policy, Terms of Service)
- ✅ Added Jason Clark attribution footer with link to jason-clark.org
- ✅ Extended file expiration options (3 months, 6 months, 1 year)
- ✅ Created modal system for footer content display
- ✅ Completed production-ready encrypted file sharing platform
- ✅ Implemented 5 interactive/personalized features:
  - File Preview: View file details and preview supported formats before upload
  - Upload Customization: Advanced options for passwords, compression, limits, and messages
  - Upload History: Local storage of past uploads with search and management
  - Smart Recommendations: AI-powered suggestions based on file types and patterns
  - Interactive Share Links: Multiple sharing methods including QR codes and social media

## System Architecture

### Frontend Architecture
- **Framework**: React with TypeScript
- **Routing**: Wouter for client-side routing
- **State Management**: TanStack Query for server state management
- **UI Components**: Radix UI with shadcn/ui component library
- **Styling**: Tailwind CSS with custom design system
- **Build Tool**: Vite for fast development and production builds

### Backend Architecture
- **Framework**: Express.js with TypeScript
- **Database**: PostgreSQL with Drizzle ORM
- **Database Provider**: Neon Database (@neondatabase/serverless)
- **File Storage**: Local file system with encrypted storage
- **Session Management**: Express sessions with PostgreSQL store
- **API Design**: RESTful API with JSON responses

### Security Architecture
- **Client-Side Encryption**: Web Crypto API with AES-GCM 256-bit encryption
- **File Obfuscation**: Random filename generation using crypto.randomBytes
- **Rate Limiting**: IP-based rate limiting for uploads and downloads
- **Content Validation**: File type and size validation
- **Data Protection**: IP address hashing for privacy

## Key Components

### Database Schema
The application uses three main tables:
- **files**: Stores encrypted file metadata including share tokens, encryption keys, and expiry dates
- **reports**: Handles user-reported content with moderation workflow
- **uploadLogs**: Tracks upload activity and implements IP-based blocking

### File Processing Pipeline
1. **Client-Side Encryption**: Files are encrypted in the browser before upload
2. **Secure Upload**: Encrypted files are uploaded with metadata
3. **Storage**: Files stored with obfuscated names and database references
4. **Link Generation**: Secure share links with embedded encryption keys
5. **Decryption**: Files are decrypted client-side during download

### Security Middleware
- **Rate Limiting**: Prevents abuse with configurable limits per IP
- **File Validation**: Blocks dangerous file types and enforces size limits
- **Content Filtering**: Prevents upload of executable and script files

### User Interface Components
- **Upload Zone**: Drag-and-drop file upload with validation
- **Progress Tracking**: Real-time upload and encryption progress
- **File Management**: Preview and removal of selected files with detailed file preview modal
- **Download Interface**: Secure file download with decryption
- **Reporting System**: User-friendly content reporting mechanism
- **Interactive Features**: 
  - File Preview modal with detailed metadata and preview capabilities
  - Upload Customization panel with advanced security and sharing options
  - Upload History tracker with local storage and search functionality
  - Smart Recommendations engine with personalized suggestions
  - Interactive Share Links with QR codes, social media integration, and multiple sharing methods

## Data Flow

### Upload Process
1. User selects files through drag-and-drop or file picker
2. Files are validated for type and size restrictions
3. Encryption key is generated using Web Crypto API
4. Files are encrypted client-side with AES-GCM
5. Encrypted files are uploaded to server with metadata
6. Server stores files with obfuscated names and creates database records
7. Share link is generated with embedded encryption key

### Download Process
1. User accesses share link with embedded encryption key
2. Client extracts share token and encryption key from URL
3. File metadata is fetched from server
4. Encrypted file is downloaded from server
5. File is decrypted client-side using stored encryption key
6. Decrypted file is provided to user for download

### Security Flow
- All file encryption/decryption occurs client-side
- Server never has access to unencrypted files or encryption keys
- IP addresses are hashed for privacy protection
- Rate limiting prevents abuse and resource exhaustion

## External Dependencies

### Core Dependencies
- **Database**: Neon PostgreSQL with connection pooling
- **UI Framework**: Radix UI primitives with shadcn/ui styling
- **Encryption**: Web Crypto API (browser native)
- **File Handling**: Multer for multipart form processing
- **Query Management**: TanStack Query for API state management

### Development Dependencies
- **TypeScript**: Full type safety across frontend and backend
- **Vite**: Fast development server and build tool
- **Tailwind CSS**: Utility-first styling framework
- **Drizzle**: Type-safe database ORM and query builder

## Deployment Strategy

### Development Environment
- **Hot Reloading**: Vite development server with HMR
- **Database**: Neon development database
- **File Storage**: Local uploads directory
- **Process Management**: tsx for TypeScript execution

### Production Build
- **Frontend**: Vite builds optimized React bundle
- **Backend**: esbuild compiles TypeScript to ESM
- **Database**: Drizzle migrations for schema management
- **File Cleanup**: Automated cleanup service for expired files

### Environment Configuration
- **DATABASE_URL**: PostgreSQL connection string
- **File Limits**: 100MB maximum file size
- **Expiry**: Configurable file expiration (default 7 days)
- **Rate Limits**: 10 requests per 15 minutes per IP

### Monitoring and Maintenance
- **File Cleanup**: Automated removal of expired files
- **Upload Tracking**: IP-based upload monitoring and blocking
- **Error Handling**: Comprehensive error logging and user feedback
- **Performance**: Optimized queries and efficient file handling