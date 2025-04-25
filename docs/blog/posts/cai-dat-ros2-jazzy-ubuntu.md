---
date:
  created: 2025-04-01
  updated: 2025-05-02
authors:
  - p_hieu
categories:
  - Mới bắt đầu  
tags:
  - Mới bắt đầu 
  - Ros2
  - festive season  
pin: true
draft: true
links:
  - Homepage: index.md
  - Blog index: blog/index.md
  - External links:
    - Material documentation: https://squidfunk.github.io/mkdocs-material
  
---

# Hướng dẫn cài đặt ros2
 Bạn có thể follow đầy đủ hướng dẫn ở đây: https://docs.ros.org/en/jazzy/Installation.html

Trong post này mình sẽ enable Ubuntu trên windows thông qua wsl (rất nhẹ và tiện so với cách cài song song 2 hệ điều hành).

> Các os khác thì bạn vui lòng xem hướng dẫn chính thức  từ ros2 ở  https://docs.ros.org/en/jazzy/Installation.html

Mở CMD hoặc Terminal trên window và cài đặt ubuntu 24.04 trên WSL, ví dụ

     WSL --install Ubuntu

- Thiết lập ngôn ngữ
```bash
locale  # Kiểm tra locale hiện tại
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
locale  # Xác nhận lại lần nữa UTF-8
```

- Thêm kho lưu trữ từ Ubuntu Universe
```bash 
	sudo  apt  install  software-properties-common
    sudo  add-apt-repository  universe
```
Bây giờ thêm khóa ROS 2 GPG bằng apt.
```bash 
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```
Sau đó thêm kho lưu trữ vào danh sách nguồn của bạn.
```bash 
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
- Cài đặt các gói cần thiết 
```bash 
sudo apt update && sudo apt install -y \
  python3-flake8-blind-except \
  python3-flake8-class-newline \
  python3-flake8-deprecated \
  python3-mypy \
  python3-pip \
  python3-pytest \
  python3-pytest-cov \
  python3-pytest-mock \
  python3-pytest-repeat \
  python3-pytest-rerunfailures \
  python3-pytest-runner \
  python3-pytest-timeout \
  ros-dev-tools
```

   - Source thư viện (bắt buộc phải làm mỗi khi mở terminal mới)
```bash
source /opt/ros/jazzy/setup.bash   

```

   - Tạo thư mục code 
>  Tên packages nên dùng dấu gạch dưới (_) không được dùng dấu (-) sẽ xảy ra nhiều lỗi sau này
```bash
source /opt/ros/jazzy/setup.bash   
mkdir -p ~/ros2_learn/src
cd ~/ros2_learn
ros2 pkg create --build-type ament_python --license Apache-2.0 hello_world
colcon build --symlink-install --packages-select hello_world
source install/local_setup.bash
```

- Ok, tạm thời đến đây thôi, trong bài viết tiếp theo tôi sẽ hướng dẫn bạn chạy ví dụ nho nhỏ và bạn sẽ thấy gì đó thú vị hơn. 

