# Contributing to SecureShare

Thank you for your interest in contributing to SecureShare! This document provides guidelines for contributing to the project.

## Code of Conduct

Please be respectful and professional in all interactions. This project aims to provide a secure and privacy-focused file sharing solution.

## How to Contribute

### Reporting Issues

- Use the GitHub issue tracker
- Provide clear, detailed descriptions
- Include steps to reproduce bugs
- For security issues, see SECURITY.md

### Submitting Changes

1. Fork the repository
2. Create a feature branch from `main`
3. Make your changes
4. Test thoroughly
5. Submit a pull request

### Development Setup

1. Clone your fork:
```bash
git clone https://github.com/yourusername/secureshare.git
cd secureshare
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment:
```bash
cp .env.example .env
# Edit .env with your database URL
```

4. Initialize database:
```bash
npm run db:push
```

5. Start development server:
```bash
npm run dev
```

## Coding Standards

### TypeScript
- Use strict TypeScript configuration
- Provide proper type annotations
- Avoid `any` types

### Code Style
- Use Prettier for formatting
- Follow existing patterns
- Write self-documenting code
- Add comments for complex logic

### Security
- Never compromise on security features
- Validate all user inputs
- Follow security best practices
- Test security-related changes thoroughly

## Testing

- Test all functionality manually
- Verify security features work correctly
- Test error handling
- Check rate limiting and validation

## Database Changes

- Use Drizzle migrations for schema changes
- Test migrations thoroughly
- Update schema documentation

## Frontend Changes

- Follow React best practices
- Use TypeScript properly
- Test responsive design
- Verify accessibility

## Pull Request Guidelines

### Before Submitting
- Test your changes thoroughly
- Update documentation if needed
- Follow the coding standards
- Keep changes focused and atomic

### PR Description
- Clear title describing the change
- Detailed description of what was changed
- List any breaking changes
- Reference related issues

### Review Process
- All PRs require review
- Address feedback promptly
- Be open to suggestions
- Maintain professional communication

## Feature Requests

When proposing new features:
- Open an issue first to discuss
- Consider security implications
- Think about privacy impact
- Provide detailed use cases

## Documentation

- Update README.md for significant changes
- Document new configuration options
- Update API documentation
- Keep security documentation current

## Release Process

Releases are managed by project maintainers:
1. Version bump in package.json
2. Update CHANGELOG.md
3. Create release tag
4. Deploy to production

## Questions?

- Open a GitHub issue for questions
- Check existing documentation first
- Be specific about your question

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

Thank you for contributing to SecureShare!