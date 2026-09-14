# Báo cáo — Ngày 2: phát hiện vật thể

**Họ và tên:** Cầm Vũ Ngọc Thạch<br>
**MSSV:** 2A202602067<br>
**Hình thức:** cá nhân<br>
**Mã cặp:** SOLO— ghi `SOLO` nếu làm cá nhân

## 1. Bài độc lập và nguồn dữ liệu

- Mã SHA-256 của ZIP ảnh được cấp:f7d99888f21440fb0374d849
- Bốn mã ảnh:  'drive_088', 'drive_022', 'drive_033', 'drive_038'
- Số vật thể thực tế: 16
- Mã SHA-256 của gói YOLO của bạn:f7d99888f21440fb0374d84962b93213bd8c14e665d093cc8d37f4c61b71ed33
- Mã SHA-256 của gói CVAT gốc của bạn: ef7960a3d98a73d80736a712f9ba4a1ecffeddc43fa41589a910066c5d73f5b4
- Nguồn đối chiếu: bạn cùng cặp hoặc bộ tham chiếu do người hướng dẫn thực hành cấp:day2-teaching-reference
- Mã SHA-256 của gói đối chiếu:c8bbc767d8bb9a29f4ca5abf0c3516e5c2af94c58143a980b0148cfe0b500d2b
- Nếu làm cá nhân, ghi mã lần phát và thời điểm nhận bộ tham chiếu:11h14 nhận bộ tham chiếu trên discord

Giải thích vì sao bài của bạn vẫn độc lập trước khi đối chiếu: output lệch nhiều,label nhiều hơn cần thiết so với bộ tham chiếu


## 2. Quyết định phân lớp

| Ảnh/vật thể | Lớp | Dấu hiệu nhìn thấy | Quy tắc áp dụng |
| --- | --- | --- | --- |
| drive_008 #20  | bus | thấy rõ xe khách dài hai tầng | thân xe khách dài, nhiều cửa sổ hoặc nhiều hàng ghế |

Nêu một ví dụ cho thấy lớp và thuộc tính là hai loại thông tin khác nhau: ví dụ 1 xe car nhưng visibility=occluded (nghĩa là dù bị che, nó vẫn thuộc lớp car, không đổi lớp chỉ vì bị che).



## 3. Tự kiểm tra và sửa nhãn

| Trước khi sửa | Loại lỗi | Cách phát hiện | Sau khi sửa và quy tắc |
| --- | --- | --- | --- |
| drive_022 #35 | phạm vi | So sánh với bộ tham chiếu thấy box của mình bị to và rộng hơn | Đã sửa cho phạm vi nhỏ lại, quy tắc: phạm vi cần phải sát và không nên lấy nhiều phần mặt đường  |

- Số hộp `needs_review` trước và sau khi kiểm:6 và sau khi kiểm còn 0
- Một quyết định chưa đủ bằng chứng và cách bạn xin hỗ trợ:các quyết định need review của mình tất cả đều là các object ở xa và khó xác định, khi so với bộ tham chiếu thì họ không detect những object như thế nên mình đã xóa tất cả các object nay nên là hiện không có quyết định nào chưa đủ bằng chứng, nếu có mình sẽ xin hỗ trợ từ các labcoach.

## 4. Một dòng nhãn YOLO

- Dòng `class x_center y_center width height`:[2, 0.392672, 0.721539, 0.438406, 0.361828]
- Tên lớp và tọa độ điểm ảnh `xyxy`:lớp=2 (bus) | tâm=(0.3927, 0.7215) | kích thước=(0.4384, 0.3618)
- Vì sao dòng đúng định dạng vẫn có thể sai lớp, phạm vi hoặc hình học: vì định dạng chỉ đảm bảo cú pháp hợp lệ hay không , chứ không đảm bảo việc class đúng hay hộp vẽ có sát, hợp lý hay không.



## 5. Huấn luyện và dự đoán thử

- Ba mã ảnh huấn luyện:drive_022, drive_033, drive_038
- Mã ảnh thẩm định:drive_008
- Mô tả một dự đoán trong `detect_result.jpg`:không có dự đoán nào, không ra kết quả lable
- Dự đoán đó gợi ý cần kiểm lại quy tắc hoặc dữ liệu nào?
- Minh chứng nào có thể bác bỏ nhận định của bạn?
- Vì sao kết quả trên bốn ảnh không phải phép đánh giá mô hình dùng thực tế?


## 6. Đối chiếu nhãn

- Số hộp ghép được:47
- IoU trung bình và trung vị:0.77015,0.801528
- Mức đồng thuận lớp:0.723404
- Số hộp phía bạn không ghép được:48
- Số hộp phía đối chiếu không ghép được:3
- Một điểm khác biệt cụ thể:các xe bus bên mình lable thường bị rộng hơn so với tham chiếu, bên tham chiếu không lấy các bộ phận như gương xe 
- Quy tắc hoặc hành động sửa phát sinh: phạm vi vẽ vừa đủ không nên rộng quá
- Vì sao mức đồng thuận cao không chứng minh mọi nhãn đều đúng: độ đồng thuận cao chỉ chứng minh quy tắc của hai bên đã áp dụng giống nhau, không chứng minh cả 2 người cùng trả lời đúng với thực tế.


## 7. Kiểm tra kho GitHub cá nhân

- [x] Có phiếu quy tắc với ba tình huống mơ hồ.
- [x] Có kết quả kiểm hai gói xuất.
- [x] Có thông tin lần huấn luyện và ảnh dự đoán.
- [x] Có tóm tắt, bảng và ảnh phủ của bước đối chiếu.
- [x] Không có gói xuất thô, bộ nhãn tham chiếu hoặc trọng số mô hình.
- [x] Không có dữ liệu VinFast/khách hàng/ảnh cá nhân/mật khẩu/mã truy cập.

Minh chứng mạnh nhất trong bài và câu hỏi còn lại cho Lab Coach: Các quyết định need review ít và đã xử lý xong, không có câu hỏi gì cho lab coach

