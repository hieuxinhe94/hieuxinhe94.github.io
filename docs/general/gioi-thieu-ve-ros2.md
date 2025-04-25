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
# Giới thiệu về Robot Operating System

Nếu bạn chỉ muốn thiết kế những robot đồ chơi hoặc sản phẩm gia dụng đơn giản trên thị trường cả chục năm nay, thực tế, bạn chỉ cần học một vài thứ nhỏ như Pygame, hay mô-đun điều khiển, hay một thư mục như OpenCV là đủ. Tuy nhiên chúng ta không ở đây để dừng lại mức đó, chúng ta cần robot với việc giao tiếp giữa các sensor, camera, di chuyển phức tạp, có khả năng tự hành, trí thông minh của AI, thì bạn cần một tập hợp các thư viện phức tạp. Dĩ nhiên các tập đoàn lớn như Tesla họ sẽ tự xây dựng riêng bộ thư viện của họ vì là bí mật kinh doanh, nhưng hầu như các công ty nổi tiếng khác đều sử dụng **Robot Operating System** trong mục đích mô phỏng, thiết kế robot. 

# Tại sao là Robot Operating System :
Là một opensource nhưng ROS (Robot Operating System) cung cấp khá đồ sộ những công cụ và khả năng customize, mở rộng rất cao là ưu điểm lớn. 

So sánh giũa Ros và việc tự implement bằng Python/OpenCV/... 

|Tính năng       |Robot Operating System         |Tự customize Python/OpenCV/...|
|----------------|-------------------------------|-----------------------------|
|Giao tiếp phân tán|`Có sẵn (Nodes, Topics, DDS)` |Không có – phải tự viết     |
|Điều khiển real-time         |`Hỗ trợ tốt`            |Khó đạt                |
|Kết nối phần cứng linh hoạt|Có hardware interface sẵn|Phải tự code driver|
|Mô phỏng robot          |Tích hợp RViz, Gazebo|Không hỗ trợ trực tiếp
|Điều hướng tự hành          |Navigation2, SLAM2D, MoveIt2|Phải tự code|
|Quan sát dữ liệu realtime          |rqt, RViz, Foxglove Studio|Phải tự viết UI|
|Cộng đồng hỗ trợ          |Rất mạnh vì không có lựa chọn khác|Không chuyên dụng|

> **Quan trọng :** Thời điểm viết khóa học này ROS đã release phiên bản khá ổn định là **ROS2 Jazzy** thế nên từ sau đây, mặc định các nội dung hay thuật ngữ của tôi sẽ áp dụng từ phiên bản này trở đi!


# Các thành phần chính trong ROS 2

    [ Sensor / Motor / Camera ]
            ↓
    [ Hardware Interface ]  <--- Kết nối driver phần cứng
            ↓
    [ Controller Manager ]  <--- Quản lý PID, trajectory, velocity...
            ↓
    [ ROS Nodes ]           <--- Perception, Planning, Control
            ↓
    [ Topic / Service / Action / TF ]
            ↓
    [ Visualization / GUI / Web / AI / SLAM ]

> Mỗi thành phần chính sẽ tách thành bài học nhỏ đảm bảo bạn không bị khủng hoảng, và tôi cũng cố gắng thay đổi cách tiếp cận của các khóa học từ nước ngoài. Lộ trình học này có thể khác biệt nhưng theo tôi nó sẽ giúp bạn tự tin từng bước và cảm giác liên tục đạt được những thành tựu và hạn chế sự bỏ cuộc.

Danh sách các thành phần chính trong ros2:

| Thành phần |Mô tả  | Bài học|
|--|--|--|
| **Hardware Interface** | Giao tiếp phần cứng qua C++|--|
| **URDF/XACRO**| Mô tả hình học và khớp nối robot|--|
| **TF2** | Quản lý hệ trục tọa độ động|--|
| **Gazebo** | Mô phỏng vật lý 3D|--|
| **RViz** | Visualization 3D dữ liệu robot|--|
| **Nodes** |Đơn vị xử lý độc lập, chạy song song, giao tiếp qua topics/services/actions|--|
| **Lifecycle nodes**| Cho phép kiểm soát vòng đời của node (inactive, active...)|--|
| **Parameters**| Cấu hình động cho nodes|--|
| **Launch system**| Tự động khởi tạo nodes, cấu hình hệ thống|--|
| **Executors** | Điều phối việc thực thi các callbacks trong nodes|--|
| **Topics** | Kênh truyền dữ liệu kiểu publish/subscribe|--|
| **Services**| Giao tiếp 2 chiều kiểu request/response|--|
| **Actions**| Thực hiện các tác vụ dài hạn có thể theo dõi trạng thái|--|
| **Controller Manager**| Quản lý các controller (PID, joint, velocity, effort...)|--|
| **ros2_control**| Framework điều khiển phần cứng thời gian thực|--|
| **ros2_controllers**| Bộ sưu tập các controller tiêu chuẩn|--|
| **Navigation2**| Điều hướng và SLAM|--|
| **AI/ML/Deep Learning**| ROS có thể tích hợp mô hình AI như YOLOv5, Detectron2, LLMs, thông qua ROS Nodes sử dụng Python/C++ để inference từ camera, lidar...|--|

Rất nhiều người khi mới học ROS 2 đều cảm thấy **hoang mang**, kể cả những người đã biết lập trình lâu năm. Đây là lĩnh vực vừa dính đến **code**, vừa dính đến **robot học**, **real-time**, lại còn **hệ thống phân tán** nữa — cho nên **khó là chuyện bình thường**.

Giờ chúng ta **chính thức xuất phát nhé!**


 