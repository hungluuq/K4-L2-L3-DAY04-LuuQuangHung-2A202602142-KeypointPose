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
