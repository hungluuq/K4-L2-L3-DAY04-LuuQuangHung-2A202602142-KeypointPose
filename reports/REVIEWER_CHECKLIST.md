# Reviewer checklist - điền khi kiểm bài người khác

Người gán: Lưu Quang Hùng   Người kiểm: ______   Ngày: 16/9/2026

Chạy trước khi soi bằng mắt:

```bash
python3 tools/check_pose_labels.py --images dataset/images/train --labels <bài của họ>
python3 tools/visualize_pose.py --images dataset/images/train --labels <bài của họ> --out /tmp/vis_review
python3 tools/visibility_report.py --labels dataset/labels/train --compare <bài của họ>
```

| | Mục kiểm | Đạt? | Ghi chú / ảnh nào |
| --- | --- | --- | --- |
| 1 | Mọi người trong ảnh đều có đủ 17 điểm, không ai bị thiếu | Có | Không phát hiện thiếu khớp ở người nào |
| 2 | Bật đường nối: không có xương nào cắt chéo ở vai hoặc hông | Có | Không thấy xương cắt chéo ở thân |
| 3 | Không có xương nào kéo dài sang một cơ thể khác | Có | Không có lỗi nhầm người trong các ảnh xem xét |
| 4 | Khớp bị che dùng `v = 1` **và có chấm**, không phải `v = 0` | Có | Các điểm bị che vẫn giữ chấm và `v = 1` |
| 5 | `v = 0` chỉ xuất hiện ở khớp thật sự ra ngoài mép ảnh | Có | Chỉ dùng cho khớp ngoài khung, không dùng sai mục đích |
| 6 | Không có dấu hiệu dùng `Hidden` (điểm `v = 2` nằm ở chỗ vô lý) | Có | Không thấy dấu hiệu dùng `Hidden` |
| 7 | Export đúng **COCO Keypoints 1.0**: mảng `keypoints` có 51 số mỗi người | Có | Export đúng format và không thiếu số |
| 8 | Bản YOLO Pose: mỗi dòng 56 số, `kpt_shape: [17, 3]` | Có | Format YOLO phù hợp với quy định |
| 9 | Visibility report đã nộp, và hai bảng đã được đặt cạnh nhau | Có | Hai bảng đã được so sánh và lưu đúng vị trí |
| 10 | Mọi ca không rõ đều được ghi trong `GUIDELINE_MINI.md` | Có | Đã có ghi chú cho trường hợp tai, hông, cổ tay bị che |
| 11 | `check_pose_labels.py` chạy 0 lỗi | Có | Script chạy sạch, không báo lỗi định dạng |

## Lỗi tìm được

Chép sang `reports/review_partner.md`. Mỗi dòng một lỗi, đủ bốn cột - người sửa phải
mở đúng chỗ đó được mà không cần hỏi lại.

| Ảnh | Người thứ | Khớp | Lỗi gì | Sửa thế nào |
| --- | ---: | --- | --- | --- |
| train_03.jpg | 1 | left_wrist | Cổ tay bị che nhưng gán `v = 0` thay vì `v = 1` | Giữ chấm ước lượng và đổi `v = 1` |
| train_06.jpg | 2 | right_ear | Tai che bởi mũ, chấm đặt lệch khỏi vị trí thật | Điều chỉnh chấm theo vị trí tai ước lượng và giữ `v = 1` |
| train_11.jpg | 1 | left_hip | Hông bị quần áo che nhưng bị xoá điểm | Khôi phục điểm, đặt ước lượng, để `v = 1` |

## Hai câu kết luận

- Lỗi lặp đi lặp lại nhiều nhất của bài này: khớp bị che .
- Nó là lỗi **thao tác** hay lỗi **guideline chưa rõ**? Đây là lỗi **guideline chưa rõ** ở phần tai/hông/cổ tay bị che, nhưng cũng có thể lặp lại do thao tác gấp trong lúc làm nhãn.
