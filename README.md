# Kairos Cloud Configuration

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

> Centralized configuration management for Kairos microservices ecosystem

## Overview

Kairos Cloud Config is a centralized configuration service for managing application settings across all Kairos microservices. It provides a single source of truth for configuration properties, making it easier to manage and deploy applications in different environments.

## Features

- **Centralized Configuration**: Manage all service configurations from a single repository
- **Environment-Specific Settings**: Support for multiple environments (dev, staging, production)
- **Version Control**: Track configuration changes with Git
- **Service Discovery**: Integrated with Kairos service registry
- **Security**: Encrypted sensitive information

## Prerequisites

- Docker 20.10.0 or higher
- Docker Compose 2.0.0 or higher
- Git

## Getting Started

### Clone the Repository

```bash
git clone https://github.com/ETS-KAIROS/kairos-cloud-config.git
cd kairos-cloud-config
```

### Environment Setup

1. Copy the example environment file:
   ```bash
   cp .env.example .env
   ```

2. Update the environment variables in `.env` as needed.

### Running with Docker

```bash
docker-compose up -d
```

This will start the configuration server and all dependent services.

## Project Structure

```
kairos-cloud-config/
├── service-user/         # User service configuration
├── service-document/     # Document service configuration
├── service-workflow/     # Workflow service configuration
├── docker-compose.yml    # Main Docker Compose configuration
└── README.md            # This file
```

## Configuration Management

### Adding a New Service

1. Create a new directory for your service under the root directory
2. Add environment-specific configuration files:
   - `application.yml` - Common configuration
   - `application-{env}.yml` - Environment-specific overrides

### Updating Configuration

1. Modify the appropriate YAML files
2. Commit and push changes to the repository
3. The configuration server will automatically detect changes and refresh the configuration

## Security

Sensitive information should be encrypted using the Spring Cloud Config encryption features:

```bash
# Encrypt a value
curl {config-server}/encrypt -d 'your-sensitive-value'

# Decrypt a value
curl {config-server}/decrypt -d 'encrypted-value'
```

## API Endpoints

- `GET /{application}/{profile}[/{label}]` - Get configuration for a specific application and profile
- `GET /{application}-{profile}.yml` - Get configuration in YAML format
- `GET /{application}-{profile}.properties` - Get configuration in properties format
- `POST /monitor` - Refresh configuration (requires webhook setup)

## Monitoring

The configuration server exposes actuator endpoints for monitoring:

- `/actuator/health` - Service health check
- `/actuator/info` - Build information
- `/actuator/refresh` - Manually trigger configuration refresh

## Troubleshooting

### Common Issues

- **Configuration not updating**: Ensure the service has the correct `spring.cloud.config.uri` and `spring.application.name`
- **Connection refused**: Verify the config server is running and accessible
- **Decryption errors**: Check that the encryption key is correctly set in the environment

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

Distributed under the MIT License. See `LICENSE` for more information.

## Contact

Kairos Team - [@kairos](https://github.com/kairos)

Project Link: [https://github.com/ETS-KAIROS/kairos-cloud-config](https://github.com/ETS-KAIROS/kairos-cloud-config)

## Acknowledgments

- [Spring Cloud Config](https://spring.io/projects/spring-cloud-config)
- [Docker](https://www.docker.com/)
- [Kairos Platform](https://github.com/kairos)