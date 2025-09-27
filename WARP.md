# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

This is a Django 5.2.6 project with Tailwind CSS integration using django-tailwind and DaisyUI. The project uses UV for dependency management and Python 3.13.

### Architecture

- **Django Project**: `myproject/` - Main Django project configuration
- **Theme App**: `theme/` - Tailwind CSS integration app with templates and styling
- **Database**: SQLite3 (default Django setup)
- **Frontend**: Tailwind CSS v4.1.11 + DaisyUI v5.0.43
- **Package Management**: UV with pyproject.toml

## Development Setup

### Initial Setup
```bash
# Install dependencies using UV
uv sync

# Activate virtual environment (if needed)
uv venv --python 3.13
# On Windows
.venv\Scripts\activate
# On Unix/macOS
source .venv/bin/activate

# Install Node.js dependencies for Tailwind
cd theme/static_src
npm install
```

### Database Setup
```bash
# Create and apply migrations
python manage.py makemigrations
python manage.py migrate

# Create superuser
python manage.py createsuperuser
```

## Common Development Commands

### Django Commands
```bash
# Run development server
python manage.py runserver

# Run tests
python manage.py test

# Create new Django app
python manage.py startapp <app_name>

# Django shell
python manage.py shell

# Check for issues
python manage.py check

# Show installed apps and versions
python manage.py showmigrations
```

### Tailwind CSS Commands
```bash
# Navigate to theme directory
cd theme/static_src

# Start Tailwind development server (watches for changes)
npm run dev
# or
npm start

# Build for production
npm run build

# Clean and rebuild CSS
npm run build:clean && npm run build:tailwind
```

### Testing
```bash
# Run all tests
python manage.py test

# Run tests for specific app
python manage.py test <app_name>

# Run tests with verbose output
python manage.py test --verbose

# Run specific test
python manage.py test <app_name>.tests.<TestClass>.<test_method>
```

## Key Configuration

### Tailwind Integration
- **App Name**: `theme` (configured in `TAILWIND_APP_NAME`)
- **NPM Path**: Windows-specific path set in settings (`NPM_BIN_PATH`)
- **CSS Source**: `theme/static_src/src/styles.css`
- **Output**: `theme/static/css/dist/styles.css`
- **Template**: `theme/templates/base.html` - Base template with Tailwind integration

### Dependencies
- **Django**: 5.2.6+ 
- **django-tailwind**: 4.2.0+ for Tailwind CSS integration
- **django-extensions**: 4.1+ for additional Django commands
- **cookiecutter**: 2.6.0+ for project templating

### File Watching
The Tailwind configuration (`@source`) watches these patterns for CSS class changes:
- All HTML files: `**/*.html`
- All Python files: `**/*.py` 
- All JavaScript files: `**/*.js`

## Development Workflow

1. **Start Django server**: `python manage.py runserver`
2. **Start Tailwind watcher** (in new terminal): `cd theme/static_src && npm run dev`
3. **Make changes** to templates in `theme/templates/` or other apps
4. **CSS automatically rebuilds** when Tailwind classes are detected

## Production Considerations

- Change `DEBUG = False` in settings
- Set proper `ALLOWED_HOSTS`
- Use `npm run build` for optimized CSS
- The project uses an insecure secret key - generate a new one for production