# 🐰 Contributing to RabbitMQ Stack

Thank you for your interest in contributing to the RabbitMQ Stack project! We welcome contributions that improve this local RabbitMQ messaging environment with SSL/TLS support and its documentation and developer experience.

## 📋 Table of Contents

- [Getting Started](#-getting-started)
- [Development Setup](#-development-setup)
- [Contributing Process](#-contributing-process)
- [Code Standards](#-code-standards)
- [Testing](#-testing)
- [Getting Help](#-getting-help)

## 🚀 Getting Started

### 🧰 Prerequisites

Before you begin, ensure you have the following installed:
- Docker and Docker Compose
- Git

### 🗂️ Project Structure

```text
├── docker-compose.yml        # RabbitMQ with management UI and SSL/TLS
├── rabbitmq.conf             # RabbitMQ SSL/TLS configuration
├── assets/                   # Architecture diagrams
└── .github/                  # GitHub workflows and templates
```

## 💻 Development Setup

1. **Fork and Clone the Repository**
   ```bash
   git clone https://github.com/mtnvencenzo/rabbitmq-stack.git
   cd rabbitmq-stack
   ```

2. **Start the RabbitMQ Stack**
   ```bash
   # Start RabbitMQ service
   docker compose up -d
   
   # Verify service is running
   docker compose ps
   ```

3. **Test the Setup**
   ```bash
   # RabbitMQ Management UI
   curl -sSf http://localhost:15672 >/dev/null && echo "RabbitMQ Management UI OK"

   # Test SSL connection (requires pika installed)
   python -c "import pika, ssl; context = ssl.create_default_context(); context.check_hostname = False; context.verify_mode = ssl.CERT_NONE; connection = pika.BlockingConnection(pika.ConnectionParameters('localhost', 5671, credentials=pika.PlainCredentials('admin', 'password'), ssl_options=pika.SSLOptions(context))); print('RabbitMQ SSL OK'); connection.close()"
   ```

## 🔄 Contributing Process

### 1. 📝 Before You Start

- **Check for existing issues** to avoid duplicate work
- **Create or comment on an issue** to discuss your proposed changes
- **Wait for approval** from maintainers before starting work (required for this repository)

### 2. 🛠️ Making Changes

1. **Create a feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/your-bug-fix
   ```

2. **Make your changes** following our [code standards](#-code-standards)

3. **Test your changes**
   - Validate `docker-compose.yml` starts cleanly
   - Confirm services become healthy and UIs are reachable
   - If you add new services, include healthchecks and docs

4. **Commit your changes**
   ```bash
   git add .
   git commit -m "feat(api): add new endpoint for ..."
   ```
   
   Use [conventional commit format](https://www.conventionalcommits.org/):
   - `feat:` for new features
   - `fix:` for bug fixes
   - `docs:` for documentation changes
   - `style:` for formatting changes
   - `refactor:` for code refactoring
   - `test:` for adding tests
   - `chore:` for maintenance tasks

### 3. 📬 Submitting Changes

1. **Push your branch**
   ```bash
   git push origin feature/your-feature-name
   ```

2. **Create a Pull Request**
   - Use our [PR template](pull_request_template.md)
   - Fill out all sections completely
   - Link related issues using `Closes #123` or `Fixes #456`
   - Request review from maintainers

## 📏 Code Standards

### 🐳 Docker & Docker Compose

- Use official RabbitMQ images with management plugin
- Follow Docker best practices for service configuration
- Use meaningful container and service names
- Include proper health checks for container reliability
- Document SSL/TLS configurations and certificate requirements

### 📝 Documentation

- Update documentation when making changes
- Use clear, concise language
- Include code examples for setup instructions
- Update service endpoint information when ports change

### 🔍 Validation Steps

Before submitting changes:

```bash
# Verify services start correctly
docker compose up -d

# Check service health
docker compose ps

curl -sSf http://localhost:15672 >/dev/null   # RabbitMQ Management UI

# Clean up
docker compose down -v
```

### 📏 Test Requirements

- **Service Startup**: All services must start without errors
- **Port Accessibility**: All documented ports must be accessible
- **Data Persistence**: Volume mounts must work correctly
- **Documentation**: Any changes must be documented


## 📜 License

By contributing to this project, you agree that your contributions will be licensed under the same license as the project (see [LICENSE](../LICENSE)).

---

Happy Contributing!  

For any questions about this contributing guide, please open an issue or contact the maintainers.
