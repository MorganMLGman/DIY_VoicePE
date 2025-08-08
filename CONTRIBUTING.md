# Contributing to DIY VoicePE

Thank you for your interest in contributing to the DIY VoicePE project! This guide will help you get started.

## Getting Started

### Prerequisites

- ESPHome 2025.5.1 or later
- ESP32-S3 development board
- Basic knowledge of ESPHome and YAML configuration

### Development Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/MorganMLGman/DIY_VoicePE.git
   cd DIY_VoicePE
   ```

2. Install ESPHome if you haven't already:
   ```bash
   pip install esphome
   ```

3. Validate the configuration:
   ```bash
   esphome config diy-voicepe-esp32-s3.yaml
   ```

## How to Contribute

### Reporting Issues

- Use the GitHub issue tracker to report bugs or request features
- Provide clear steps to reproduce any issues
- Include relevant hardware and software versions

### Making Changes

1. Fork the repository
2. Create a new branch for your feature/fix:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. Make your changes
4. Test your changes thoroughly
5. Commit with clear, descriptive messages
6. Push to your fork and create a pull request

### Code Style

- Follow ESPHome YAML best practices
- Use meaningful component names and IDs
- Comment complex configurations
- Maintain consistent indentation (2 spaces)

### Testing

- Always test configuration changes on actual hardware when possible
- Validate YAML syntax with `esphome config`
- Ensure all features work as expected

## Project Structure

```
DIY_VoicePE/
├── diy-voicepe-esp32-s3.yaml     # Main ESPHome configuration
├── diy-voicepe-esp32-s3.factory.yaml  # Factory configuration
├── assets/                        # Images and documentation assets
├── sounds/                        # Audio files for voice responses
├── static/                        # Static website files
└── .github/                       # GitHub workflows and templates
```

## Pull Request Process

1. Ensure your code follows the project standards
2. Update documentation if you're changing functionality
3. Test your changes thoroughly
4. Write clear commit messages
5. Fill out the pull request template completely

## Community Guidelines

- Be respectful and inclusive
- Help others learn and contribute
- Focus on constructive feedback
- Share knowledge and best practices

## Questions?

If you have questions about contributing, feel free to:
- Open an issue for discussion
- Join community discussions
- Review existing issues and pull requests

Thank you for contributing to DIY VoicePE!