# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Đinh Thành Vinh (2A202603044)       Người kiểm (học viên): Võ Tiến Phát (2A202603130)  
Ngày: 21/11/2026                     Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `vinh-front.zip`, `vinh-fisheye.zip` (revision 1)  
Số ảnh kiểm: 20 (+ 4 ảnh thêm `A13–A16`, kiểm toàn bộ qua `lint`)   Số nhãn đã kiểm (shape + tag): Toàn bộ shape & tag trong 24 ảnh  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 24 | 4 *(6 ca ngoại lệ)* | nặng |
| QC1-03 position | sai thuộc tính / thừa | 24 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 24 | 33 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 24 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 24 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 24 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 24 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 24 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 24 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 8 | 8 | chính |
| QC1-12 file | lỗi file | 24 | 1 | nhẹ |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-12 | `A01` | `lane#0@(333,505)` | nhẹ | Trùng 2 điểm liền nhau (click đúp), cần xóa 1 điểm thừa. |
| 2 | QC1-04 | `A01` | `lane#0, #4, #5, #6` | chính | Vẽ ngược chiều polyline (từ xa về gần). Cần đảo chiều từ dưới lên trên. |
| 3 | QC1-04 | `A02` | `lane#3, #4` | chính | Vẽ ngược chiều polyline (điểm đầu cao hơn điểm cuối). |
| 4 | QC1-04 | `A03` | `lane#1, #2` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 5 | QC1-04 | `A04` | `lane#0, #3` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 6 | QC1-04 | `A06` | `lane#11@(48,405)` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 7 | QC1-04 | `A07` | `lane#1@(695,273)` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 8 | QC1-04 | `A08` | `lane#7, #10` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 9 | QC1-04 | `A09` | `lane#0, #3` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 10 | QC1-04 | `A10` | `lane#1, #2` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 11 | QC1-04 | `A11` | `lane#5, #6` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 12 | QC1-04 | `A12` | `lane#4@(541,381)` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 13 | QC1-04 | `A13` | `lane#2, #4, #5` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 14 | QC1-04 | `A14` | `lane#0, #6` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 15 | QC1-04 | `A15` | `lane#2, #3, #4` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 16 | QC1-04 | `A16` | `lane#0, #1, #2, #4` | chính | Vẽ ngược chiều polyline (từ xa về gần). |
| 17 | QC1-02 | `A08, A10, A12, A14` | `lane` (`L1` / `R1`) | nặng | Thiếu nhãn `L1` (`A08`) hoặc `R1` (`A10, A12, A14`); cần kiểm tra lại xem có vẽ sót hoặc gán nhầm `position` không. |
| 18 | QC1-11 | `B02` | `lane#0@(39,558)` | chính | Chỉ có 3 điểm trên ảnh fisheye; cần thêm điểm trung gian bám theo cung cong của vạch. |
| 19 | QC1-11 | `B03` | `lane#0, #1`, `road_curb#4` | chính | Mỗi đường chỉ có 3 điểm; chưa ôm sát độ cong ống kính fisheye. |
| 20 | QC1-11 | `B04` | `lane#0@(598,266)` | chính | Chỉ có 3 điểm trên ảnh fisheye; cần đặt thêm điểm theo độ cong vạch. |
| 21 | QC1-11 | `B07` | `lane#2, #3` | chính | Chỉ có 3 điểm trên ảnh fisheye; cần bổ sung điểm theo cung cong. |
| 22 | QC1-11 | `B08` | `lane#1@(62,745)` | chính | Chỉ có 2 điểm nối thẳng trên ảnh fisheye; cần bổ sung điểm theo cung cong. |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| `A05`, `A06`, `A07`, `A09` | `lint` báo `[QC1-02]` thiếu `L1`/`R1` nhưng thực tế mặt đường tại hiện trường không sơn vạch làn. | Xác nhận ngoại lệ hợp lệ: không vẽ thêm vạch giả, giữ nguyên bài làm. |

## Quyết định
Lỗi nặng: 0 *(4 ca `QC1-02` cần rà soát lại)*   Lỗi chính: 41 / 24 ảnh   Lỗi nhẹ: 1   Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Tồn tại số lượng lớn lỗi mức **chính** mang tính hệ thống (33 lỗi vẽ ngược chiều polyline `QC1-04` trên bộ `front` và 8 lỗi thiếu điểm uốn cong `QC1-11` trên bộ `fisheye`). Cần dùng tính năng *Switch direction* trên CVAT để đảo chiều làn và bổ sung điểm trung gian trên ảnh fisheye trước khi xuất lại.