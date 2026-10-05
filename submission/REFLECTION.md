# Reflection — Lab 19

**Tên:** _Lê Hoàng Thiên Phú_
**Mã học viên:** _2A202602908_
**Cohort:** _A20-K4-L3A_
**Path đã chạy:** _docker_

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên 50 golden queries, hybrid đạt Precision@10 cao nhất toàn bộ (78.6%),
cao hơn BM25 (77.8%) và vector (73.2%). Theo từng slice, BM25 và hybrid cùng
mạnh ở `exact` (96.7%) vì các từ khóa xuất hiện trực tiếp; hybrid thắng rõ
nhất ở `mixed` (100.0%) nhờ kết hợp tín hiệu từ cả hai chỉ mục. Với
`paraphrase`, BM25 (33.3%) nhỉnh hơn hybrid (32.0%) và vector (24.0%) trong
lần chạy này. Điều đó cho thấy chất lượng embedding đa ngữ vẫn là biến quan
trọng, không thể mặc định semantic search sẽ luôn tốt hơn.

Tôi dùng hybrid khi truy vấn có thể vừa chứa keyword chính xác vừa diễn đạt
ngữ nghĩa khác đi, và khi có đủ ngân sách latency. Tôi chọn BM25 thuần cho
mã lỗi, tên sản phẩm, định danh, hoặc yêu cầu latency/chi phí thấp. Tôi chọn
vector thuần khi truy vấn chủ yếu là paraphrase đa ngôn ngữ và embedding đã
được đánh giá tốt trên dữ liệu miền; khi đó fusion chỉ làm hệ thống phức tạp
và tăng độ trễ mà không đem lại lợi ích tương xứng.

---

## Điều ngạc nhiên nhất khi làm lab này

Điều ngạc nhiên nhất là hybrid không tự động thắng mọi lát cắt: kết quả
paraphrase kém cho thấy phải đo trên golden set thay vì tin vào trực giác.

---

## Bonus challenge

- [x] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
