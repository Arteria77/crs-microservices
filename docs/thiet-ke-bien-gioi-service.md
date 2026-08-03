
# Danh sách Microservices

| Service | Cổng | Database | Trách nhiệm chính |
| :--- | :---: | :---: | :--- |
| **api-gateway** | 8080 | *(Không có)* | Điểm vào duy nhất, định tuyến, xác thực sơ bộ, CORS |
| **auth-service** | 8081 | `auth_db` | Quản lý User, Student, đăng nhập, sinh/xác thực JWT |
| **course-service** | 8082 | `course_db` | Quản lý Course, tìm kiếm, phân trang, quản lý số chỗ |
| **registration-service** | 8083 | `registration_db` | Quản lý Registration, gọi sang `course-service` để đăng ký |

# Bảng Định Tuyến Gateway (Dự Kiến)

| Route | Forward tới | Ghi chú |
| :--- | :--- | :--- |
| `/api/auth/**` | `http://localhost:8081` | Public (login), phần còn lại cần JWT |
| `/api/courses/**` | `http://localhost:8082` | GET public, POST/PUT/DELETE cần role ADMIN |
| `/api/registrations/**` | `http://localhost:8083` | Cần JWT (STUDENT/ADMIN) |
| `/api/public/courses` | `http://localhost:8082` | Dùng API Key, dành cho đối tác ngoài |