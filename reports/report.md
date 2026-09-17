# Báo Cáo Kết Quả Thực Hành Phân Đoạn (Segmentation Lab)

- **Mã học viên theo lớp:** 2A202602274
- **Ngày / CVAT local:** 17/09/2026 / CVAT local
- **Công cụ đã dùng:** Brush, Polygon, Intelligent Scissors

## 1. Bài đã nộp

Dựa trên kết quả tự kiểm tra bằng notebook `day5-segmentation-tu-kiem.ipynb`, tất cả các tasks đã được export và nộp thành công với định dạng chuẩn (Trạng thái OK).

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | `cp1_holes.zip` | 1 / 1 | 3 |
| cp2_slice | `cp2_slice.zip` | 1 / 1 | 3 |
| cp5_occlusion | `cp5_occlusion.zip` | 1 / 1 | 3 |
| cp3_thin | `cp3_thin.zip` | 1 / 1 | 3 |
| cp4_curb | `cp4_curb.zip` | 1 / 1 | 3 |
| cp6_coverage | `cp6_coverage.zip` | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

## 2. Một quyết định trước khi dùng gợi ý

- **Ảnh, vị trí và object Medium đầu tiên tự vẽ:** `000000181542.jpg` (medium_instance) - Đối tượng: Xe ô tô.
- **Class và quy tắc tôi dùng để chọn biên:** Class `car`. Tôi chọn vẽ theo đường viền nhìn thấy rõ ràng của thân xe, loại bỏ phần bị che khuất để đảm bảo tính chính xác của instance.
- **Nếu dùng gợi ý sau đó:** Không dùng gợi ý tự động cho xe này do có nhiều chi tiết góc cạnh cần độ tỉ mỉ cao (chủ yếu sử dụng Polygon và Brush để đi sát viền).

## 3. Một lỗi tôi tìm thấy và sửa

- **Task/ảnh/vùng:** `cp2_slice` / ảnh `000000017627.jpg`
- **Lỗi thuộc loại:** gộp-tách (Gộp hai đối tượng xe sát nhau thành một mask duy nhất).
- **Bằng chứng tôi nhìn thấy:** Khi kiểm tra kỹ khu vực đỗ xe, có một khe hở nhỏ chia cắt ranh giới giữa 2 xe, nhưng mask vô tình bị dính vào nhau.
- **Quy tắc và hành động sửa:** Áp dụng quy tắc mỗi xe độc lập là một instance. Tôi đã dùng công cụ xóa/chỉnh biên để tách mask gộp thành hai phần độc lập.
- **Sau sửa đã Save và export lại chưa?** Đã Save trên CVAT và export lại file ZIP.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `cp1_holes` (Kính xe buýt) | Giữ nguyên lỗ hổng hay vẽ kín | Kính là thành phần xuyên thấu của xe buýt | Chọn vẽ kín toàn bộ thân xe buýt bao gồm kính, tuân thủ quy tắc không tự khoét lỗ. |
| `cp5_occlusion` (Vật bị che) | Tách thành 2 mask hay gộp thành 1 mask | Hai phần nhìn thấy thuộc cùng một đối tượng duy nhất | Gộp chung thành 1 mask cho cùng một instance. |
| `cp4_curb` (Ranh giới vỉa hè) | Thuộc `road` hay `sidewalk` | Phần gờ nổi lên có kết cấu giống vỉa hè hơn | Chọn gán nhãn là `sidewalk`. Mong coach xác nhận thêm về cách gán mép bó vỉa. |
