# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:** 2A202604119
- **Họ và tên:** Hà Phan Đại Dương
- **SEED** (in ở ô đầu notebook): 9450

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | ☐ |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | ☐ |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | ☐ |

## 2. Kết quả chính
F1 test thường (SUB)  F1 50 case khó  acc 50 case khó
1. BoW + LogReg                    0.824           0.333             0.52
2. BoW + MLP                       0.889           0.378             0.54
3a. Emb + kNN                      1.000           0.724             0.68
3b. Emb + LogReg                   0.974           0.522             0.56
3c. Emb + MLP head                 1.000           0.553             0.58
% đoán ĐÚNG theo nhóm case (càng đậm càng tốt)
 	1. BoW + LogReg	2. BoW + MLP	3a. Emb + kNN	3b. Emb + LogReg	3c. Emb + MLP head
Tưởng spam nhưng không phải	100%	90%	70%	80%	80%
Thao túng / lừa đảo	12%	25%	100%	25%	25%
Spam giọng tự nhiên	10%	0%	40%	10%	10%
Né từ khoá	17%	17%	83%	67%	83%
Prompt injection	67%	83%	83%	100%	100%
Nói về spam	100%	100%	25%	50%	50%
Tin giao dịch hợp lệ	83%	100%	67%	83%	83%
TỔNG (50 case)	52%	54%	68%	56%	58%


## 3. Dự đoán và thực tế

1. dl_relu: Tôi dự đoán F1 sẽ giảm nhẹ, nhưng thực tế F1 = 0.938, không giảm so với MLP có ReLU. Nguyên nhân có thể vì Bag-of-Words đã đủ để phân loại tuyến tính khá tốt, nên ReLU không mang lại nhiều lợi ích.

2. emb_tricky: Tôi dự đoán Encoder sẽ phân loại đúng nhiều hơn BoW, nhưng thực tế cả hai đều đúng 5/6 tin. Nguyên nhân là embedding không phải lúc nào cũng nhận diện tốt spam tinh vi, đặc biệt tin giả dạng thông báo tài khoản hợp lệ.

3. emb_search: Tôi dự đoán kết quả gần nhất là spam và thực tế cả 6 tin gần nhất đều là spam. Tuy nhiên, điểm cosine chỉ khoảng 0.50–0.56, thấp hơn mức tương đồng tôi kỳ vọng. Nguyên nhân là các tin có cùng ý nghĩa quảng cáo trúng thưởng nhưng khác cách diễn đạt và chi tiết.

## 4. Phân tích 50 case khó

BoW + MLP tụt F1 nhiều nhất, từ 0.889 xuống 0.378. Nhóm khó nhất là spam giọng tự nhiên với tỷ lệ đúng 0%, do mô hình phụ thuộc vào từ khóa và không hiểu ý định của tin nhắn. Kết quả cho thấy điểm cao trên test thông thường chưa đảm bảo mô hình hoạt động tốt trước các kiểu spam mới.

## 5. Thử thách cá nhân

*Đề theo SEED của bạn, cách làm, kết quả, giải thích.*

## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*

## 7. AI log và điều đã học

*Mỗi lần dùng AI: hỏi gì, nhận gì, bạn sửa gì. Sau đó 2–3 câu: điều bạn hiểu ra hôm nay mà trước đó chưa hiểu.*
