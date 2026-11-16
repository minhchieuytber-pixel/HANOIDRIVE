# Hanoi Drive 3D — prototype v0.2

Game lái xe 3D chạy trực tiếp trên trình duyệt, xây dựng bằng Three.js, JavaScript và Vite. Bản 0.2 tập trung nâng cấp mạng lưới đường, giao lộ, cảnh quan và cơ chế LOD/chunk để làm nền cho thành phố mở rộng lấy cảm hứng từ Hà Nội.

## Chạy trên máy

Yêu cầu Node.js 20.19+ hoặc 22.12+.

```bash
npm install
npm run dev
```

Mở địa chỉ Local mà Vite hiển thị trong Terminal.

## Kiểm tra và build

```bash
npm run check
npm run build
npm run preview
```

`npm run check` kiểm tra cú pháp JavaScript. `npm run build` tạo thư mục `dist` để triển khai.

## Đưa lên GitHub Pages

1. Tạo repository trên GitHub.
2. Giải nén và đưa toàn bộ nội dung thư mục dự án vào repository.
3. Push mã nguồn lên nhánh `main`.
4. Vào **Settings → Pages** và chọn **GitHub Actions** ở mục Build and deployment.
5. Workflow `.github/workflows/deploy.yml` sẽ cài thư viện, build và triển khai trang.

`vite.config.js` đã đặt `base: './'` để đường dẫn tài nguyên hoạt động trên GitHub Pages project site.

## Điều khiển

- WASD hoặc phím mũi tên: tiến, lùi và đánh lái.
- Điện thoại: chạm giữ cụm nút ở góc trái dưới.
- Kéo ngang trên màn hình để xoay camera.

## Những gì được nâng cấp trong v0.2

- Đường trục chính rộng hơn đường nội bộ; vỉa hè và bó vỉa đi theo từng tuyến.
- Vạch làn, vạch qua đường tại các giao lộ được gom bằng `InstancedMesh` thay vì tạo hàng trăm mesh rời.
- Cây xanh, cột đèn và một số biển chỉ dẫn dùng instancing.
- Có đèn tín hiệu chu kỳ đỏ – vàng – xanh tại khu vực trung tâm.
- Bố trí lại nhà trong lòng ô phố, tránh đặt trực tiếp lên lòng đường và các khu vực dành cho địa danh.
- LOD theo chunk: chỉ chunk chứa xe được bổ sung cửa sổ mặt tiền và chi tiết mái; các chunk lân cận dùng mô hình khối nhẹ hơn.
- Chunk 500 × 500 m, tải vùng 3 × 3 chunk quanh xe (tối đa 1.5 × 1.5 km đang hiển thị) và giải phóng chunk ở xa.
- Bản đồ procedural có biên khoảng 6 × 6 km; lõi đô thị quanh điểm xuất phát có thể mở rộng khoảng 3 × 3 km, còn vùng ngoài được sinh theo yêu cầu khi xe di chuyển.
- Mặt đường, vỉa hè và bó vỉa cũng dùng `InstancedMesh`, giảm mạnh số draw calls so với việc tạo mesh riêng cho từng đoạn.
- Giới hạn tốc độ render theo pixel ratio, tắt bóng thời gian thực và giới hạn xe trong biên bản đồ.

## Các khu vực cách điệu

- Hoàn Kiếm: hồ nhỏ, đảo và Tháp Rùa cách điệu.
- Tây Hồ: mặt hồ lớn với các đoạn cầu tại những tuyến đường cắt qua hồ.
- Ba Đình: quảng trường và công trình khối thấp-poly.
- Văn Miếu: quần thể kiến trúc văn hóa cách điệu.
- Khu đô thị mới và công viên.

Các mô hình là hình khối tự dựng cho game, không phải bản sao chính xác địa lý hoặc mô hình 3D của địa danh thật.

## Hiệu năng và giới hạn

- Mỗi lần chỉ giữ tối đa 9 chunk lân cận; chunk xa được gỡ khỏi scene và giải phóng geometry.
- `InstancedMesh` giảm draw calls cho nhà, cây, vạch đường và đèn.
- Không bật shadow map; pixel ratio tối đa 1.25 để ưu tiên thiết bị di động.
- Chưa có va chạm xe – công trình, giao thông AI, người đi bộ, nhiệm vụ, minimap, âm thanh, mô hình xe chi tiết hoặc dữ liệu GIS thật.
- Đèn tín hiệu là hiệu ứng chu kỳ trình diễn, chưa điều khiển phương tiện AI.
- Chưa xác nhận FPS thực tế trên iPhone/Android; cần thử trên thiết bị thật và điều chỉnh mật độ cảnh theo kết quả.

## Dữ liệu và giấy phép

Bản hiện tại không tải dữ liệu Google Maps, không dùng dữ liệu OpenStreetMap và không chứa mô hình 3D bên thứ ba. Nếu bổ sung OpenStreetMap sau này, cần tuân thủ ODbL và hiển thị ghi công phù hợp; mọi mô hình/texture bên ngoài cần giấy phép sử dụng rõ ràng.
