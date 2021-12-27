# 1. Khái quát về Micro Frontend (MF)

Micro frontends là một kiến trúc phần mềm mà trong đó, nó sẽ chia ứng dụng theo hướng **vertical domain**.
Tuơng ứng, mỗi phần được xây dựng từ database đến UI và được điều hành bởi một nhóm chuyên dụng.
Các nhóm frontend sẽ tích hợp các phần của mình để tạo ra một website cho người dùng sử dụng.

Lý do chính để sử dụng:
- Tối ưu hóa cho việc phát triển tính năng: 
  - Một nhóm sẽ bao gồm tất cả các kỹ năng cần thiết để phát triển một tính năng. 
  - Không cần phối hợp giữa các nhóm frontend và backend riêng biệt.
- Dễ dàng nâng cấp FE: Các nhóm có thể quyết định cập nhật hoặc chuyển đổi công nghệ FE của họ một cách độc lập.
- Tăng sự hiểu rõ về business domain: Mỗi nhóm sẽ thực hiện các tính năng trực tiếp cho khách hàng. 
- Dễ dàng hơn cho dev mới khi tìm hiểu các app nhỏ hơn thay vì hiểu monolith với cả ngàn dòng code.

![image](https://user-images.githubusercontent.com/30824675/147120990-e91bdf52-a9bc-4185-910a-2cb71de8ce91.png)

## 1.1 Nhóm và hệ thống
Mỗi hệ thống là tự trị, có nghĩa là nó có thể hoạt động ngay cả khi các hệ thống lân cận gặp sự cố. Mội hệ thống sẽ có cơ sở dữ liệu riêng biệt.

### 1.1.1 Nhiệm vụ của nhóm
- Một hệ thống được sở hữu bởi một nhóm. 
- Mỗi nhóm có lĩnh vực chuyên môn của mình để cung cấp giá trị cho khách hàng. 
- Mỗi nhóm phải có tên mô tả và nhiệm vụ tập trung vào người dùng rõ ràng. 

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

Mỗi nhóm có thể dùng HTML, CSS và JS cần thiết cho một tính năng nhất định. Ngoài ra, để dễ dàng hơn thì họ có thể sử dụng các thư viện hay framework có sẵn như React, Angular, Vue,... Mỗi nhóm được tự do lựa chọn thư viện hay framework phù hợp nhất với trường hợp sử dụng của họ.

Và chúng ta có thể chia frontend thành 2 loại.
- *Theo Page*:
  - Mỗi nhóm có thể xây dựng các trang của riêng họ và làm cho các trang có thể truy cập được thông qua một public domain.
  - Chúng ta có thể kết nối tới các trang này thông qua các liên kết (links) để người dùng có thể điều hướng chúng.
  - Tuy nhiên, mỗi nhoóm phải implement giống nhau vì thông thường các phần từ xuất hiện trên nhiều trang (header, footer).
- *Theo Fragment*: 
  - Khắc phục các nhược điểm khi chia theo page.
  - Một nhóm có thể quyết định bao gồm chức năng từ một nhóm khác bằng cách thêm nó vào vị trí nào đó trên trang.

![image](https://user-images.githubusercontent.com/30824675/147398088-a4c55060-5420-4c06-926a-23c805081d14.png)

## 1.3 Tích hợp Frontend

Là một kĩ thuật để kết hợp UI của các nhóm (pages và fragments) thành một ứng dụng nhất quán cho end-user.

Gồm 3 loại kĩ thuật:
- Định tuyến (Routing) và chuyển trang (Page Transitions): chuyển từ trang thuộc sở hữu của Nhóm A đến trang thuộc sở hữu của Nhóm B
  - Sử dụng một liên kết HTML (reload page)
  - Sử dụng một ứng dụng shell được chia sẻ hoặc sử dụng meta-framework như single-spa (điêu hướng phía browser).
- Thành phần (Composition): lấy các fragments và đặt chúng vào đúng vị trí.
  - Server-side composition: SSI, ESI, Tailor or Podium
  - Client-side composition: iframes, Ajax, or Web Components
- Giao tiếp (Communication): 
  - Tương tác sự kiện qua lại giữa các fragments - fragments hoặc fragments - pages
  - Ví dụ: Mini Basket nên được cập nhật lại sau khi click nút mua.

![image](https://user-images.githubusercontent.com/30824675/147398992-f7eb7e60-b5c5-4a89-be65-8e0dfb607013.png)

## 1.4 Shared topics

Trước khi bắt đầu làm việc với Micro Frontends, để chắc chắn có kết quả tốt và tránh làm việc dư thừa thì nên áp dụng shared topics:
- Web Performance: Mỗi page được tập hợp từ nhiều fragment bởi nhiều nhóm => phải theo dõi performance ngay từ đầu. Điều đó giúp tránh tải xuống framework hay tài nguyên dư thừa.
- Design System: Giúp nhất quán giao diện cho người dùng => tạo common components.
- Sharing Knowledge: Giúp bạn tập trung vào nhiệm vụ của nhóm => chọn một giải pháp để chia sẻ hoặc ít nhất là chấp nhận giải pháp từ các nhóm khác. (Tạo cơ chế quản lý lỗi)

![image](https://user-images.githubusercontent.com/30824675/147435536-b831a1a8-a7f5-4f31-bc9c-7c15f7278399.png)







