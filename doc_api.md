# API Documentation - Clinic Management System

## Base URL
```
http://your-domain/api
```

## Authentication

### Register User
- **URL**: `/auth/register`
- **Method**: `POST`
- **Description**: Đăng ký tài khoản mới cho bệnh nhân
- **Request Body**:
```json
{
    "username": "string",
    "password": "string",
    "confirmPassword": "string",
    "name": "string",
    "email": "string",
    "phone": "string (10 digits)"
}
```
- **Response**:
```json
{
    "message": "Đăng ký thành công"
}
```

### Register Doctor (Admin only)
- **URL**: `/auth/register/doctor`
- **Method**: `POST`
- **Description**: Đăng ký tài khoản mới cho bác sĩ (yêu cầu quyền ADMIN)
- **Request Body**: Giống như Register User
- **Response**: 
```json
{
    "message": "Đăng ký tài khoản bác sĩ thành công"
}
```

### Login
- **URL**: `/auth/login`
- **Method**: `POST`
- **Description**: Đăng nhập và nhận JWT token
- **Request Body**:
```json
{
    "username": "string",
    "password": "string"
}
```
- **Response**:
```json
{
    "token": "JWT_TOKEN"
}
```

### Change Password
- **URL**: `/auth/change-password`
- **Method**: `POST`
- **Description**: Đổi mật khẩu cho tài khoản hiện tại
- **Request Body**:
```json
{
    "currentPassword": "string",
    "newPassword": "string",
    "confirmPassword": "string"
}
```
- **Response**:
```json
{
    "message": "Đổi mật khẩu thành công"
}
```

## User Management

### Get Current User
- **URL**: `/users/me`
- **Method**: `GET`
- **Description**: Lấy thông tin user đang đăng nhập
- **Response**: User object

### Update Current User
- **URL**: `/users/me`
- **Method**: `PUT`
- **Description**: Cập nhật thông tin user đang đăng nhập
- **Request Body**:
```json
{
    "name": "string",
    "email": "string",
    "phone": "string"
}
```
- **Response**: Updated User object

### Get All Users (Admin only)
- **URL**: `/users`
- **Method**: `GET`
- **Description**: Lấy danh sách tất cả users
- **Response**: Array of User objects

### Get User by ID (Admin only)
- **URL**: `/users/{id}`
- **Method**: `GET`
- **Description**: Lấy thông tin user theo ID
- **Response**: User object

### Update User (Admin only)
- **URL**: `/users/{id}`
- **Method**: `PUT`
- **Description**: Cập nhật thông tin user theo ID
- **Request Body**: User object
- **Response**: Updated User object

### Delete User (Admin only)
- **URL**: `/users/{id}`
- **Method**: `DELETE`
- **Description**: Xóa user theo ID

### Search Users (Admin only)
- **URL**: `/users/search`
- **Method**: `GET`
- **Parameters**: 
  - `keyword`: Search term
- **Response**: Array of matching User objects

## Doctor Management

### Get All Doctors
- **URL**: `/doctors`
- **Method**: `GET`
- **Description**: Lấy danh sách tất cả bác sĩ
- **Response**: Array of Doctor objects

### Create Doctor (Admin only)
- **URL**: `/doctors`
- **Method**: `POST`
- **Description**: Tạo thông tin bác sĩ mới
- **Request Body**:
```json
{
    "name": "string",
    "specialization": "string",
    "description": "string",
    "email": "string",
    "phone": "string",
    "userId": "number"
}
```
- **Response**: Created Doctor object

### Get Doctor by ID
- **URL**: `/doctors/{id}`
- **Method**: `GET`
- **Description**: Lấy thông tin bác sĩ theo ID
- **Response**: Doctor object

### Update Doctor (Admin only)
- **URL**: `/doctors/{id}`
- **Method**: `PUT`
- **Description**: Cập nhật thông tin bác sĩ
- **Request Body**: Doctor object
- **Response**: Updated Doctor object

### Delete Doctor (Admin only)
- **URL**: `/doctors/{id}`
- **Method**: `DELETE`
- **Description**: Xóa thông tin bác sĩ

### Search Doctors
- **URL**: `/doctors/search`
- **Method**: `GET`
- **Parameters**:
  - `keyword`: Search term
- **Response**: Array of matching Doctor objects

### Get Doctor Schedule
- **URL**: `/doctors/{id}/schedule`
- **Method**: `GET`
- **Parameters**:
  - `startDate`: Date (YYYY-MM-DD)
  - `endDate`: Date (YYYY-MM-DD) (optional)
- **Response**: Array of DoctorSchedule objects

### Get All Specializations
- **URL**: `/doctors/specialization`
- **Method**: `GET`
- **Description**: Lấy danh sách tất cả chuyên khoa
- **Response**: Array of strings

### Get Doctors by Specialization
- **URL**: `/doctors/specialization/{specialization}`
- **Method**: `GET`
- **Description**: Lấy danh sách bác sĩ theo chuyên khoa
- **Response**: Array of Doctor objects

### Toggle Doctor Active Status (Admin only)
- **URL**: `/doctors/{id}/active`
- **Method**: `PUT`
- **Description**: Bật/tắt trạng thái hoạt động của bác sĩ
- **Response**: Updated Doctor object

## Appointment Management

### Create Appointment
- **URL**: `/appointments`
- **Method**: `POST`
- **Description**: Tạo lịch hẹn mới
- **Request Body**:
```json
{
    "doctorId": "number",
    "patientName": "string",
    "patientPhone": "string",
    "appointmentTime": "datetime",
    "notes": "string"
}
```
- **Response**: Created Appointment object

### Get All Appointments (Admin/Doctor only)
- **URL**: `/appointments`
- **Method**: `GET`
- **Parameters**:
  - `startDate`: DateTime (optional)
  - `endDate`: DateTime (optional)
  - `status`: PENDING/CONFIRMED/CANCELLED/DONE (optional)
- **Response**: Array of Appointment objects

### Get My Appointments
- **URL**: `/appointments/me`
- **Method**: `GET`
- **Parameters**:
  - `startDate`: DateTime (optional)
  - `endDate`: DateTime (optional)
  - `status`: PENDING/CONFIRMED/CANCELLED/DONE (optional)
- **Response**: Array of user's Appointment objects

### Get Appointment by ID
- **URL**: `/appointments/{id}`
- **Method**: `GET`
- **Description**: Lấy thông tin lịch hẹn theo ID
- **Response**: Appointment object

### Get Doctor's Appointments (Admin/Doctor only)
- **URL**: `/appointments/doctor/{doctorId}`
- **Method**: `GET`
- **Parameters**:
  - `startDate`: DateTime (optional)
  - `endDate`: DateTime (optional)
  - `status`: PENDING/CONFIRMED/CANCELLED/DONE (optional)
- **Response**: Array of doctor's Appointment objects

### Update Appointment
- **URL**: `/appointments/{id}`
- **Method**: `PUT`
- **Description**: Cập nhật thông tin lịch hẹn
- **Request Body**: Appointment object
- **Response**: Updated Appointment object

### Update Appointment Status (Admin/Doctor only)
- **URL**: `/appointments/{id}/status`
- **Method**: `PUT`
- **Parameters**:
  - `status`: PENDING/CONFIRMED/CANCELLED/DONE
- **Response**: Updated Appointment object

### Delete Appointment
- **URL**: `/appointments/{id}`
- **Method**: `DELETE`
- **Description**: Hủy lịch hẹn

### Search Appointments (Admin/Doctor only)
- **URL**: `/appointments/search`
- **Method**: `GET`
- **Parameters**:
  - `keyword`: Search term
- **Response**: Array of matching Appointment objects

### Check Appointment Conflicts (Admin/Doctor only)
- **URL**: `/appointments/conflicts`
- **Method**: `GET`
- **Parameters**:
  - `doctorId`: Doctor ID
  - `startTime`: DateTime
  - `endTime`: DateTime
- **Response**: Array of conflicting Appointment objects

## Data Types

### User Object
```json
{
    "id": "number",
    "username": "string",
    "name": "string",
    "email": "string",
    "phone": "string",
    "role": "USER/DOCTOR/ADMIN",
    "active": "boolean"
}
```

### Doctor Object
```json
{
    "id": "number",
    "name": "string",
    "specialization": "string",
    "description": "string",
    "email": "string",
    "phone": "string",
    "user": "User object",
    "active": "boolean"
}
```

### Appointment Object
```json
{
    "id": "number",
    "patientName": "string",
    "patientPhone": "string",
    "appointmentTime": "datetime",
    "notes": "string",
    "status": "PENDING/CONFIRMED/CANCELLED/DONE",
    "doctor": "Doctor object",
    "user": "User object"
}
```

## Error Responses

### Common Error Response Format
```json
{
    "message": "Error message"
}
```

### Common HTTP Status Codes
- 200: Success
- 201: Created
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 409: Conflict
- 500: Internal Server Error

## Authentication
- Tất cả các API (trừ /auth/register và /auth/login) yêu cầu JWT token trong header:
```
Authorization: Bearer YOUR_JWT_TOKEN
``` 
