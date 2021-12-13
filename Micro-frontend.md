# I. Khái niệm cơ bản?
## 1. Micro frontend là gì?
- Micro-Frontend là một phần của trang web (không phải toàn bộ trang).
- Trong kiến trúc micro-frontend, một trange host/container có thể chứa một hoặc nhiều micro-frontend app.
- Trang host/container cũng có thể chia sẻ một số component Micro-Frontend của riêng nó.
- Trong đó, kiến trúc gồm 3 phần chính:
  - Micro-Frontends app.
  - Host/container
  - Micro-Frontends framework: __Webpack 5 Module Federation Plugin__
 
![Screenshot from 2021-12-10 22-06-11](https://user-images.githubusercontent.com/30824675/145595519-6de656ab-afa1-4d00-86e9-038895ed6d69.png)


## 2. Tại sao dùng Micro frontend?
Micro-frontends được giới thiệu để giải quyết các vấn đề của SPA. Nó rất khó để mở rộng quy mô, sửa đổi hoặc thậm chí đào tạo các dev mới.
- **Team Scalability:** Có thể chia công việc và scale hệ thống bởi nhiều team. 
- **Single responsibility:**
  - Cho phép mỗi team sẽ build các component của riêng họ.
  - Ví dụ:
    - Team host có thể tập trung 100% vào việc tạo host page.
    - Mỗi Micro-Frontend team có thể tập trung 100% vào các chức năng ứng dụng của họ.
- **Reusability:** 
  - Có khả năng sử dụng code ở nhiểu nơi. 
  - Ví dụ: Một component sẽ được build và deploy => team khác có thể tái sử dụng.- **Technology agnosticism: **
  - Kiến trúc Micro Frontends không phụ thuộc vào công nghệ. 
  - Bạn có thể sử dụng components từ React, Vue, Angular và không cần phải lo lắng về deploying hoặc bulding chúng.
- **Learning Curve:** Dễ dàng hơn cho dev mới khi tìm hiểu các app nhỏ hơn thay vì hiểu monolith với cả ngàn dòng code.
- **Domain-Driven Architecture:** Một trong những lý do chính đằng sau việc phát minh ra cả Micro-Frontends và Microservices là cho phép thực hiện **vertical domain**
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
