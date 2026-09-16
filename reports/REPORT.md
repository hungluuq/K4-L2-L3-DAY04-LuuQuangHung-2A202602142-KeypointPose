# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Lưu Quang Hùng   Nhóm: ______   Ngày: 16/9/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 29 |
| v=2 / v=1 / v=0 | 348 / 113 / 32 |
| Thời gian trung bình mỗi ảnh | ### |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. `right_ear` - 38%
2. `left_ear` - 34%
3. `left_wrist` và `right_wrist` - 31% (đồng hạng)

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.9588 | ### |
| OKS@0.50 | 1.0 | ### |
| OKS@0.75 | 1.0 | ### |
| Lỗi `dao_trai_phai` | 0 | ### |
| Lỗi `nham_nguoi` | 1 | ### |
| Lỗi `xoa_khop_bi_che` | 0 | ### |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

Bài của tôi không cần sửa gì

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

Bài của tôi không cần sửa gì

## 3. Kiểm chéo

Bạn cùng nhóm: ______

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| ### | ### | ### | ### | ### |
| ### | ### | ### | ### | ### |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

-

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | 0.8450 | 0.8450 | +0.0000 |
| pose_mAP50-95 | 0.6853 | 0.6908 | +0.0055 |
| pose_precision | 0.9734 | 0.9792 | +0.0058 |
| pose_recall | 0.8462 | 0.8462 | +0.0000 |
| box_mAP50-95 | 0.8119 | 0.8041 | -0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.
1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?
 - `pose_mAP50-95` tăng từ `0.6853` lên `0.6908`, tức `+0.0055` trên 10 ảnh test. Chỉ số không giảm nên không có kết luận rằng 20 ảnh đã làm hỏng kiến thức COCO; mức tăng nhỏ cho thấy dữ liệu pose bổ sung chỉ cải thiện nhẹ khả năng định vị khớp trong các cảnh tương tự tập train.
 
2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?
 - Ở baseline, `box_mAP50-95 - pose_mAP50-95 = 0.8119 - 0.6853 = 0.1266`; sau fine-tune là `0.8041 - 0.6908 = 0.1133`. Model tìm *người* dễ hơn tìm *khớp*, vì xác định vùng hộp tổng quát ổn định hơn việc đặt chính xác 17 điểm, nhất là các điểm bị che hoặc ở tư thế khó.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):
 - `train_10` là một ví dụ lỗi **nhầm người**: kết quả ghi model có 2 người trong khi nhãn có 1 người. `train_03` cũng có hiện tượng tương tự, model 4 người còn nhãn 2 người; đây là lỗi số lượng/định danh người, không chỉ là lệch nhẹ một keypoint.

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?
 - `train_13` có OKS model so với nhãn thấp nhất là `0.593`. Không thể kết luận chỉ từ OKS rằng ai đúng; khi đối chiếu gold, nhãn của tôi ở các người tương ứng đạt `0.907` và `0.9187`, nên có bằng chứng rằng nhãn gần gold hơn và model là phía cần nghi ngờ. Cần xem ảnh visualize để xác nhận từng khớp cụ thể.

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?
 - Không trùng: OKS thấp nhất giữa nhãn của tôi và gold là `train_04` với `0.8895`, còn ảnh model đoán tệ nhất là `train_13` với `0.593`. Vì vậy chưa có bằng chứng rằng cùng một ảnh vừa khó cho người gán vừa khó cho model; hai kết quả đang phản ánh hai loại bất đồng khác nhau.

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

Trong ảnh `train_01.jpg`, người thứ 2, tôi chọn khớp `right_ankle` và đặt `v=0`.
Phần chân của người này bị cắt ở mép dưới ảnh, không còn thấy mắt cá chân và không thể suy ra một vị trí nằm trong khung từ phần chân còn lại.
Vì khớp đã ở ngoài khung nên tôi không đặt chấm tại mép ảnh; `v=1` chỉ dùng khi khớp còn trong ảnh nhưng bị che và có thể ước lượng vị trí.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->
