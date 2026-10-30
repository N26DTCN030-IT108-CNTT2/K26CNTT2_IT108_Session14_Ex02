# K26CNTT2_IT108_Session14_Ex02
# 🛡️ Báo cáo Bài tập: Ngăn chặn rò rỉ dữ liệu do chia sẻ sai quyền
**Môn học:** Nhập Môn Công Nghệ Thông Tin (Buổi 15: Không gian cộng tác đám mây)  
**Học viên:** Lê Hồ Thanh Thảo (N26DTCN030)

---

## 1. Mục tiêu
- Phân biệt chính xác 3 mức quyền trên không gian đám mây: `Viewer`, `Commenter`, `Editor`.
- Thực hành quy tắc chia sẻ an toàn để ngăn chặn tuyệt đối tình trạng rò rỉ dữ liệu (`Data Leak`).

---

## 2. Bối cảnh & Vấn đề
> **Tình huống:** An chia sẻ tài liệu chứa danh sách số điện thoại khách hàng của Startup cho một cộng tác viên bên ngoài. Do muốn tiện lợi, An đã chọn chế độ *"Anyone with the link"* kết hợp với quyền `Editor` để đối tác dễ dàng chỉnh sửa. 
> 
> **Hậu quả:** Đường dẫn bị phát tán công khai lên mạng xã hội, dẫn đến việc kẻ xấu truy cập và xóa sạch toàn bộ dữ liệu khách hàng.

---

## 3. Yêu cầu đầu ra

### Phần 1: Phân tích nguyên nhân vi phạm "Quy tắc Cờ Đỏ Bảo mật"
Hành động của An đã phạm phải ba sai lầm nghiêm trọng trong quản trị tài nguyên số:

1. **Sử dụng chế độ công khai không kiểm soát (`Anyone with the link`):** Biến một tài liệu nội bộ thành tài liệu công cộng mà không có bất kỳ lớp xác thực danh tính nào.
2. **Cấp quyền tối đa (`Editor`) cho đối tác bên ngoài:** Trao quyền xóa và chỉnh sửa dữ liệu ngang hàng với chủ sở hữu cho một bên thứ ba chưa được kiểm soát độ tin cậy.
3. **Vi phạm nguyên tắc đặc quyền tối thiểu (Principle of Least Privilege):** Cấp quyền vượt quá mức cần thiết chỉ vì sự tiện lợi trước mắt, tạo lỗ hổng chí mạng dẫn đến thảm họa mất dữ liệu (`Data Leak`).

---

### Phần 2: Đề xuất cấu trúc phân quyền chuẩn (Sửa lỗi)

Để khắc phục triệt để rủi ro trên và bảo vệ tài sản dữ liệu của Startup, An cần áp dụng quy trình chuẩn sau:

#### (1) Mức quyền tối ưu cho cộng tác viên:
* Chỉ cấp quyền **`Commenter` (Người nhận xét)** hoặc **`Viewer` (Người xem)** nếu đối tác chỉ cần đọc hoặc góp ý.
* Trong trường hợp bắt buộc phải chỉnh sửa nội dung, phải phân quyền trực tiếp qua **Email cá nhân cụ thể** thay vì dùng liên kết mở.

#### (2) Chế độ chia sẻ an toàn 100%:
* Sử dụng chế độ **`Restricted` (Hạn chế)**: Tài liệu chỉ hiển thị và cho phép truy cập đối với những tài khoản đã được chủ sở hữu thêm vào danh sách cấp phép qua email. Tuyệt đối không sử dụng chế độ *"Anyone with the link"* cho dữ liệu nhạy cảm.

#### (3) Thiết lập bảo mật nâng cao ngăn chặn rò rỉ:
* **Khóa quyền chia sẻ của người chỉnh sửa:** Bật tùy chọn cài đặt nâng cao của chủ sở hữu:  
  > ⚙️ *"Disable editors from changing permissions and sharing"*  
  *(Ngăn chặn người chỉnh sửa tự ý thay đổi quyền hạn hoặc chia sẻ tiếp đường dẫn cho người lạ).*
