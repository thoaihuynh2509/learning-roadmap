# I. Khái niệm cơ bản?
## 1. Micro frontend là gì?
- MF là một phần của trang web (không phải toàn bộ trang).
- Trong kiến trúc MF, một trange host/container có thể chứa một hoặc nhiều MF app.
- Trang host/container cũng có thể chia sẻ một số component MF của riêng nó.
- Trong đó, kiến trúc gồm 3 phần chính:
  - MF app.
  - Host/container
  - MF framework: __Webpack 5 Module Federation Plugin__
 
![Screenshot from 2021-12-10 22-06-11](https://user-images.githubusercontent.com/30824675/145595519-6de656ab-afa1-4d00-86e9-038895ed6d69.png)


## 2. Tại sao dùng Micro frontend?
MF được giới thiệu để giải quyết các vấn đề của SPA. Nó rất khó để mở rộng quy mô, sửa đổi hoặc thậm chí đào tạo các dev mới.
- **Team Scalability:** Có thể chia công việc và scale hệ thống bởi nhiều team. 
- **Single responsibility:**
  - Cho phép mỗi team sẽ build các component của riêng họ.
  - Ví dụ:
    - Team host có thể tập trung 100% vào việc tạo host page.
    - Mỗi Micro-Frontend team có thể tập trung 100% vào các chức năng ứng dụng của họ.
- **Reusability:** 
  - Có khả năng sử dụng code ở nhiểu nơi. 
  - Ví dụ: Một component sẽ được build và deploy => team khác có thể tái sử dụng.- **Technology agnosticism: **
  - Kiến trúc MF không phụ thuộc vào công nghệ. 
  - Bạn có thể sử dụng components từ React, Vue, Angular và không cần phải lo lắng về deploying hoặc bulding chúng.
- **Learning Curve:** Dễ dàng hơn cho dev mới khi tìm hiểu các app nhỏ hơn thay vì hiểu monolith với cả ngàn dòng code.
- **Domain-Driven Architecture:** Một trong những lý do chính đằng sau việc phát minh ra cả MF và Microservices là cho phép thực hiện **vertical domain**
  - **Monolith**: là một source code duy nhất (FE + BE), được quản lý bởi toàn bộ thành viên của công ty.
  - **Micro Services**: được quản lý bởi nhiều teams.
    - Giúp công ty mở rộng quy mô phát triển giữa các team và thúc đẩy việc sở hữu backend riêng.
    - Tuy nhiên, Frontend vẫn là một monolith và phụ thuộc vào nhiều teams.
  - **Vertical Domain**: Bằng việc sử dụng Micro Frontends, mỗi domain sẽ sở hữu 1 FE, 1BE riêng biệt.
  
  ![image](https://user-images.githubusercontent.com/30824675/145671757-8bf8a10f-b120-46ec-ab3f-98f3203f1c18.png)

## 3. So sánh các kiến trúc Frontends.

___  | Frontend Monolith | MF with Build-time Integration | MF with runtime integration
------------- | ------------- | ------------ | ---------------
Kiến trúc | Chỉ có 1 repository với tất cả mọi thứ trong đó | Một root app có npm installs mỗi mf app | Một root app load tự động từng ứng dụng web được deploy độc lập.
Setup  | Dễ | Vừa | Khó
Tách repositories  | Không | Không | Có hoặc không
Tách builds  | Không | Có | Có
Tách deployments  | Không | Có | Có
Thuận lợi  | Đơn giản | Mỗi ứng dụng web có thể được xây dựng riêng trước khi xuất bản lên npm | Hỗ trợ deploy và release MF độc lập mà không có bất kỳ dependencies nào. Khả năng mở rộng đáng kinh ngạc.
Bất lợi  | <ul><li>Build chậm bởi vì chứa tất cả code.</li><li>Tất cả các deployments đều gắn liền với nhau</li></ul> | Ứng dụng gốc cần phải install lại, build lại và deploy lại bất cứ khi nào một trong các ứng dụng web thay đổi. | Yêu cầu kiến thức về mối quan hệ giữa app shell (container app) và micro frontends app.



# II. Các cách implement micro frontends?

![image](https://user-images.githubusercontent.com/30824675/145705336-d0438762-d995-4515-bc50-e60ff6f2728c.png)

## 1. Build-Time integration**
Là việc coi các ứng dụng như một package và ứng dụng chính sẽ thêm các ứng dụng con như một thư viện như sau:

```
{
  "name": "@micro-frontends/container",
  "version": "1.0.0",
  "description": "Micro frontends demo",
  "dependencies": {
    "@micro-frontends/products": "^1.2.3",
    "@micro-frontends/checkout": "^4.5.6",
    "@micro-frontends/user-profile": "^7.8.9"
  }
}
```

Tuy nhiên, nó xảy ra nhiều vấn đề:
- Khó sử dụng các công nghệ khác nhau.
- Re-compile (bundle) các app chính và release lại mỗi khi cácapp con có thay đổi.
- Kích thước của package cuối cùng sẽ rất lớn bởi vì nó chứa tất cả dependencies.

## 2. Run-time integration via iframes
## 3. Run-time integration via javascript
## 4. Run-time integration via web components
## 5. Server-Side Composition
- BE sẽ quyết định Micro-Frontend nào sẽ tải. 
- Sử dụng proxy ngược đơn giản bằng Nginx để thực hiện tác vụ này. Tuy nhiên, có nhiều cách triển khai khác.

Ưu điểm:
- Tốt cho SEO.

Nhược điểm:
- Không thể thao tác như SPA.
- Thời gian load đầu tiên lâu vì chúng ta cần đợi tất cả các mf được tạo thành.
- Sự phức tạp trong quá trình phát triển vì cần một cấu hình server phức tạp.

![image](https://user-images.githubusercontent.com/30824675/146583081-89b02f3f-f0e6-47df-88e8-65148a615990.png)

## 6. Client-Side Composition
- Container / Host có thể được build và deploy riêng biệt.
- Mỗi MF có thể được hiển thị như một package riêng biệt mà Container/Host app lưu trữ có thể tìm nạp MF cần thiết.

Ưu điểm:
- Là một tiêu chuẩn web, vì vậy nó có thể được hỗ trợ lâu dài và nhiều bản cập nhật trong tương lai.
- Có thể chọn bất kì thư viện hay frameworks nào để phát triển.

Nhược điểm:
- Không thân thiện cho SEO.
- Thời gian tương tác lâu vì phải load nhiều script.

# III. Chi tiết về micro frontends?
## 1. Micro frontend sẽ kết hợp Micro services như thế nào?
- MF và MS đểu được quản lý bởi các team khác nhau và cả hai sẽ đại diện cho các business domain hoặc các services khác nhau.
- Giống như MS sẽ kiểm soát database của chính nó, mỗi MF sẽ kiểm soát một phần của ứng dụng web của riêng nó.
- Trong đó, **Container App (top-level)** sẽ có trách nhiệm:
  - Định vị các MF có sẵn.
  - Quản lý các common elements như shared header, shared footer,...
  - Quản lý life-circle (mounted, unmounted DOM) của mỗi MF dựa trên routing event.
  - Xử lý các công việc chung như shared data, communication, feature flags, loader component, locale, and UI theme.

![image](https://user-images.githubusercontent.com/30824675/146682712-be71e4cc-10fc-4240-b5e0-31bf13941a10.png)

## 2. 






