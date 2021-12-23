# 1. Khái quát về Micro Frontend (MF)

Micro frontends là một kiến trúc phần mềm mà trong đó, nó sẽ chia ứng dụng theo hướng **vertical domain**.
Tuơng ứng, mỗi phần được xây dựng từ database đến UI và được điều hành bởi một team chuyên dụng.
Các team frontend sẽ tích hợp các phần của mình để tạo ra một website cho người dùng sử dụng.

Lý do chính để sử dụng:
- Tối ưu hóa cho việc phát triển tính năng: 
  - Một team sẽ bao gồm tất cả các kỹ năng cần thiết để phát triển một tính năng. 
  - Không cần phối hợp giữa các frontend team và backend team riêng biệt.
- Dễ dàng nâng cấp FE: Các team có thể quyết định cập nhật hoặc chuyển đổi công nghệ FE của họ một cách độc lập.
- Tăng sự hiểu rõ về business domain: Mỗi team sẽ thực hiện các tính năng trực tiếp cho khách hàng. 
- Dễ dàng hơn cho dev mới khi tìm hiểu các app nhỏ hơn thay vì hiểu monolith với cả ngàn dòng code.

![image](https://user-images.githubusercontent.com/30824675/147120990-e91bdf52-a9bc-4185-910a-2cb71de8ce91.png)

## 1.1 Team và hệ thống
Mỗi hệ thống là tự trị, có nghĩa là nó có thể hoạt động ngay cả khi các hệ thống lân cận gặp sự cố. Mội hệ thống sẽ có cơ sở dữ liệu riêng biệt.

### 1.1.1 Nhiệm vụ của team
Một hệ thống được sở hữu bởi một team. Mỗi team có lĩnh vực chuyên môn của mình để cung cấp giá trị cho khách hàng. Mỗi team phải có tên mô tả và nhiệm vụ tập trung vào người dùng rõ ràng. 

Ví dụ: Trong các dự án của mình, chúng tôi sắp xếp các nhóm theo hành trình của khách hàng - các giai đoạn mà khách hàng phải trải qua khi mua thứ gì đó.

### 1.1.2 Cross-functional teams
Sự khác biệt đáng kể giữa Micro Frontends và các kiến trúc khác là ở team structure. 

![image](https://user-images.githubusercontent.com/30824675/147123718-41e982ae-92ce-4235-90ff-24267779f258.png)

Specialist team: 
- Mỗi thành viên sẽ được tập hợp theo kĩ năng hoặc công nghệ khác nhau.
- Các thành viên có thể thảo luận về bugs mà họ đang cố gắng sửa hoặc đưa ra các ý tưởng về cách cải thiện một phần cụ thể của mã.

Cross-functional team:
- Tất cả thành viên đều được tham gia vào quá trình phát triển tính năng.
- Giúp tất cả mọi người dễ dàng tham gia, đóng góp và quan trọng nhất là tự nhận diện sản phẩm.


## 1.2 Frontend

Mỗi team có thể dùng HTML, CSS và JS cần thiết cho một tính năng nhất định. Ngoài ra, để dễ dàng hơn thì họ có thể sử dụng các thư viện hay framework có sẵn như React, Angular, Vue,... Mỗi team được tự do lựa chọn thư viện hay framework phù hợp nhất với trường hợp sử dụng của họ.
