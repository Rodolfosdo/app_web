# RF Cosméticos Web Application

## Overview
RF Cosméticos is a Flask-based web application for a cosmetics and perfume business. The app is designed to showcase imported perfumes and provide a way for customers to learn about products and contact the business. The project uses a simple architecture with Flask for the backend, Bootstrap and custom CSS for the frontend, and is configured for deployment on Replit.

## User Preferences
Preferred communication style: Simple, everyday language.

## System Architecture
The application follows a simple monolithic architecture using Flask. It's a lightweight web application focused on presenting information about RF Cosméticos and its products. Key architectural decisions include:

1. **Frontend**: HTML templates with Bootstrap 5 for responsive design and styling
2. **Backend**: Flask web framework handling routing and page rendering
3. **Deployment**: Configured for Replit using Gunicorn as the WSGI HTTP Server
4. **Static Content**: Images, CSS, and JavaScript served from the static directory

### Rationale
This simple architecture was chosen because:
- The current needs are primarily informational (product showcase, company info)
- Flask provides a lightweight, easy-to-maintain solution for a simple website
- The monolithic design allows for quick development and straightforward deployment

## Key Components

### Flask Application (app.py)
The core of the application is a simple Flask app that handles routing and template rendering. It's currently minimal with just an index route but appears designed to be extended with more functionality.

```python
# Main application entry point
app = Flask(__name__)
app.secret_key = os.environ.get("SESSION_SECRET", "rf_cosmeticos_secret_key")
```

### Templates
The application uses Jinja2 templates with a base template that includes:
- Common structure and navigation
- Meta information
- CSS/JS includes
- Header and main navigation components

Individual pages like `index.html` extend this base template.

### Static Assets
Static files are organized in the following structure:
- `/static/css/` - Stylesheet files including `styles.css`
- `/static/js/` - JavaScript files including `script.js`
- `/static/images/` - Image assets including the logo

## Data Flow
Currently, the application follows a simple request-response pattern:
1. User requests a page (e.g., homepage)
2. Flask routes the request to the appropriate handler
3. The handler renders the corresponding template
4. The rendered HTML is returned to the user

Future enhancements might include:
- User authentication (suggested by Flask-Login dependency)
- Database integration (suggested by Flask-SQLAlchemy dependency)
- Form handling for customer inquiries

## External Dependencies
The application relies on several external libraries and frameworks:

### Python Dependencies
- Flask (web framework)
- Flask-Login (for user authentication - not yet implemented)
- Flask-SQLAlchemy (for database ORM - not yet implemented)
- Gunicorn (WSGI HTTP server for deployment)
- Psycopg2-binary (PostgreSQL adapter - not yet implemented)
- Email-validator (for validating email addresses)
- Werkzeug (WSGI utilities)

### Frontend Dependencies (loaded via CDN)
- Bootstrap 5 (CSS framework)
- Font Awesome 6.4.0 (icon library)
- Animate.css (animation library)

## Deployment Strategy
The application is configured for deployment on Replit with the following components:

### Replit Configuration
- Python 3.11 as the primary runtime
- Nix packages for OpenSSL and PostgreSQL
- Deployment target set to "autoscale"
- Run command using Gunicorn

### Workflow Configuration
The Replit workflow is set up with:
- A main "Project" workflow running in parallel
- A "Start application" task that executes Gunicorn 
- Port 5000 exposed for the application

```
gunicorn --bind 0.0.0.0:5000 --reuse-port --reload main:app
```

This configuration ensures the application is properly served in the Replit environment with auto-reloading for development.

## Future Considerations

### Database Implementation
The dependencies indicate plans for database functionality:
- Flask-SQLAlchemy and Psycopg2 suggest a PostgreSQL database will be used
- This would enable features like product catalog, user accounts, and order management

### Authentication System
Flask-Login dependency suggests plans for user authentication, which could support:
- Customer accounts
- Admin interface for managing products
- Order history tracking

### Contact Form Processing
The WhatsApp links could be supplemented with a contact form that:
- Validates input using email-validator
- Stores inquiries in the database
- Sends email notifications to administrators