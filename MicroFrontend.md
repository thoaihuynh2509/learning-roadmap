# Part 1: Bắt đầu với Micro Frontend
## 1. Khái quát về Micro Frontend (MF)

Micro frontends là một kiến trúc phần mềm mà trong đó, nó sẽ chia ứng dụng theo hướng **vertical domain**.
Tuơng ứng, mỗi phần được xây dựng từ database đến UI và được điều hành bởi một team chuyên dụng.
Các team frontend sẽ tích hợp các phần của mình để tạo ra một website cho người dùng sử dụng.

![image](https://user-images.githubusercontent.com/30824675/146969051-43a9c5bf-978a-4628-bc9a-086983c93dc5.png)

Lý do chính để sử dụng:
- Tối ưu hóa cho việc phát triển tính năng: 
  - Một team sẽ bao gồm tất cả các kỹ năng cần thiết để phát triển một tính năng. 
  - Không cần phối hợp giữa các frontend team và backend team riêng biệt.
- Dễ dàng nâng cấp FE: Các team có thể quyết định cập nhật hoặc chuyển đổi công nghệ FE của họ một cách độc lập.
- Tăng sự hiểu rõ về business domain: Mỗi team sẽ thực hiện các tính năng trực tiếp cho khách hàng. 
- Dễ dàng hơn cho dev mới khi tìm hiểu các app nhỏ hơn thay vì hiểu monolith với cả ngàn dòng code.
