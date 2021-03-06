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

# 2. Các vấn đề khi sử dụng Micro Frontends?
## 2.1 Tối ưu hóa việc phát triển tính năng
- Tình huống: Giả sử bộ phận marketing có ý tưởng tạo ra một banner mới. Đầu tiên, họ sẽ nói với team UI để thiết kế. Sau đó, team UI mới đưa cho team frontend để thảo luận. Một buổi họp sẽ được sắp xếp and đặc tả yêu cầu sẽ được viết. Mỗi team sẽ lên kế hoạch đê làm nó trong sprint tiếp theo => tốn rất nhiều thời gian giữa các team.
- Nhưng với Micro Frontends, tất cả mọi người tham gia tạo tính năng mới chỉ ở trong 1 team. Số lượng công việc giống nhau nhưng sẽ tiết kiệm nhiều thời gian hơn:    - Có thể giao tiếp trực tiếp (ko cần meeting). 
   - Không ảnh hưởng tới những team khác.

![image](https://user-images.githubusercontent.com/30824675/147456321-a516d211-c9bf-45f6-8166-62c5d0510417.png)

## 2.2 Khắc phục bất lợi Frontend Monolithic
- Build và deploy độc lập.
- Dễ dàng refactor, tìm kiếm bug vì codebase nhỏ.
- Dễ dàng hiểu rõ business domain vì mỗi team chỉ nắm một vài business domain nhất định

## 2.3 Không làm ảnh hưởng đến code cũ
![image](https://user-images.githubusercontent.com/30824675/147488645-229444ac-ca95-4654-b8a1-d1bd0995f48a.png)

## 2.4 Tính tự chủ
Là một trong những lợi ích quan trọng của microservices và cũng như là micro frontends. Nó rất hữu ích khi các nhóm được tự quyết định những thay đổi quan trọng hơn.

- Tính độc lập: Pages và Fragments là độc lập. Do đó, mỗi nhóm có thể deploy tính năng mới là một fragments mà không cần thảo luận với các nhóm khác.
- Chi phí kĩ thuật thấp: (Tìm hiểu sau).
- Hạn chế chia sẻ nhiều làm ảnh hưởng tới thời gian phát triển tính năng.

## 2.5 Nhược điểm

Như đã nêu trước đó, Micro Frontends giúp các nhóm tự quản mọi thứ mà họ cần. Từ đó tạo ra các tính năng có ý nghĩa cho khách hàng. Quyền tự chủ này rất mạnh mẽ nhưng gặp phải một số bất cập:

### 2.5.1 Dư thừa (Redundancy)
Trước đây, mọi người được yêu cầu phải giảm thiểu sự dư thừa trong code của mình => tăng hiệu quả và tính nhất quán.

Tuy nhiên, khi làm việc với Micro Frontends, mỗi nhóm cần phải setup project, CI/CD,... Điều đó dẫn tới việc có thể trùng lập mã code giữa các team

Ví dụ:
- Khi một lỗi xuất hiện trong một thư viện phổ biến (scroll table trong antd) thì tất cả các nhóm nếu sử dụng thư viện này sẽ phải bắt buộc sửa lỗi đó giống nhau.
- Khi một nhóm làm CI/CD nhanh hơn các nhóm khác => Nhóm này phải chia sẻ lại kiến thức cho họ. Và sau đó, các nhóm khác này sẽ phải tối ưu hóa giống như vậy.

### 2.5.2 Không nhất quán (Consistency)
Tất cả các nhóm phải có cơ sở dữ liệu của riêng họ nhưng đôi khi một nhóm cần dữ liệu mà nhóm khác sở hữu.

Một giải pháp điển hình cho việc này là sao chép dữ liệu bằng cách sử dụng event bus hoặc feed system. Tuy nhiên, nó có thể gây mất thời gian cũng như dộ trễ.

Ví dụ: Một sản phẩm được khuyến mại có giảm giá trên trang chủ nhưng có thể không có chiết khấu trong giỏ hàng (vì độ trễ khi sync dữ liệu giữa các team).

### 2.5.3 Không đồng nhất (Heterogeneity)
Được lựa chọn công nghệ là một trong những lợi thế quan trọng nhất mà Micro Frontends giới thiệu. Tuy nhiên, việc này khiến các nhà phát triển khó chuyển đổi từ nhóm này sang nhóm khác hoặc thậm chí trao đổi các phương pháp hay nhất.

Mặc dù vậy, không nhất thiết sử dụng khác công nghệ vì lợi ích cốt lõi của việc nâng cấp phiên bản tự động và ít chi phí giao tiếp hơn vẫn còn.

# 3. Khi nào nên và không nên dùng Micro Frontends?
## 3.1 Nên dùng
- Team size từ vừa đến lớn: Recommend mỗi team từ 5-10 thành viên.
- Tốt hơn khi xây dựng trên Web
- Quan trọng năng suất hơn là sự phức tạp trong setup hay chi phí vận hành.

## 3.2 Không nên dùng
- Có ít nhà phát triển và việc giao tiếp không thành vấn đề.
- Có business domain có khả năng chia theo vertial system vì nếu nhiệm vụ nhóm không rõ ràng hoặc chồng chéo sẽ dẫn đến sự không chắc chắn và các cuộc thảo luận kéo dài.
- Trong môi trường start-up: 
  - Mọi thứ đều hoạt động tốt cho đến thời điểm mà công ty cần để thay đổi mô hình kinh doanh của mình. 
  - Giải pháp: có thể tổ chức lại các nhóm và phần mềm liên quan, nhưng nó tạo ra nhiều xung đột và công việc bổ sung.
- Cần tạo nhiều ứng dụng và giao diện người dùng gốc khác nhau để chạy trên mọi thiết bị.

# 4. Chuyển trang bởi links
![image](https://user-images.githubusercontent.com/30824675/147804284-f556faa1-1bcc-4641-9236-fd2957d75c28.png)

## 4.1 Ưu điểm
- Sự kết nối giữa các ứng dụng thấp:
  - Nhóm chỉ cần triển khai mẫu URL của nhóm khác để liên kết với họ.
  - Nhóm không phải quan tâm đến ngôn ngữ lập trình, frameworks, styling, deployment hay cách hoisting nhóm khác sử dụng.
- Độ bền cao: 
  - Khi một ứng dụng gặp sự cố sẽ không ảnh hưởng đến page hiện tại và không ảnh hưởng đến hệ thống của nhóm khác.

## 4.2 Nhược điểm
Không tối ưu theo quan điểm người dùng vì không có cách nào kết hợp dữ liệu từ hai nhóm khác nhau vào một chế độ xem

## 4.3 Khi nào sử dụng?
Khi bạn đang xây dựng một trang web hơi phức tạp, việc tích hợp chỉ dựa vào các liên kết là không đủ trong hầu hết các trường hợp.

Thường thì bạn cần nhúng thông tin từ một nhóm khác nhờ vào các kĩ thuật tích hợp khác.

# 5. Composition via iframe
![Screenshot from 2021-12-31 17-38-24](https://user-images.githubusercontent.com/30824675/147818782-d275114e-64e1-4bab-8ffa-898e249fdb09.png)

```
<div id="app-shell">
  <iframe src="https://squad-fragment.com/header"></iframe>
  <iframe src="https://squad-inside.com"></iframe>  
</div>
```

## 5.1 Ưu điểm
- Dễ để thực hiện.
- Cô lập hoàn toàn giữa các micro frontends. (HTML riêng biệt, CSS, JS, hình ảnh,…)
- Hoạt động tốt trên tất cả các trình duyệt.
- Mang một số tính năng bảo mật tự vệ cho từng micro frontends.

## 5.2 Nhược điểm
- Không thể đặt tự động chiều cao của Iframe (nhược điểm lớn nhất).
- Giảm hiệu suất vì mỗi iframe đều tạo ra một context browser mới => tăng bộ nhớ và CPU.
- Không tốt cho khả năng tiếp cận (cho người khuyết tật) và cho SEO.

## 5.3 Khi nào sử dụng
- Biết được kích thước của nội dung trong iframe (tĩnh) và không cần SEO.
- Ứng dụng nội bộ của công ty vì nó dễ dàng để bắt đầu với kĩ thuật Micro Frontends.

# 6. Composition via Ajax và server-side routing
![Screenshot from 2022-01-02 00-15-59](https://user-images.githubusercontent.com/30824675/147856177-cb7a77c2-41b0-4bf4-a262-d0aa779b0d61.png)

Bạn có thể tích hợp nội dung của nhiều pages vào một <document /> thông qua việc tải bởi Ajax. So sánh với Iframe thì tích hợp bởi Ajax sẽ tốt hơn cho khả năng tiếp cận (cho người khuyết tật), SEO hay hiệu suất.

Tuy nhiên, vì nó đặt các fragments vào trong cùng <document /> nên có khả năng xảy ra xung đột CSS. Để giải quyết vấn đề này, ta có thể sử dụng prefix cho classname của CSS.

Ví dụ:

Trong /team-decide/static/page.js

```
const element = document.querySelector(".decide_recos");
const url = element.getAttribute("data-fragment");

window.fetch(url)
  .then((res) => res.text())
  .then(html => element.innerHTML = html);

```

Trong /team-decide/view.js
```
<body>
  <aside
    class="decide_recos"
    data-fragment="http://localhost:3002/fragment/recommendations/porsche"
  >
    <a href="http://localhost:3002/recommendations/porsche">Show Recommendations</a>
  </aside>  
  <script src="/static/page.js" async></script>
</body>  
```

![Screenshot from 2022-01-02 00-17-47](https://user-images.githubusercontent.com/30824675/147856207-b072ecff-f6b2-418e-9d6d-83a79fcfcb5e.png)

## 6.1 Ưu điểm
- Dễ dàng triển khai.
- Giống như web bình thường: chiều cao của các fragment được tự động điều chỉnh.
- Tốt cho SEO, accessibility.
- Dễ dàng cung cấp một dự phòng đáng tin cậy trong trường hợp JavaScript bị lỗi hoặc chưa được thực thi.
``` 
    <h-include src="">
      <button>Show detail</button>
    </h-include>
```
- Linh hoạt trong việc xử lý lỗi với **new Promise().catch()**

## 6.2 Nhược điểm
- Asynchronous loading
  - Có thể nhận thấy rằng trang web nhảy hoặc lắc lư một chút khi tải do tải không đồng bộ.
  - Tải nội dung không đồng bộ luôn đi kèm với sự đánh đổi là nội dung xuất hiện với độ trễ (Ngoại trừ các fragments nằm sâu hơn bên dưới trang và bên ngoài chế độ xem).
- Không cô lập: Xung đột CSS
- Khó khăn khi tương tác với các phần tử thông qua JS
  - Khi trang bên ngoài cập nhật một fragment bằng cách thay thế nó bằng đánh dấu mới fragment (được tìm nạp từ máy chủ), 
  - Sau đó, trình xử lý sự kiện này cần được xóa và thêm lại vào fragment mới này.

## 6.3 Khi nào sử dụng?
- Muốn ứng dụng các lợi ích của server-side render.
- Các Fragment **không** chứa nhiều tương tác và **không có** trạng thái cục bộ. Nguyên nhân là việc tải và tải lại sẽ gây ra cảm giác chậm trễ do độ trễ của mạng

# 6.4. Server-side routing via Nginx


Tình huống: Khách hàng mong đợi rằng domain trong thanh địa chỉ trình duyệt sẽ không thay đổi sau mỗi lần thao tác sự kiện. 
![Screenshot from 2022-01-02 16-51-15](https://user-images.githubusercontent.com/30824675/147872259-69fddabf-b5fb-46d9-880a-718ad18ec01f.png)

Giải pháp: 
- Bạn có thể định tuyến nội dung của nhiều ứng dụng thông qua một frontend proxy (Nginx).
- Proxy này cung cấp tất cả nội dung thông qua một domain thống nhất. 
- Ngoài ra, kết hợp với việc sử dụng prefix (tên nhóm) trong đường dẫn URL là một cách tuyệt vời để giúp gỡ lỗi và định tuyến dễ dàng hơn.

Ưu điểm:
- Tránh CORS
- Cho phép chia sẻ dữ liệu (Vd: login by cookie)
- Hiệu suất tốt hơn (chỉ một lần tra cứu DNS, SSL handshake, …)

Ai là người quản lý:
- Về mặt truyền thống thì team platform.
- Tuy nhiên, việc này sẽ xảy ra một vấn đề là khi máy chủ web không hoạt động, khách hàng không nhìn thấy gì, ngay cả khi các ứng dụng đằng sau nó vẫn đang chạy.

![Screenshot from 2022-01-02 16-15-33](https://user-images.githubusercontent.com/30824675/147871459-fba7dcf0-d75f-49d7-9822-cf3f92af67f1.png)




