# Báo cáo cá nhân — Ngày 11
Họ tên: Võ Tiến Phát              Mã học viên: 2A202603130  
Phiên bản CVAT Server version: 2.82.1 và UI version: 2.82.1
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-20 22:29    Số lần nộp lại sau Rework: 0  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | Đủ `lane`, `road_curb`, `crosswalk` (Polyline/Polygon), `drivable` (Polygon), `traffic_light`, `traffic_sign` (Rectangle). |
| Thuộc tính và giá trị | Đúng | Đối chiếu khớp với đầu ra của `python3 -m road_lab.taxonomy`. |
| 4 tag ảnh | Đúng | Đủ `camera`, `timeofday`, `weather`, `source` trên toàn bộ 20 ảnh. |

Cách kết thúc polyline trên bản CVAT này: Nhấn phím `N` hoặc nhấp đúp chuột trái tại điểm cuối cùng.  
Cách đặt tag ảnh trên bản CVAT này: Mở bảng `Objects` bên phải → chuyển sang tab `Tags` → chọn từng tag trong 4 nhóm (`camera`, `timeofday`, `weather`, `source`) và bấm `Add tag` cho từng frame.  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 31 | 6 | 3 | 22 | 22 | 12 |
| front-extra (đã làm 4 / 4) | 4 | 10 | 3 | 4 | 9 | 7 | 10 |
| fisheye | 8 | 12 | 6 | 6 | 9 | 9 | 4 |
| fisheye-extra (đã làm 4 / 4) | 4 | 0 | 2 | 6 | 2 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05, A06, A07, A09, A11 | `lane` | Tự ước lượng vẽ `L1`/`R1` hay bỏ trống | Không vẽ `lane` thiếu, chỉ vẽ `road_curb` và `drivable` | Thực tế mặt đường tại vị trí đó không sơn vạch kẻ làn; không tự vẽ vạch giả để tránh sai lệch GT (đã xác nhận qua `QC1-02`). |
| A01, A08, A11, A12 | `lane` | Gộp thành 1 polyline hay tách theo nhánh/đoạn | Tách/giữ đúng theo cấu trúc nhánh vạch thực tế | Tại vị trí mở rộng/tách làn có 2 nhánh vạch độc lập cùng phía nên giữ riêng từng polyline theo đúng hình học mặt đường. |
| B02_03177_FV.png | `traffic_light` | Tắt hay bật `edge_zone` | Bật `edge_zone = true` cho 3 đèn sát mép ảnh | Tâm các hộp đèn tại `(1089,74)`, `(88,70)`, `(120,112)` nằm ở vùng rìa ngoài 80% bán kính ống kính fisheye. |
| B07_01216_MVR.png | `lane` | Gán `L1`/`R1` hay `other` | `position = other` | Camera gắn gương bên phải (`fisheye_right`), theo guideline mọi vạch làn trên camera hông/sau đều đặt `other`. |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: [Điền tên bạn được ghép cặp]  Quyết định nhận được: [Đạt / Cần sửa nhẹ]  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-03 (`B07` `lane#1`) | 1 | Đồng ý | Đã sửa `position = other` |
| QC1-11 (`B02` `traffic_light`) | 3 | Đồng ý | Đã bật `edge_zone` |
| QC1-12 (`A07`, `A09`, `A10` trùng điểm) | 3 | Đồng ý | Đã xóa điểm chấm đúp |
| QC1-10 (`A10` `traffic_sign#2` < 8px) | 1 | Đồng ý | Đã xóa box dưới 8px |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `phat-front.zip` | Có | 8 / 8 (`A01`: 3 drivable, 4 lane, 1 traffic_sign) | 6 / 6 (`A02`: 3 drivable, 3 lane) | Có (`camera="front"`) |
| `phat-fisheye.zip` | Có | 6 / 6 (`B01`: 1 crosswalk, 1 drivable, 2 road_curb, 3 traffic_light — tổng 7 shape) | 5 / 5 (`B02`: 1 crosswalk, 1 drivable, 4 traffic_light — tổng 6 shape) | Có (`fisheye_front`, `fisheye_rear`, `fisheye_left`, `fisheye_right`) |

*(Lưu ý kiểm tra lại cột số shape ảnh 1, 2 của `phat-fisheye.zip` là **7 / 7** cho `B01` và **6 / 6** cho `B02` khớp với tổng số đối tượng hiển thị trên CVAT).*

## 6. Ảnh chụp màn hình
1. Tab Labels của project: `![Labels](screenshots/1_labels.png)`
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển): `![Front sample](screenshots/2_front.png)`
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong: `![Fisheye sample](screenshots/3_fisheye.png)`
4. Một đoạn XML có `<polyline label="lane">`: `![XML lane](screenshots/4_xml_lane.png)`

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
Lỗi gặp nhiều nhất là `QC1-12` (click đúp tạo 2 điểm trùng tọa độ trên polyline `lane`) và `QC1-11` (quên tick `edge_zone` ở rìa ảnh fisheye). Cách tránh ở Ngày 20: kết thúc polyline bằng phím `N` thay vì nhấp đúp chuột, đồng thời tạo thói quen kiểm tra đủ thuộc tính (`edge_zone`, `position = other`) ngay trước khi chuyển frame và chạy `lint` sớm.  

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
Các nhãn hình học (`lane`, `drivable`, `road_curb`, `crosswalk`) và hộp (`traffic_light`, `traffic_sign`) được chuyển đổi thành Ground Truth để huấn luyện các bài toán nhận thức đường bộ như phát hiện làn đường (lane detection / row-anchor), phân vùng mặt đường chạy được (drivable area segmentation) và nhận diện biển báo/