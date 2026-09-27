# SecureShare - Encrypted File Sharing Platform

A production-ready encrypted file sharing platform similar to AnonFiles with client-side AES-256 encryption, PostgreSQL database, and comprehensive security features.

## 🔒 Features

- **Client-Side Encryption**: Files are encrypted with AES-256 in your browser before upload
- **Anonymous Sharing**: No registration required, share files instantly
- **Flexible Expiration**: Choose from 24 hours to 1 year retention periods
- **Security First**: Rate limiting, file type validation, and abuse prevention
- **Privacy Protected**: IP address hashing and no user tracking
- **Production Ready**: PostgreSQL database with automated cleanup

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ 
- PostgreSQL database
- 2GB+ RAM recommended

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/secureshare.git
cd secureshare
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```bash
# Create .env file
DATABASE_URL=postgresql://username:password@localhost:5432/secureshare
```

4. Initialize the database:
```bash
npm run db:push
```

5. Start the development server:
```bash
npm run dev
```

The application will be available at `http://localhost:5000`

## 🏗️ Architecture

### Tech Stack
- **Frontend**: React + TypeScript + Tailwind CSS + Vite
- **Backend**: Express.js + TypeScript
- **Database**: PostgreSQL with Drizzle ORM
- **Encryption**: Web Crypto API (AES-256-GCM)
- **UI Components**: Radix UI + shadcn/ui

### Security Features
- Client-side encryption prevents server access to files
- Rate limiting (5 uploads per 15 minutes per IP)
- File type validation blocks executables and scripts
- IP address hashing for privacy
- Automatic file cleanup for expired content

## 📁 Project Structure

```
├── client/                 # React frontend
│   ├── src/
│   │   ├── components/     # UI components
│   │   ├── pages/         # Application pages
│   │   ├── lib/           # Utilities and crypto
│   │   └── hooks/         # React hooks
├── server/                # Express backend
│   ├── middleware/        # Security middleware
│   ├── services/         # Background services
│   └── routes.ts         # API endpoints
├── shared/               # Shared types and schemas
│   └── schema.ts        # Database schema
└── uploads/             # File storage directory
```

## 🔧 Configuration

### Environment Variables

- `DATABASE_URL`: PostgreSQL connection string
- `NODE_ENV`: Environment (development/production)
- `PORT`: Server port (default: 5000)

### File Limits

- Maximum file size: 100MB
- Supported formats: Documents, images, archives, media
- Blocked formats: Executables, scripts for security

## 🚀 Deployment

### Using Replit (Recommended)

1. Fork this repository on Replit
2. Set the `DATABASE_URL` environment variable
3. Run `npm run db:push` to initialize the database
4. Click "Deploy" to launch your instance

### Manual Deployment

1. Build the application:
```bash
npm run build
```

2. Set up PostgreSQL database
3. Configure environment variables
4. Start the production server:
```bash
npm start
```

## 🛡️ Security Considerations

- Files are encrypted client-side before reaching the server
- Encryption keys are never stored on the server
- IP addresses are hashed for privacy protection
- Rate limiting prevents abuse
- Automatic cleanup removes expired files
- File type validation blocks dangerous uploads

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

Made with ❤️ by [Jason Clark](https://jason-clark.org)

## 🔒 Privacy & Security

SecureShare is designed with privacy as a core principle:
- No user tracking or analytics
- Client-side encryption ensures server never sees your files
- Automatic file deletion after expiration
- IP address hashing for abuse prevention only
- No cookies or persistent tracking

For questions about security or privacy, please open an issue.