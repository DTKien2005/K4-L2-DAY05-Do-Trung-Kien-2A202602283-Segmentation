# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Họ và tên: Đỗ Trung Kiên
- Mã học viên theo lớp: 2A202602283
- Ngày / CVAT local: 18/09/2026 / CVAT local (http://localhost:8080)
- Công cụ đã dùng: Brush, Polygon, CVAT local

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | --- | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `000000181542.jpg`, chiếc xe hơi (`car`) màu đỏ/sẫm ở tiền cảnh góc dưới bên trái của ảnh.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Tôi dùng Polygon/Brush vẽ sát mép thân xe nhìn thấy được; dừng biên ngay tại mép gương chiếu hậu và lốp xe tiếp giáp mặt đường, không bao gồm bóng đổ (`shadow`) của xe dưới mặt đường vào mask của `car`.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Khi thử công cụ tự động, phần bóng đổ dưới gầm xe và bánh xe hay bị lấn gộp vào thân xe; tôi đã dùng Brush chế độ Eraser xóa phần bóng đổ này để mask ôm đúng biên vỏ xe và lốp xe.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình: Có sử dụng kết hợp và đã kiểm tra chỉnh sửa lại biên bằng tay.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `medium_instance`, ảnh `000000181542.jpg` (phố chợ đông người) và Task `easy_semantic`, ảnh `817bca71-00000000.jpg`.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: Sai lớp đối tượng xe và thừa các bounding box nhiễu ở nền; phân định ranh giới bó vỉa hè (`sidewalk` vs `road`).
- Bằng chứng tôi nhìn thấy: Ở ảnh `000000181542.jpg`, chiếc xe tải lớn chở hàng màu xanh/trắng ban đầu bị gán nhầm thành `car`; đồng thời có 35 mask nhỏ li ti (1–4 px) và một số người bị gán nhầm vào cột đèn/bụi cây; thiếu chiếc xe máy ở sát mép trái. Ở `easy_semantic`, ranh giới vỉa hè và mặt đường bị lấn vào nhau do chói sáng.
- Quy tắc và hành động sửa: Đổi nhãn chiếc xe tải sang `truck`; xóa sạch toàn bộ 35 đối tượng thừa/nhiễu; vẽ bổ sung xe máy và người đi bộ bị sót; ở semantic phóng to mép gờ bó vỉa (curb) phân định chuẩn `road` và `sidewalk`.
- Sau sửa đã Save và export lại chưa? Đã Save trực tiếp trên các job CVAT local và export lại đầy đủ các file ZIP nộp bài.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có):

| Task | Metric | Điểm trước | Điểm sau tối ưu | Kết quả ghi nhận |
| :--- | :---: | :---: | :---: | :--- |
| `easy_semantic` | mIoU = 0.851 | 15.7 / 20 | **20.0 / 20** | Phủ chuẩn thảm thực vật và ranh bó vỉa |
| `medium_instance` | Metric = 0.825 | 17.2 / 32 | **30.2 / 32** | Chuẩn hóa `truck`, P@0.5=1.00, R@0.5=1.00 (71/71 TP) |
| `hard_panoptic` | PQ = 0.694 | 15.6 / 30 | **30.0 / 30** | Chỉnh đúng sân vỉa hè `sidewalk`, dọn 22 xe rác |
| **Tổng tự đánh giá** | | **48.5 / 82** | **80.2 / 82** | **Đạt 80.2 / 82 điểm (không cờ nghi vấn)** |

Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. `cp4_curb` (ảnh `7d83710e-4697c3b2.jpg`), đoạn dốc bó vỉa hạ thấp cùng chất liệu nhựa đường | (1) Coi toàn bộ mảng cùng màu nhựa đường là `road`; hoặc (2) Phân tách phần vỉa hè nâng cao là `sidewalk` | Quy tắc ranh giới chức năng và độ cao địa hình gờ bó vỉa, không phụ thuộc vào màu vật liệu | Quyết định gán phần nâng cao là `sidewalk`, phần xe chạy là `road`. Câu hỏi cho coach: Với đoạn dốc nối lối xe vào nhà (driveway), nên quy về `sidewalk` hay `road`? |
| 2. `cp1_holes` (ảnh `000000144300.jpg`), kính cửa sổ ô tô nhìn xuyên thấu qua nền phía sau | (1) Khoét rỗng kính xe để lộ nền phía sau; hoặc (2) Phủ kín toàn bộ xe bao gồm cả kính | Quy tắc đặc thù của `cp1_holes`: "Holes: windows/gaps stay inside the mask — do NOT cut them out" | Quyết định giữ kín toàn bộ kính trong mask của `car`, tuyệt đối không khoét lỗ |
| 3. `cp5_occlusion` (ảnh `000000336232.jpg`), xe tải/ô tô bị cột biển báo chắn ngang cắt đôi thân xe thành 2 phần rời rạc | (1) Tách thành 2 mask/instance riêng biệt vì 2 cụm pixel rời nhau; hoặc (2) Gộp chung thành 1 instance | Quy tắc Instance segmentation: một vật thể duy nhất bị vật khác che khuất một phần vẫn là 1 instance duy nhất | Quyết định tạo multi-polygon/gộp chung thành 1 mask instance duy nhất cho chiếc xe đó |
