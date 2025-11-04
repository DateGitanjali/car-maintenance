# Complete Setup Guide - Smart Car Service Booking System

## Quick Start (5 minutes)

### 1. Install Python Dependencies
\`\`\`bash
pip install -r requirements.txt
\`\`\`

### 2. Run Migrations
\`\`\`bash
python manage.py migrate
\`\`\`

### 3. Create Admin User
\`\`\`bash
python manage.py createsuperuser
\`\`\`

### 4. Start Server
\`\`\`bash
python manage.py runserver
\`\`\`

### 5. Access Application
- Frontend: http://localhost:8000
- Admin: http://localhost:8000/admin
- API: http://localhost:8000/api/

---

## Detailed Setup

### Database Configuration

#### SQLite (Default)
No additional setup needed. Database file will be created automatically.

#### MySQL Setup
1. Install MySQL server
2. Create database:
\`\`\`sql
CREATE DATABASE car_service_db;
CREATE USER 'car_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON car_service_db.* TO 'car_user'@'localhost';
FLUSH PRIVILEGES;
\`\`\`

3. Update `settings.py`:
\`\`\`python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'car_service_db',
        'USER': 'car_user',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
\`\`\`

4. Install MySQL driver:
\`\`\`bash
pip install mysqlclient
\`\`\`

### Creating Test Data

\`\`\`bash
python manage.py shell
\`\`\`

\`\`\`python
from django.contrib.auth.models import User
from accounts.models import UserProfile
from bookings.models import ServiceType
from decimal import Decimal

# Create test users
customer = User.objects.create_user(
    username='customer1',
    email='customer@example.com',
    password='testpass123',
    first_name='John',
    last_name='Doe'
)
UserProfile.objects.create(user=customer, role='customer', phone='9876543210')

admin_user = User.objects.create_user(
    username='admin1',
    email='admin@example.com',
    password='testpass123',
    first_name='Admin',
    last_name='User'
)
UserProfile.objects.create(user=admin_user, role='admin', phone='9876543211')

driver = User.objects.create_user(
    username='driver1',
    email='driver@example.com',
    password='testpass123',
    first_name='Driver',
    last_name='User'
)
UserProfile.objects.create(user=driver, role='driver', phone='9876543212')

# Create service types
ServiceType.objects.create(
    name="Basic Service",
    description="Oil change, filter replacement, and basic inspection",
    base_price=Decimal('49.00'),
    estimated_duration=1
)

ServiceType.objects.create(
    name="Standard Service",
    description="Comprehensive maintenance including fluid checks",
    base_price=Decimal('99.00'),
    estimated_duration=2
)

ServiceType.objects.create(
    name="Premium Service",
    description="Complete overhaul with detailed inspection",
    base_price=Decimal('199.00'),
    estimated_duration=3
)

print("Test data created successfully!")
exit()
\`\`\`

### Environment Variables

Create `.env` file in project root:
\`\`\`
DEBUG=True
SECRET_KEY=your-secret-key-here
ALLOWED_HOSTS=localhost,127.0.0.1
DATABASE_URL=sqlite:///db.sqlite3
\`\`\`

### Running Tests

\`\`\`bash
python manage.py test
\`\`\`

### Collecting Static Files

\`\`\`bash
python manage.py collectstatic --noinput
\`\`\`

---

## Deployment

### Using Gunicorn

1. Install Gunicorn:
\`\`\`bash
pip install gunicorn
\`\`\`

2. Run with Gunicorn:
\`\`\`bash
gunicorn car_service.wsgi:application --bind 0.0.0.0:8000
\`\`\`

### Using Docker

Create `Dockerfile`:
\`\`\`dockerfile
FROM python:3.9
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["gunicorn", "car_service.wsgi:application", "--bind", "0.0.0.0:8000"]
\`\`\`

Build and run:
\`\`\`bash
docker build -t car-service .
docker run -p 8000:8000 car-service
\`\`\`

### Production Checklist

- [ ] Set `DEBUG = False`
- [ ] Change `SECRET_KEY`
- [ ] Configure allowed hosts
- [ ] Set up HTTPS/SSL
- [ ] Configure database (PostgreSQL recommended)
- [ ] Set up email backend
- [ ] Configure static files serving
- [ ] Set up logging
- [ ] Configure CORS properly
- [ ] Set up monitoring and alerts

---

## Troubleshooting

### Issue: ModuleNotFoundError
**Solution**: Ensure virtual environment is activated and all dependencies are installed
\`\`\`bash
pip install -r requirements.txt
\`\`\`

### Issue: Database locked
**Solution**: Delete `db.sqlite3` and run migrations again
\`\`\`bash
rm db.sqlite3
python manage.py migrate
\`\`\`

### Issue: Port 8000 already in use
**Solution**: Use different port
\`\`\`bash
python manage.py runserver 8001
\`\`\`

### Issue: Static files not loading
**Solution**: Collect static files
\`\`\`bash
python manage.py collectstatic
\`\`\`

### Issue: CORS errors
**Solution**: Check CORS settings in `settings.py` and ensure frontend URL is in `CORS_ALLOWED_ORIGINS`

---

## Performance Optimization

1. **Database Indexing**: Add indexes to frequently queried fields
2. **Caching**: Implement Redis caching for frequently accessed data
3. **Pagination**: API endpoints are paginated by default
4. **Compression**: Enable gzip compression in production
5. **CDN**: Serve static files from CDN

---

## Security Hardening

1. **HTTPS**: Always use HTTPS in production
2. **CSRF Protection**: Enabled by default
3. **SQL Injection**: Protected by Django ORM
4. **XSS Protection**: Implement Content Security Policy
5. **Rate Limiting**: Add rate limiting to API endpoints
6. **Input Validation**: Validate all user inputs
7. **Authentication**: Use strong password policies

---

## Monitoring & Logging

Configure logging in `settings.py`:
\`\`\`python
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'handlers': {
        'file': {
            'level': 'ERROR',
            'class': 'logging.FileHandler',
            'filename': 'errors.log',
        },
    },
    'loggers': {
        'django': {
            'handlers': ['file'],
            'level': 'ERROR',
            'propagate': True,
        },
    },
}
\`\`\`

---

## Support & Resources

- Django Documentation: https://docs.djangoproject.com/
- Django REST Framework: https://www.django-rest-framework.org/
- Bootstrap Documentation: https://getbootstrap.com/docs/
- Python Documentation: https://docs.python.org/

---

**Last Updated**: 2025
