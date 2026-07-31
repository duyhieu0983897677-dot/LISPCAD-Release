# VK Quản Lý Khối Lượng — Kho phát hành

Kho này **chỉ chứa bản phát hành**: `version.json` và file cài đặt `.zip`.
Mã nguồn nằm ở kho riêng và không công khai.

Kho phải luôn ở chế độ **public**. Plugin trên máy người dùng đọc
`version.json` bằng một request ẩn danh — kho private sẽ trả về 404 và
toàn bộ cơ chế tự động cập nhật ngừng hoạt động mà không báo lỗi gì.

| File | Vai trò |
|---|---|
| `version.json` | Số phiên bản mới nhất, link tải, SHA256, danh sách thay đổi |
| `VK_QuanLyKhoiLuong_v2.0.zip` | Bộ cài: DLL đã mã hoá, VK_Updater.exe, form mẫu, hướng dẫn |

## Cách plugin dùng kho này

1. Mở bảng điều khiển (`TL`) → plugin đọc `version.json`
2. Nếu `version` lớn hơn phiên bản đang cài → hiện popup báo cập nhật
3. Người dùng bấm tải → plugin tải zip theo `downloadUrl`, **đối chiếu `sha256`**
4. `VK_Updater.exe` đợi AutoCAD đóng rồi giải nén đè lên thư mục cài đặt

Lệnh `VKCAPNHAT` trong AutoCAD kiểm tra thủ công và in rõ lý do nếu lỗi.

## Phát hành bản mới

Đừng sửa tay hai file trong kho này. Chạy script trong kho mã nguồn:

```
.\phathanh.ps1 -PhienBan 2.0.4
```

Script tự tăng số phiên bản trong code, biên dịch, đóng gói, tính lại SHA256
và ghi `version.json`. Sửa tay rất dễ để lệch số phiên bản hoặc lệch hash —
cả hai đều làm bản phát hành câm lặng, không một máy nào nhận được.
