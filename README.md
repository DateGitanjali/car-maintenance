# Smart Car Service & Maintenance Booking System

A comprehensive full-stack web application for managing car service appointments with role-based access for customers, admins, drivers, and mechanics.

## Features

### Customer Features
- User registration and authentication
- Vehicle management (add, edit, delete vehicles)
- Book service appointments with two modes:
  - Self-Drop Service
  - Pickup & Drop Service
- Real-time booking status tracking
- Online and COD payment options
- Invoice generation and download
- Service feedback and ratings
- Dashboard with booking history

### Admin/Manager Features
- Manage all bookings
- Assign drivers and mechanics to bookings
- Update booking status
- View all registered users
- Manage drivers and mechanics
- Generate service reports and analytics
- View payment information

### Driver Features
- View assigned pickup tasks
- Update pickup/delivery status
- Track earnings
- View assigned bookings

### Mechanic Features
- View assigned service jobs
- Update service status
- Upload service reports

## Tech Stack

### Backend
- **Framework**: Django 4.2
- **API**: Django REST Framework
- **Database**: SQLite (default) / MySQL
- **Authentication**: Token-based authentication
- **CORS**: django-cors-headers

### Frontend
- **HTML5** with semantic markup
- **CSS3** with Bootstrap 5
- **JavaScript** (Vanilla JS with Fetch API)
- **Responsive Design** for mobile and desktop

## Project Structure

\`\`\`
car-service-booking/
├── manage.py
├── requirements.txt
├── car_service/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── views.py
├── accounts/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── admin.py
├── vehicles/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── admin.py
├── bookings/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── admin.py
├── payments/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   └── admin.py
└── templates/
    ├── base.html
    ├── home.html
    ├── register.html
    ├── login.html
    ├── dashboard.html
    ├── book-service.html
    ├── my-bookings.html
    ├── booking-detail.html
    ├── admin-dashboard.html
    ├── driver-dashboard.html
    ├── profile.html
    ├── payment.html
    ├── invoice.html
    └── feedback.html
\`\`\`

## Installation & Setup

### Prerequisites
- Python 3.8+
- pip (Python package manager)
- Virtual environment (recommended)

### Step 1: Clone the Repository
\`\`\`bash
git clone <repository-url>
cd car-service-booking
\`\`\`

### Step 2: Create Virtual Environment
\`\`\`bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
\`\`\`

### Step 3: Install Dependencies
\`\`\`bash
pip install -r requirements.txt
\`\`\`

### Step 4: Database Setup
\`\`\`bash
python manage.py makemigrations
python manage.py migrate
\`\`\`

### Step 5: Create Superuser (Admin)
\`\`\`bash
python manage.py createsuperuser
\`\`\`

### Step 6: Create Sample Data (Optional)
\`\`\`bash
python manage.py shell
\`\`\`

Then in the shell:
\`\`\`python
from bookings.models import ServiceType
from decimal import Decimal

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

exit()
\`\`\`

### Step 7: Run Development Server
\`\`\`bash
python manage.py runserver
\`\`\`

The application will be available at `http://localhost:8000`

## Usage

### Admin Access
1. Go to `http://localhost:8000/admin`
2. Login with superuser credentials
3. Manage users, bookings, and service types

### Customer Registration
1. Go to `http://localhost:8000/register`
2. Fill in registration form
3. Select "Customer" as role
4. Login with credentials

### Booking a Service
1. Login as customer
2. Go to "Book Service"
3. Select vehicle and service type
4. Choose service mode (Self-Drop or Pickup & Drop)
5. Select date and time
6. Confirm booking
7. Proceed to payment

### Admin Dashboard
1. Login as admin
2. Go to Admin Dashboard
3. View all bookings
4. Assign drivers and mechanics
5. Update booking status
6. View reports

### Driver Dashboard
1. Login as driver
2. Go to Driver Dashboard
3. View assigned pickups
4. Update status (Picked, Delivered)
5. View earnings

## API Endpoints

### Authentication
- `POST /api/accounts/users/register/` - Register new user
- `POST /api/accounts/users/login/` - Login user

### Vehicles
- `GET /api/vehicles/` - List user's vehicles
- `POST /api/vehicles/` - Add new vehicle
- `PUT /api/vehicles/{id}/` - Update vehicle
- `DELETE /api/vehicles/{id}/` - Delete vehicle

### Bookings
- `GET /api/bookings/bookings/` - List all bookings
- `POST /api/bookings/bookings/` - Create new booking
- `GET /api/bookings/bookings/{id}/` - Get booking details
- `POST /api/bookings/bookings/{id}/update_status/` - Update booking status
- `POST /api/bookings/bookings/{id}/assign_driver/` - Assign driver
- `POST /api/bookings/bookings/{id}/assign_mechanic/` - Assign mechanic
- `GET /api/bookings/service-types/` - List service types

### Payments
- `POST /api/payments/payments/process_payment/` - Process payment
- `GET /api/payments/invoices/` - List invoices

## Status Flow

\`\`\`
Booked → Approved → Car Picked → In Service → Ready → Out for Delivery → Delivered → Completed
\`\`\`

## Features Implemented

✅ User authentication with role-based access
✅ Vehicle management
✅ Booking system with two service modes
✅ Real-time status tracking
✅ Admin dashboard with analytics
✅ Driver dashboard with task management
✅ Payment processing (simulated)
✅ Invoice generation
✅ Feedback and ratings system
✅ Responsive UI with Bootstrap
✅ REST API endpoints
✅ CORS support

## Future Enhancements

- Email notifications for booking updates
- SMS notifications
- PDF invoice generation
- Real payment gateway integration (Stripe, PayPal)
- Google Maps integration for location tracking
- Push notifications
- Mobile app (React Native/Flutter)
- Advanced analytics and reporting
- Service history and maintenance reminders
- Customer support chat

## Troubleshooting

### Database Issues
\`\`\`bash
python manage.py flush  # Clear database
python manage.py migrate  # Reapply migrations
\`\`\`

### Static Files Not Loading
\`\`\`bash
python manage.py collectstatic
\`\`\`

### Port Already in Use
\`\`\`bash
python manage.py runserver 8001
\`\`\`

## Security Notes

- Change `SECRET_KEY` in production
- Set `DEBUG = False` in production
- Use environment variables for sensitive data
- Implement HTTPS in production
- Add rate limiting for API endpoints
- Implement proper CORS policies

## License

This project is open source and available under the MIT License.

## Support

For issues and questions, please create an issue in the repository or contact support@smartcarservice.com

## Contributors

- Development Team

---

**Version**: 1.0.0
**Last Updated**: 2025
