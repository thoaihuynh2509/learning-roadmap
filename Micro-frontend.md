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
