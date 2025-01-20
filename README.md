# Gym Class Scheduling & Membership Management System

The **Gym Class Scheduling and Membership Management System** is a robust Django-based application designed to streamline gym operations. It efficiently manages class schedules, trainers, and trainee bookings while enforcing critical business rules and maintaining role-based access control.

![image](https://github.com/user-attachments/assets/d86a0b04-3719-40f3-a95e-c59450551cfd)


## Features and Functionality

### User Roles and Permissions

#### 👤 **User Registration**
- 🚀 All new users register with the **default role set to None**.
- 🛠️ Superusers have full control over assigning and managing user roles.

---

### 🔑 **Role Management**

#### ⭐ **Superuser**
- **Responsibilities**:
  - 🔒 Manage roles and grant admin privileges to any user.
  - ⚙️ Use the [`/accounts/user`](https://gym-class-scheduling-q6cx.vercel.app/accounts/users/) API or admin dashboard for role management.
- **Access**:
  - 🛡️ Full access to all features and functionalities.

#### 👔 **Admin**
- **Responsibilities**:
  - 📋 Manage trainers and class schedules.
  - 🛠️ Perform all administrative tasks.

#### 🧑‍🏫 **Trainer**
- **Creation**:
  - Created **only by admin users**.
  - Requires a valid username or email from an existing active user.
- **Access**:
  - 🗓️ View only their assigned class schedules.
  - ⚠️ Cannot access schedules if the username or email is invalid.

#### 🧑‍💻 **Trainee**
- **Default Role**:
  - All normal users register with this role.
- **Access**:
  - 📅 Book **one class per day** based on the available schedule.

---

### ⚙️ **Business Rules**

#### 📅 **Class Scheduling**
- 🕒 Each day is limited to a **maximum of 5 class schedules**.
- ⏳ Each class lasts for **2 hours**.
- 👥 A **maximum of 10 trainees per class schedule** is enforced.
- 🛠️ Admins handle scheduling and assigning trainers to schedules.

#### 🏋️ **Booking System**
- ✅ Trainees can book class schedules **if slots are available**.
- ❌ Trainees cannot book **multiple classes in the same time slot**.
- 🔄 Bookings can be canceled by trainees if necessary.

---


## Tech Stack
- **Backend**: Django, Django REST Framework
- **Database**: PostgreSQL ( Superbase)
- **Authentication**: JWT-based authentication
- **Deployment**: Hosted on [vercel](https://vercel.com/)
---

## Project Structure

```plaintext
GYM/  # Project Root
│── gym/  # Django Project Folder
│   │── settings.py  # Main project settings
│   │── urls.py  # URL configurations
│   │── asgi.py  # ASGI entry point for async support
│   │── wsgi.py  # WSGI entry point for deployment
│
│── accounts/  # User Authentication & Profile Management App
│   │── models.py  # User models
│   │── serializers.py  # DRF serializers
│   │── views.py  # API views for authentication
│   │── urls.py  # Routes for authentication
│
│── admins/  # Admin-specific functionalities
│   │── models.py  # Trainer, ClassSchedule models
│   │── serializers.py
│   │── views.py
│   │── urls.py
│
│── trainees/  # Trainee-related features (Gym members)
│   │── models.py  # Booking models
│   │── serializers.py
│   │── views.py
│   │── urls.py
│
│── trainers/  # Gym trainers management
│   │── models.py
│   │── serializers.py
│   │── views.py
│   │── urls.py
│
│── manage.py  # Django management script
│── README.md  # Project documentation
│── requirements.txt  # Python dependencies
```


# 🔐 User Roles and Credentials

| **Role**    | **Username** | **Password**  |
|-------------|--------------|---------------|
| **Superuser** | admin      | admin1234     |
| **Admin**     | meraz      | meraz2004     |
| **Trainer**   | sagor      | meraz2004     |
| **Trainee**   | antor      | meraz2004     |


## API Endpoints

### Accounts

- **Register**: `POST /accounts/register/`
- **Login**: `POST /accounts/login/`
- **Profile**: `GET /accounts/profile/`
- **Logout**: `POST /accounts/logout/`
- **All User**: `POST/GET/PUT/DELETE /accounts/users/`
- 

### Admins

- **Manage Trainers**: `GET/POST /admins/trainers/`
- **Manage Class Schedules**: `GET/POST /admins/class-schedules/`
  - **Request Body Example**:
    ```json
    {
      "date": "2025-01-19",
      "start_time": "08:00:00",
      "trainer": 1
    }
    ```

### Trainers

- **View Schedules**: `GET /trainers/my-schedules/`
  - **Response Example**:
    ```json
    {
      "success": true,
      "schedules": [
        {
          "id": 1,
          "date": "2025-01-19",
          "start_time": "08:00:00",
          "end_time": "10:00:00",
          "trainer": "John Doe"
        }
      ]
    }
    ```

### Bookings

- **View All Bookings**: `GET /book/bookings/`
- **View Specific Booking**: `GET /book/bookings/{id}`
- **Create Booking**: `POST /book/bookings/`
  - **Request Body Example**:
    ```json
    {
      "schedule": 1
    }
    ```
- **Cancel Booking**: `DELETE /book/bookings/{id}`

## Authentication and Authorization

The system uses **JWT-based authentication** to enforce role-based access:

- **Admins** can manage trainers and schedules.
- **Trainers** can only view their assigned schedules.
- **Trainees** can book available classes.

## Error Handling

### Unauthorized Access

- **Error Message**:
  ```json
  {
    "detail": "Unauthorized access"
  }
  ```

### Validation Errors

- **Example**: Invalid email format or missing required fields.
- **Error Message**:
  ```json
  {
    "email": ["Enter a valid email address."]
  }
  ```

### Trainer Not Found

- **Error Message**:
  ```json
  {
    "success": false,
    "message": "Validation error occurred. Check your matched trainer name and email address.",
    "errorDetails": {
      "field": "trainer",
      "message": "Trainer not found"
    }
  }
  ```

## Installation and Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/gym-management-system.git
   cd gym-management-system
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Apply migrations:
   ```bash
   python manage.py migrate
   ```

5. Create a superuser:
   ```bash
   python manage.py createsuperuser
   ```

6. Run the development server:
   ```bash
   python manage.py runserver
   ```

7. Access the application:
   - API Root: [https://gym-class-scheduling-q6cx.vercel.app/](https://gym-class-scheduling-q6cx.vercel.app/)
   - Admin Panel: [https://gym-class-scheduling-q6cx.vercel.app/admin/](https://gym-class-scheduling-q6cx.vercel.app/admin/)



Enjoy managing your gym efficiently with this system!
