# Mini guideline - nhóm: ______  |  người gán: Lưu Quang Hùng  |  ngày: 16/9/2026

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật nhóm bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài | Nếu hông bị che bởi quần áo dài nhưng vẫn nằm trong khung, đặt chấm ở vị trí ước lượng theo giải phẫu và để `v = 1`; không xoá khớp. | Hông là điểm ẩn định của thân, nên ước lượng tốt hơn là bỏ trống khi người còn nằm trong ảnh. |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | Nếu mép tai còn thấy hoặc có thể suy ra vị trí từ hình dáng đầu, đặt chấm ở vị trí ước lượng và để `v = 1`; không dùng `h`. | Tai là dáng điển hình dễ bị che, và giữ lại khớp giúp model giữ đúng hình dạng đầu và tỷ lệ thân. |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Mọi khớp còn trong khung thì vẫn đặt chấm và gắn `v = 1`; các điểm ngoài khung thì không đặt, `v = 0`. | Quy tắc lớp là rõ: còn trong khung = ước lượng + `v = 1`; ra ngoài khung = không chấm + `v = 0`. |
| Cổ tay nằm sau tay lái / sau thân mình | Nếu cổ tay còn trong khung nhưng bị che, đặt chấm ước lượng ở đầu tay và cho `v = 1`; không xoá khớp. | Cổ tay là vị trí quan trọng để phân biệt tay trái-phải và độ dài cánh tay, nên không nên mất thông tin khi bị che nhẹ. |
| Hai người chồng lên nhau | Gán theo người rõ nhất ở mặt trước; nếu điểm thuộc người phía sau không phân biệt rõ, chỉ đặt khi nó còn rõ và thuộc cơ thể được xác định; không lẫn người. | Nhầm người là lỗi nguy hiểm nhất vì model học sai trái-phải và hình dạng thân. |
| Người nhỏ đến mức nào thì không gán nữa | Nếu người quá nhỏ đến mức không xác định được điểm nào hoặc không phân biệt được trái/phải, thì coi là không đủ thông tin để gán; trong bộ này, mọi người đều đủ lớn để gán. | Duy trì tiêu chí “có thể xác định đủ 17 điểm và trái/phải” để tránh gán bừa nhưng vẫn không bỏ sót người hợp lệ. |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_02.jpg`, người thứ `1`, khớp `left_ear,right_ear,left_eye,right_eye,nose`

- Mơ hồ ở chỗ nào: Chủ thể quay mặt về  phía sau, không chắc điểm tai , mắt , mũi thật nằm ở đâu.
- Bạn quyết thế nào: Đặt chấm ở vị trí ước lượng sát vị trí thật, còn trong khung, và gắn `v = 1`.
- Vì sao: Nếu tai , mắt , mũi vẫn nằm trong khung mà chỉ bị che, tiến hành ước lượng là đúng luật; xoá điểm sẽ làm mất thông tin về hình dạng đầu.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model sẽ học sai vị trí đầu .

### Ca 2 - ảnh `train_08.jpg`, người thứ `1`, khớp `left_hip,left_knee,left_ankle`

- Mơ hồ ở chỗ nào: Phần thân dưới trái bị che bởi xe và không có đường viền rõ, rất dễ gán lệch lên xuống.
- Bạn quyết thế nào: Đặt chấm ước lượng theo giải phẫu hông và để `v = 1`, không xoá vì khớp vẫn còn trong khung.
- Vì sao: Hông là tiêu điểm để xác định thân và cân bằng cơ thể; nếu bỏ đi, đường thân sẽ bị méo và không thể đánh giá chân/thắt lưng đủ chính xác.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model sẽ hiểu cơ thể bị lệch hoặc gập sai, dễ gây ra lỗi chiều cao thân, nhầm tỷ lệ hông và chân.

### Ca 3 - ảnh `train_13.jpg`, người thứ `2,3`, khớp `all`

- Mơ hồ ở chỗ nào: Hình ảnh mờ không nhìn rõ toàn bộ cơ thể.
- Bạn quyết thế nào: Đặt chấm ước lượng theo hướng cơ thể, giữ `v = 1` vì khớp còn trong khung và có thể suy ra.
- Vì sao: Không gán khớp sẽ làm thiếu vật thể
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model sẽ học sai.
## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `left_ear` (bạn `62%` / họ `48%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**: guideline chưa rõ ở phần tai và hông bị che bởi quần áo hoặc mũ, nên cần thống nhất thêm luật trước khi gán tiếp.
- Luật mới bổ sung vào mục 2 sau khi thống nhất: Nếu khớp còn trong khung nhưng bị che bởi tóc, mũ, quần áo, tay lái hoặc thân mình, vẫn đặt chấm ở vị trí ước lượng và gắn `v = 1`; chỉ khi khớp thật sự ra ngoài mép ảnh mới không đặt chấm và dùng `v = 0`.
