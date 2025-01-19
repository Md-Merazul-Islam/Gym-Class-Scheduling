GYM/                              # Project Root
│── gym/                          # Django Project Folder
│   │── __init__.py
│   │── settings.py               # Main project settings
│   │── urls.py                    # URL configurations
│   │── wsgi.py                    # WSGI entry point for deployment
│   │── asgi.py                    # ASGI entry point for async support
│   │── middleware.py               # Custom middlewares (if any)
│
│── accounts/                      # User Authentication & Profile Management App
│   │── migrations/                 # Database migrations
│   │── __init__.py
│   │── admin.py                    # Admin panel integration
│   │── apps.py
│   │── models.py                   # User models
│   │── serializers.py              # DRF serializers
│   │── views.py                    # API views for authentication
│   │── urls.py                      # Routes for authentication
│   │── tests.py
│
│── admins/                         # Admin-specific functionalities
│   │── migrations/
│   │── __init__.py
│   │── admin.py
│   │── apps.py
│   │── models.py                   # Trainer, ClassSchedule models
│   │── serializers.py
│   │── views.py
│   │── urls.py
│   │── tests.py
│
│── trainees/                       # Trainee-related features (Gym members)
│   │── migrations/
│   │── __init__.py
│   │── admin.py
│   │── apps.py
│   │── models.py                    # Booking  models
│   │── serializers.py                # DRF serializers for trainees
│   │── views.py                      # API views for trainees
│   │── urls.py
│   │── tests.py
│
│── trainers/                        # Gym trainers management
│   │── migrations/
│   │── __init__.py
│   │── admin.py
│   │── apps.py
│   │── models.py                    #  models
│   │── serializers.py                # DRF serializers for trainers
│   │── views.py
│   │── urls.py
│   │── tests.py
│
│── venv/                             # Virtual Environment (Not in Git)
│── db.sqlite3                         # Database file (SQLite or Postgres if configured)
│── manage.py                          # Django management script
│── README.md                          # Project documentation
│── requirements.txt                    # Python dependencies
│── .gitignore                          # Git ignore file
