# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: Hồ Minh Hậu - 202602058
- Ngày / CVAT local: 18/09/2026
- Công cụ đã dùng: cvat

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic |easy_semantic.zip | 3 / 3 | 20 |
| medium_instance |medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic |hard_panoptic.zip |2 / 2 | 30 |
| cp1_holes |cp1_holes.zip |1 / 1 | 3 |
| cp2_slice |cp2_slice.zip |1 / 1 | 3 |
| cp5_occlusion |cp5_occlusion.zip |1 / 1 | 3 |
| cp3_thin |cp3_thin.zip |1 / 1 | 3 |
| cp4_curb |cp4_curb.zip |1 / 1 | 3 |
| cp6_coverage |cp6_coverage.zip |1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Task `medium_instance`, ảnh phố đi bộ đen trắng (`000000373353.jpg`), vị trí chính giữa ảnh — người phụ nữ mặc áo dài trắng đang đi bộ qua đường.
- Class và quy tắc tôi dùng để chọn biên: Class `person` (màu đỏ `#dc143c`). Quy tắc chọn biên: Vẽ bám sát vóc dáng và hai tà áo dài đè lên chiếc xe máy phía sau (xử lý che khuất/occlusion); tách hoàn toàn đối tượng người đi bộ ra khỏi người lái và xe máy bên cạnh.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: không dùng
- Nếu không dùng gợi ý: không dùng; tôi tự tay sử dụng công cụ Polygon vẽ viền chi tiết cho người phụ nữ (`person`) để bảo đảm ranh giới sắc nét và phân tách chuẩn định dạng Instance Segmentation với chiếc xe máy (`motorcycle`) phía sau.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `medium_instance`, ảnh thứ 2 (ảnh phố New York có hàng xe đỗ dọc lề đường bên trái).
- Lỗi thuộc loại: gộp-tách (gộp các xe đỗ sát nhau thành một mask duy nhất).
- Bằng chứng tôi nhìn thấy: Ban đầu vẽ một polygon lớn trùm lên toàn bộ hàng xe van/ô tô đỗ sát nhau bên lề đường trái; quan sát thấy rõ khe hở giữa các xe và bánh xe riêng biệt nhưng đang bị dính chung mask.
- Quy tắc và hành động sửa: Theo quy tắc Instance Segmentation (các xe cạnh nhau phải là instance riêng biệt), tôi đã cắt và phân tách polygon gộp ban đầu thành từng mask `car` độc lập cho từng chiếc xe đỗ nối đuôi nhau.
- Sau sửa đã Save và export lại chưa?: Đã Save trên CVAT và export lại file `medium_instance.zip` vào thư mục `submissions/`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Metric của `medium_instance` tăng từ 0.501 (7.2 điểm) lên 0.548 (10.5 điểm) sau khi tách rời các xe và export lại. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `easy_semantic` — Ảnh `817bca71-00000000.jpg` (dãy nhà) | Tách riêng từng ngôi nhà hay tô gộp thành mảng `building`? | Task là Semantic Segmentation (chỉ gán nhãn theo lớp pixel, không yêu cầu tách rời instance từng vật). | Tôi chọn tô gộp thành mảng `building`; xin coach xác nhận trong Semantic có cần tách ranh từng căn nhà kề nhau không? |
| `medium_instance` — Ảnh `000000181542.jpg` (xe bus) | Có nên gán nhãn `person` cho các bóng người nhìn thấy mờ qua cửa kính xe bus không? | Nhận diện được hình dáng người (head/silhouette) đằng sau lớp kính mờ. | Quyết định vẫn khoanh nhãn `person`; xin coach xác nhận các đối tượng nhìn mờ qua kính xe có bắt buộc đánh nhãn không? |
| `hard_panoptic` — Ảnh `000000460147.jpg` (xe tải chở ô tô) | Nên gán nhãn gộp cả xe tải + các ô tô chở theo thành 1 `truck` hay tách riêng từng ô tô `car` trên thùng xe? | Các ô tô trên xe tải là hàng hóa chở theo nhưng vẫn là hình dáng xe ô tô hoàn chỉnh. | Tôi chọn tách riêng từng ô tô trên thùng xe thành nhãn `car` và khung xe tải là `truck`; xin coach xác nhận cách chia instance này. |
