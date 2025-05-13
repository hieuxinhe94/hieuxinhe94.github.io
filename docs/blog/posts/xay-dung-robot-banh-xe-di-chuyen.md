---
date:
  created: 2025-04-01
  updated: 2025-05-02
authors:
  - p_hieu
categories:
  - Đơn giản
tags:
  - Đơn giản
  - Ros2
  - Mới bắt đầu
pin: true
draft: true
links:
  - Homepage: index.md
  - Blog index: blog/index.md
  - External links:
      - Material documentation: https://squidfunk.github.io/mkdocs-material
---

# Tóm tắt mục tiêu

Xây dựng robot đơn giản có khả năng di chuyển bằng bánh xe, thử nghiệm những thành phần quan trọng của ros2.

> Tham khảo source code đầy đủ ở đây https://github.com/hieuxinhe94/ros2-learning

## Nội dung bài viết

- Tạo mới project
- Triển khai docker
- Thiết kế prototype robot
- Cách bố trí thư mục sourcecode
- Mô tả URDF/XARCO cho robot theo prototype
- Launch hiển thị robot prototype
- Khái niệm về topics, nodes, controller
- Khái niệm Ros2 Control: controller_manager, JointStateBroadcaster, DiffDriveController...
- Implement điều khiển robot
- Random di chuyển robot

## 1. Tạo mới project

> Hướng dẫn này được thực hiện trên Ubuntu 24.04 hoặc Windows WSL (cài đặt Ubuntu 24.04)

- Tạo thư mục

```bash
mkdir -p ~/ros2-docker/src && cd ~/ros2-docker/src # tạo thư mục làm việc
```

- Tạo project với type ament_CMake (bạn có thể dùng ament_python, nhưng tôi thường chọn ament_CMake hơn, chúng ta vẫn sẽ code bằng python)

> Lưu ý tên project tránh dùng các ký hiệu - (gạch ngang),... để tránh rắc rối sau này.

```bash
ros2 pkg create --build-type ament_cmake --license Apache-2.0 first_robot # Tạo project mới tên là first_robot
code .
```

- Tạo các thư mục trong `~/ros2-docker/src/first_robot/*` lần lượt như sau:

```bash
cd ~/ros2-docker/src/first_robot/ && mkdir -p config/ description/ launch/ scripts/ worlds/
```

- Khai báo bổ sung các thư mục vừa tạo lúc buid code ở file `CMakeLists.txt`

> thêm vào cuối file và trước dòng `ament_package()`

```bash
install(
  DIRECTORY config description launch worlds scripts
  DESTINATION share/${PROJECT_NAME}
)

ament_package()
```

## 2. Thiết kế robot prototype
Trong project đầu tiên này, tôi muốn đơn giản hóa sự phức tạp robot vật lý, nên sẽ lựa chọn robot di chuyển bằng 2 bánh xe trái-phải, và một bánh xe ở giữa để cân bằng. 





