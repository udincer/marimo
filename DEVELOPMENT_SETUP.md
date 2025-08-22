# Development Environment Setup Guide

This guide will help you set up a development environment for the marimo project.

## Prerequisites

Before setting up the development environment, ensure you have the following tools installed:

- **Python 3.9+** (we recommend Python 3.12)
- **Node.js v22+** (required for frontend development)
- **pnpm v9+** (for frontend package management)
- **uv** (for Python package management)
- **hatch** (for Python environment management)

## Quick Setup

### 1. Check Prerequisites

First, verify all required tools are installed:

```bash
make check-prereqs
```

### 2. Install Missing Prerequisites

If any prerequisites are missing, install them:

#### Install uv and hatch
```bash
pip install uv hatch
```

#### Install pnpm
```bash
npm install -g pnpm@9
```

#### Update Node.js (if needed)
If you're using an older version of Node.js, update to v22+:
```bash
# On Ubuntu/Debian
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### 3. Set Up Virtual Environment

Create a Python virtual environment and install dependencies:

```bash
uv venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
make py
```

### 4. Install Frontend Dependencies

Install frontend dependencies and build assets:

```bash
pnpm install --no-frozen-lockfile
make fe
```

### 5. Test the Setup

Verify your development environment is working:

```bash
# Check marimo version
marimo --version

# Test development server (runs in background)
marimo edit --headless --no-token /tmp &
# Should be accessible at http://localhost:2718
```

## Development Workflow

### Start Development Environment

To start the complete development environment with hot-reloading:

```bash
make dev
```

This command:
- Starts the marimo backend server in headless mode
- Starts the frontend development server with hot-reloading
- Automatically opens your browser to the development interface

### Build and Test

```bash
# Build frontend assets
make fe

# Run tests
make test

# Run linting and type checking
make check
```

### Common Commands

| Command | Description |
|---------|-------------|
| `make help` | Show all available commands |
| `make py` | Install Python dependencies |
| `make fe` | Build frontend assets |
| `make dev` | Start development servers |
| `make test` | Run all tests |
| `make check` | Run linting and type checking |

## Troubleshooting

### Frontend Build Issues

If you encounter issues with frontend compilation related to TypeScript transformation:

1. Ensure you have Node.js v22+ installed
2. Check that tsx is available: `npm install -g tsx`
3. Clean and rebuild: `rm -rf node_modules && pnpm install --no-frozen-lockfile && make fe`

### Python Environment Issues

If you have Python dependency conflicts:

1. Remove the virtual environment: `rm -rf .venv`
2. Recreate it: `uv venv && source .venv/bin/activate`
3. Reinstall dependencies: `make py`

### Node.js Version Issues

If commands fail with "bad option" errors:

1. Check Node.js version: `node --version`
2. Ensure you're using the system Node.js v22+: `export PATH="/usr/bin:$PATH"`
3. If using nvm, switch to latest: `nvm use node`

## Alternative Setup Methods

### Using Pixi (Recommended)

If you prefer using pixi for dependency management:

```bash
# Install pixi first
curl -fsSL https://pixi.sh/install.sh | bash

# Launch development environment
pixi run hatch shell
make fe && make py
make dev
```

### Using Docker/Dagger

For containerized development:

```bash
# Install dagger CLI
curl -L https://dl.dagger.io/dagger/install.sh | sh

# Run development environment in container
dagger call make dev
```

## Contributing

Once your environment is set up, see [CONTRIBUTING.md](CONTRIBUTING.md) for detailed contribution guidelines.

## Support

If you encounter issues setting up your development environment:

1. Check the [FAQ](https://docs.marimo.io/faq.html)
2. Join our [Discord community](https://marimo.io/discord)
3. Open an issue on [GitHub](https://github.com/marimo-team/marimo/issues)